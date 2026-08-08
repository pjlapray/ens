# ⏱️ Délai de propagation ($t_{pd}$)

Dans un composant réel, le changement d'état en sortie n'est pas instantané. Le temps nécessaire au signal pour traverser les transistors est appelé **délai de propagation**.

wavedrom(
{ "signal": [
  { "name": "Entrée A", "wave": "0.1.......0.", "node": "..a.......c" },
  { "name": "Sortie Y", "wave": "0..1.......0", "node": "...b.......d" }
],
  "edge": [
    "a<->b t_pd", 
    "c<->d t_pd"
  ],
  "head": {
    "text": "Illustration du retard de propagation sur un Buffer",
    "tick": 0
  },
  "config": { "hscale": 1.5 }
}
)

**Explications pour les étudiants :**
- L'arc `t_pd` montre que la sortie $Y$ ne monte à '1' qu'un court instant après l'entrée $A$.
- Ce délai est critique pour les circuits à haute fréquence car il limite la vitesse maximale de l'horloge.

J'ai mis à jour le **Canvas** pour inclure ces optimisations de rendu. Les arcs de mesure (`edge`) dans WaveDrom sont l'outil parfait pour pointer visuellement ce décalage.


# La Métastabilité

En logique séquentielle, le respect du timing est crucial. Si l'entrée **D** change d'état précisément au moment du front d'horloge (**CLK**), la bascule entre dans un état instable appelé **métastabilité**.

## Le danger
Dans cet état, la sortie $Q$ ne sait pas si elle doit passer à `0` ou à `1`. Elle peut rester bloquée entre deux tensions pendant quelques nanosecondes ou osciller follement.



!!! warning "Conséquence système"
    Un signal métastable peut provoquer des erreurs imprévisibles (crashs) car il pourrait être interprété différemment par les circuits logiques qui suivent.


## Représentation du signal instable
wavedrom (
{ "signal": [
  { "name": "CLK", "wave": "p..p..p" },
  { "name": "D",   "wave": "0.x0.x1", "desc": "Violation du setup time" },
  { "name": "Q",   "wave": "0.x..=.", "data": ["Stable"] }
],
  "head": { "text": "Zone d'incertitude temporelle" }
}
)

## Comment l'éviter ?
Pour sécuriser un signal asynchrone (comme un bouton-poussoir), on utilise un **synchroniseur** : on place deux bascules D en série.
1. La première bascule encaisse l'instabilité potentielle.
2. La deuxième bascule récupère un signal stabilisé au coup d'horloge suivant.


# Timing Setup ($t_s$) et Hold ($t_h$)
Ce schéma définit la "fenêtre de stabilité" autour du front d'horloge.
### ⏳ Fenêtre de métastabilité et contraintes temporelles

Pour garantir un fonctionnement déterministe, le signal de donnée $D$ ne doit subir aucune transition dans la zone rouge.

wavedrom(
{ "signal": [
  { "name": "CLK", "wave": "l.P...", "node": "..c" },
  { "name": "D",   "wave": "x.2.x.", "node": ".ab", "data": ["STABLE"] },
  { "name": "Q",   "wave": "x...2.", "node": "....q" }
],
  "edge": [
    "a-b", "c-b", "c-a",
    "a<->c t_su",
    "c<->b t_h",
    "c<->q t_co"
  ],
  "config": { "hscale": 3 }
}
)