### ⏱️ Le délai de propagation ($t_{pd}$)

Dans un composant logique ou une bascule D réels, le changement d'état en sortie $Q$ n'est pas instantané après une modification de l'entrée $D$ ou du front d'horloge. 

Le temps nécessaire au signal électrique pour traverser les transistors et stabiliser la sortie est appelé **délai de propagation** ($t_{pd}$, pour *propagation delay*).

* **Points clés à retenir :**
	* **Inertie physique :** Comme le montre le chronogramme ci-dessus, la sortie $Q$ met un temps $t_{pd}$ pour recopier le niveau logique de l'entrée $D$.
	* **Fréquence maximale :** Ce délai limite la vitesse de fonctionnement du circuit. Plus $t_{pd}$ est grand, plus la fréquence d'horloge maximale du système doit être réduite.


```tikz
\documentclass{standalone}
\usepackage{tikz}
\usetikzlibrary{arrows.meta, positioning, calc}
\usepackage{circuitikz}

\begin{document}
\begin{tikzpicture}[>=Stealth, font=\sffamily\small]


    % --- Partie Gauche : Schéma de la Bascule ---
    \begin{scope}[shift={(0,1.5)}]
       % Draw a D flip-flop node
  \node[flipflop D] (D1) at (0,0) {};
  
  % Connect or label the pins using built-in anchors
  \node[left] at (D1.pin 1) {entrée};
  \node[left] at (D1.pin 3) {Clk};
  \node[right] at (D1.pin 6) {sortie};
  \node[right] at (D1.pin 4) {};
    \end{scope}

    % --- Partie Droite : Chronogramme ---
    \begin{scope}[shift={(5.5,0)}]
        % Alignement temporel du front d'horloge (x = 3)
        % Lignes de repère verticales
        \draw[gray!60, dashed, thick] (1.8, -0.5) -- (1.8, 4.2); % Fin Setup / Début Hold (Front CLK)
        \draw[red!60, dashed] (0.8, -0.5) -- (0.8, 4.2);        % Début Setup
        \draw[green!60!black, dashed] (2.8, -0.5) -- (2.8, 4.2); % Fin Hold

        % Signal Input
        \node[left, font=\bfseries, orange!90!black] at (-0.6, 3.5) {entrée};
        \draw[thick, orange!90!black] (-0.6,3) -- (0.1,3) -- (0.4,4) -- (2.8,4) --  (3.3,4) -- (3.6,3) -- (4.5,3);

        % Signal CLK
        \node[left, font=\bfseries, cyan!80!black] at (-0.6, 2) {CLK};
        \draw[thick, cyan!80!black] (-0.6,1.5) -- (1.5,1.5) -- (1.8,2.5) -- (4.2,2.5) -- (4.5,1.5);
        \draw[->, cyan!80!black, ultra thick] (1.8, 1.6) -- (1.8, 2.3); % Flèche du front montant

        % Signal Output
        \node[left, font=\bfseries, orange!70!black] at (-0.6, 0) {sortie};
        \draw[thick, orange!70!black] (-0.6,-0.3) -- (2.2,-0.3) -- (2.5,0.5) -- (4.5,0.5);

        % Cotations t_setup et t_hold
        % t_setup (entre x=0.8 et x=1.8)
        \draw[<->, red!80!black, thick] (0.8, 2.8) -- (1.8, 2.8) node[midway, above, font=\scriptsize\bfseries] {$t_{setup}$};
        
        % t_hold (entre x=1.8 et x=2.8)
        \draw[<->, green!50!black, thick] (1.8, 2.8) -- (2.8, 2.8) node[midway, above, font=\scriptsize\bfseries] {$t_{hold}$};

        % Cotation t_cq / t_pd
        \draw[<->, blue!80!black, thick] (1.8, 0.5) -- (2.5, 0.5) node[midway, above, font=\scriptsize\bfseries] {$t_{pd}$};
    \end{scope}

\end{tikzpicture}
\end{document}
```

---

### ⚠️ Le phénomène de Métastabilité

* En logique séquentielle, la donnée $D$ doit rester parfaitement **stable** pendant une fenêtre temporelle stricte autour du front d'horloge :
	*  **Temps de setup ($t_{su}$) :** La donnée doit être stable *avant* le front d'horloge.
	*  **Temps de hold ($t_{h}$) :** La donnée doit rester stable *après* le front d'horloge.

Si l'entrée $D$ change d'état à l'intérieur de cette fenêtre critique, la bascule ne parvient pas à décider si la valeur capturée est un `0` ou un `1`. Elle entre alors dans un état instable appelé **métastabilité**.

