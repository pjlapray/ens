# Logique séquentielle

La logique séquentielle diffère de la logique combinatoire par l'introduction de la notion de **mémoire**. L'état des sorties ne dépend plus uniquement des entrées actuelles, mais aussi de l'historique des états précédents.

## Les circuits séquentiels élémentaires

Les briques de base de la logique séquentielle sont les **verrous et bascules** (latches et flip-flops), capables de mémoriser un bit d'information.

!!! info "Laboratoire Virtuel : Les Bascules RS, D et JK"
    Utilisez le simulateur interactif ci-dessous pour tester le comportement des différentes bascules. Observez particulièrement la différence entre une commande sur **niveau** (verrou ou latch) et sur **front** (bascule ou flip-flop).

    <div class="circuit-container" style="text-align: center; margin: 20px 0;">
        <iframe 
            src="https://circuitverse.org/simulator/embed/elec-num-partie-3-9cc032fe-5536-4bd0-9568-119b1518c853?theme=lite-born-spring&display_title=true&clock_time=false&fullscreen=false&zoom_in_out=true" 
            style="border: 2px solid #2c3e50; border-radius: 10px; box-shadow: 0 4px 8px rgba(0,0,0,0.2);" 
            name="myiframe" 
            id="projectPreview" 
            scrolling="no" 
            frameborder="0" 
            height="350" 
            width="80%" 
            allowFullScreen>
        </iframe>
    </div>


### Points clés à observer :
* **Bascule RS :** Notez l'état interdit ($R=1, S=1$).
* **Bascule D :** Observez comment la donnée est "verrouillée" ou mémorisée.
* **Horloge (Clock) :** Identifiez si le changement se fait sur le front montant ou descendant.
## Le Registre à Décalage

Le registre à décalage est un circuit séquentiel capable de transformer une donnée **Série** (un bit après l'autre) en données **Parallèles** (plusieurs bits disponibles simultanément).
Il résout un problème majeur : le manque de broches sur un microcontrôleur.

Ci-après une simulation du principe, avec un registre à décalage de 4-bit.

=== ":material-chip: Simulation Logique (CircuitVerse)"
	<div class="circuit-container" style="text-align: center; margin: 20px 0;">
		<iframe src="https://circuitverse.org/simulator/embed/untitled-33a0e2d3-a7b2-4ac9-b251-3b190e37a715" 
				style="border: 2px solid #2c3e50; border-radius: 10px;" 
				height="400" 
				width="100%" 
				allowFullScreen>
		</iframe>
	</div>
	
---

### Simulation et Expérimentation

Le montage suivant sous TinkerCad permet de tester manuellement le registre à décalage 8-bit 74HC595. Il y a 3 entrées clés :

1. **SER (Data Serial) :** Définit la valeur du bit à faire rentrer (0 ou 1).
2. **SCK (Shift Clock) :** À chaque front montant, le bit présent sur SER entre dans le registre et décale les autres.
3. **RCK (Read Clock / Latch) :** Transfère tout le contenu du registre interne vers les sorties physiques (les LED).


!!! info "Simulation technologique"
	Observez comment les données "voyagent" dans le composant avant d'être affichées.
	
	=== ":material-chip: Simulation Techno (Tinkercad)"
		<div style="border: 1px solid #dee2e6; border-radius: 8px; padding: 10px; background: #f8f9fa; margin: 20px 0; text-align: center;">
			<iframe width="725" height="353" src="https://www.tinkercad.com/embed/fuTHfCgIBA3?editbtn=1" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>
			<p><em>Utilisation du 74HC595 pour piloter 8 LED.</em></p>
		</div>

---

wavedrom(
{ "signal": [
  { "name": "SCK (Horloge)", "wave": "p........." },
  { "name": "SER (Donnée)",    "wave": "010110....", "data": ["D0", "D1", "D2", "D3"] },
  {},
  { "name": "Interne Q0",     "wave": "0.10110..." },
  { "name": "Interne Q1",     "wave": "0..10110.." },
  { "name": "Interne Q2",     "wave": "0...10110." },
  { "name": "..."},
  { "name": "RCK (Verrou)",  "wave": "0.......10" },
  { "name": "Sorties (Qn)",   "wave": "x.......=x", "data": ["DATA"] }
],
  "head": {
    "text": "Fonctionnement du 74HC595",
    "tick": 0
  },
  "config": { "hscale": 1.5 }
}
)