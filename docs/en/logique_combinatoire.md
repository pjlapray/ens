# Logique Combinatoire Complexe

## 1. Les portes logiques élémentaires

Avant d'aborder les circuits complexes, il est essentiel de maîtriser les briques de base : les portes logiques.

<div class="circuit-container" style="text-align: center; margin: 20px 0;">
    <iframe src="https://circuitverse.org/simulator/embed/portes-logiques-fad4de60-2f75-429a-b10a-6e1eed13cf84?theme=default&display_title=false&clock_time=false&fullscreen=true&zoom_in_out=true" 
            style="border: 2px solid #2c3e50; border-radius: 10px;" 
            name="myiframe" 
            id="projectPreview" 
            scrolling="no" 
            frameborder="0" 
            height="340" 
            width="80%" 
            allowFullScreen>
    </iframe>
</div>

---

## 2. L'Additionneur Complet (1-bit Full Adder)

L'additionneur complet est l'unité de base du calcul numérique. Contrairement au demi-additionneur, il prend en compte une retenue d'entrée ($C_{in}$), permettant de cascader plusieurs unités pour additionner des nombres de plusieurs bits.

### Analyse et Conception

=== ":material-table: Table de Vérité"
    | $A$ | $B$ | $C_{in}$ | $S$ (Somme) | $C_{out}$ (Retenue) |
    |:---:|:---:|:---:|:---:|:---:|
    | 0 | 0 | 0 | **0** | **0** |
    | 0 | 0 | 1 | **1** | **0** |
    | 0 | 1 | 0 | **1** | **0** |
    | 0 | 1 | 1 | **0** | **1** |
    | 1 | 0 | 0 | **1** | **0** |
    | 1 | 0 | 1 | **0** | **1** |
    | 1 | 1 | 0 | **0** | **1** |
    | 1 | 1 | 1 | **1** | **1** |

=== ":material-sitemap: Logigramme"
    L'additionneur calcule deux fonctions logiques :
	
    * **Somme ($S$)** : $A \oplus B \oplus C_{in}$ (vrai si un nombre impair d'entrées est à 1).
    * **Retenue ($C_{out}$)** : Vrai si au moins deux entrées sont à 1.

    wavedrom (
    { "assign": [
        ["S", ["^", "A", "B", "Cin"]],
        ["Cout", ["|", ["&", "A", "B"], ["&", "B", "Cin"], ["&", "A", "Cin"]]]
    ]}
    )
	
=== ":material-chip: Simulation Logique (CircuitVerse)"
	<div class="circuit-container" style="text-align: center; margin: 20px 0;">
		<iframe src="https://circuitverse.org/simulator/embed/additionneur-complet-9a573fbc-972c-43cd-ae37-bbbd50f4fa93" 
				style="border: 2px solid #2c3e50; border-radius: 10px;" 
				height="400" 
				width="100%" 
				allowFullScreen>
		</iframe>
	</div>
	
=== ":material-chip: Simulation Techno (Tinkercad)"
    <div style="border: 1px solid #dee2e6; border-radius: 8px; padding: 10px; background: #f8f9fa; margin: 20px 0; text-align: center;">
        <iframe width="725" height="453" src="https://www.tinkercad.com/embed/hbotEYDtzwv?editbtn=1" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>
        <p><em>Mise en œuvre avec des circuits intégrés de la série 74HC.</em></p>
    </div>

---

## 3. Aiguillage : Mux, Demux et Décodeur

Ces circuits ne transforment pas l'information, ils la dirigent. Ils sont essentiels pour la sélection de données ou l'adressage mémoire.

<div class="circuit-container" style="text-align: center; margin: 20px 0;">
    <iframe src="https://circuitverse.org/simulator/embed/elec-num-partie-2?theme=default&display_title=false&clock_time=false&fullscreen=true&zoom_in_out=true" 
            style="border: 2px solid #2c3e50; border-radius: 10px;" 
            height="400" 
            width="100%" 
            allowFullScreen>
    </iframe>
</div>

### Le Multiplexeur (MUX)
Le Multiplexeur agit comme un entonnoir : il sélectionne l'une des entrées pour la diriger vers la sortie unique, selon l'état d'une entrée de sélection ($Sel$).



* **Application :** Sélectionner quelle variable afficher sur un écran unique.

### Le Démultiplexeur (DEMUX)
C'est l'inverse du MUX : il dirige une donnée d'entrée vers l'une des multiples sorties possibles.



### Le Décodeur
Le décodeur active une sortie spécifique parmi $2^n$ en fonction d'un code binaire en entrée.

* **Exemple (2 vers 4) :** * Entrée `00` $\rightarrow$ Sortie 0 active.

    * Entrée `10` $\rightarrow$ Sortie 2 active.



!!! info "Le saviez-vous ?"
    Un décodeur est souvent utilisé pour transformer un nombre binaire en un affichage lisible (par exemple, un décodeur 7 segments pour afficher les chiffres).