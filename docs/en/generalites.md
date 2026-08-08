# Logique Combinatoire vs Séquentielle

Il est très important de faire la distinction fondamentale entre les deux types de circuits logiques.

## 1. Concepts Fondamentaux

Pour comprendre l'électronique numérique, il faut différencier la manière dont un circuit réagit à ses entrées :

* **Logique Combinatoire :** La sortie est une fonction directe des entrées à l'instant $t$. Si l'entrée change, la sortie change immédiatement (aux temps de propagation près). Le circuit n'a aucune mémoire.
* **Logique Séquentielle :** La sortie dépend des entrées actuelles, mais aussi de l'état précédent. Le circuit possède une mémoire ("état").

---

## 2. Exemple

Le circuit ci-dessous permet de comparer deux comportements à partir d'un bouton poussoir :
1.  **En haut (Combinatoire) :** Une simple lampe pilotée par un interrupteur.
2.  **En bas (Séquentiel) :** Un télérupteur (réalisé ici avec une bascule D).

=== ":material-chip: Simulation logique (CircuitVerse)"
	<div class="circuit-container" style="text-align: center; margin: 20px 0;">
		<iframe 
			src="https://circuitverse.org/simulator/embed/elec-num-partie-1?theme=g-and-w&display_title=false&clock_time=false&fullscreen=true&zoom_in_out=true" 
			style="border: none; overflow: hidden;" 
			name="myiframe" 
			id="projectPreview" 
			scrolling="no" 
			frameborder="0" 
			marginheight="0" 
			marginwidth="0" 
			height="400" 
			width="100%" 
			allowFullScreen>
		</iframe>
	</div>

=== ":material-chip: Simulation Techno (Tinkercad)"

    <div style="border: 1px solid #dee2e6; border-radius: 8px; padding: 10px; background: #f8f9fa; margin: 20px 0;">
        <iframe width="725" height="453" src="https://www.tinkercad.com/embed/bHByAgWqSC8?editbtn=1" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>
        <p><em>Vue du câblage.</em></p>
    </div>
---

## 3. Analyse du chronogramme

wavedrom (
   {     
   "signal": [
  { "name": "Bouton (Entrée)",      "wave": "010...10..", "node": "..A...B.." },
  {},
  { "name": "Combinatoire (Sortie)", "wave": "010...10..", "node": "..C...D.." },
  { "name": "Séquentiel (Sortie)",   "wave": "01....0...", "node": ".E....F..." }
],
  "edge": [
    "E<->F maintien d'état"
  ],
  "config": { 
    "hscale": 1.0
	}
}
)

---


### Le système combinatoire (L'interrupteur)
Ici, l'état de la lampe est une copie conforme de l'état de l'interrupteur. 

* Si le bouton est **appuyé** ($1$), la lampe est **allumée** ($1$).
* Si le bouton est **relâché** ($0$), la lampe est **éteinte** ($0$).


### Le système séquentiel (Le télérupteur)
Le télérupteur est le plus petit système séquentiel. Il utilise une impulsion pour changer d'état.
Le système "se souvient" s'il était allumé ou éteint pour décider du prochain état. 


