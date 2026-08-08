# Immersion ASE

## 🌿 Liste du matériel : Prototype Serre Connectée

Ce tableau présente les composants nécessaires pour le nouveau support pédagogique de serre automatisée. Ce système est conçu pour être alimenté par la **platine 3.3V / 5V / 12V** de JJ.



| Composant | Fonction principale | Atelier | Prix | Lien RS |
| :--- | :--- | :---: | :---: | :--- |
| :material-check-decagram-outline: **Arduino Uno** | "Cerveau" du système : gestion des cycles. | Tous | Stock | <a href="https://fr.rs-online.com/web/p/processeurs-et-microcontroleurs/7697409" target="_blank">Voir</a> |
| **Capteur Humidité Sol** | Mesure analogique du taux d'eau. | At. 2 | 2,50 € | <a href="https://fr.rs-online.com/web/p/kits-et-cartes-compatibles-arduino/2163778?gb=a" target="_blank">Voir</a> |
| :material-check-decagram-outline: **Capteur DHT22** | Température et humidité de l'air. | At. 2 | 4,50 € | <a href="https://www.digikey.fr/fr/products/detail/digilent-inc/410-347/6679813" target="_blank">Voir</a> ou <a href="https://www.lextronic.fr/module-capteur-temperature-et-humidite-dht22-64326.html" target="_blank">Voir</a> |
| **Bande LED RGB** | Gestion du spectre (suivant la variété) et indicateur d'état possible. | At. 1 | 8,00 € | <a href="https://fr.rs-online.com/web/p/rubans-led/1807502" target="_blank">Voir</a> |
| **Mini-pompe (12V)** | Actionneur pour l'irrigation. | At. 4 | 20,00 € | <a href="https://www.lextronic.fr/mini-pompe-a-eau-1-1-l-min-11296.html" target="_blank">Voir</a> ou <a href="https://www.leroymerlin.fr/produits/pompe-submersible-miniature-12-v-cc-3-metres-de-haut-resistante-a-des-temperatures-jusqu-a-60-98813622.html?megaBoost&at_source=google" target="_blank">Voir</a> ou <a href="https://funduinoshop.com/fr/modules-electroniques/vannes-et-pompes/pompes/r385-pompe-a-eau-6-12v" target="_blank">Voir</a>|
| **Tuyau 8mm** | Alimentation eau. | At. 4 | 6,00 € | <a href="https://www.lextronic.fr/tuyau-accessoires-de-montage-5410329680831-31657.html" target="_blank">Voir</a>|
| :material-check-decagram-outline: **Ventilateur (12V)** | Régulation thermique. | At. 4 | 5,00 € | <a href="https://fr.rs-online.com/web/p/ventilateurs-axiaux/1442036" target="_blank">Voir</a> |
| **ULN2803** | Commutation Pompe / Ventilateur. | At. 3 | en stock | <a href="" target="_blank">Voir</a> |
| :material-check-decagram-outline: **Écran LCD I2C** | Affichage des données supervisées. | At. 1 | 5,50 € | <a href="https://fr.rs-online.com/web/p/afficheurs-monochromes-lcd/0735064?gb=a" target="_blank">Voir</a> |
| :material-check-decagram-outline: **Capteur LDR** | Mesure de l'ensoleillement. Il faut un diviseur de tension. | At. 3 | 1,00 € | <a href="https://fr.rs-online.com/web/p/photoresistances/0596141" target="_blank">Voir</a> |
| **Structure** Plaastique ou plexi| Bac et couvercle. | Tous | 12,00 € | <a href="https://www.ferplast.fr/products/geo-medium" target="_blank">Voir</a> ou <a href="https://www.ikea.com/fr/fr/p/doftrips-set-jardinage-transparent-blanc-casse-60612337" target="_blank">Voir</a> ou <a href="https://www.leclercbrico.fr/aquariums/61077-geo-small-bac-couvercle-coloris-ferplast.html" target="_blank">Voir</a> |
| **TOTAL ESTIMÉ** | | | **~68,00 €** | |

!!! info "A prévoir également :"

	* Gaine thermo (en stock), 
	* Colliers de serrage, 
	* Gaine spirale,
	* Fiche JST ou bornier à vis (pour pouvoir séparer facilement le bac de l'alim/contrôle,
	* Nappe Ribon pour LCD ?
	* Etiqueteuse pour identifier chaque lot de fils, car le nombre de capteurs pourra être important.
	* Horloge temps réel
	* Breadboard à remplacer

> :warning:
> **Attention à l'humidité**

> * **Protection :** Évitez toute projection d'eau sur la platine d'alimentation.
> * **Boucle de goutte :** Faites en sorte que les fils remontent légèrement avant d'entrer dans le boîtier électronique (pour éviter que l'eau ne s'écoule par capillarité vers l'électronique).

---

## ⚙️ Exploitation de la platine d'alimentation existante
Ce projet est conçu pour réutiliser la platine d'alimentation :

* **Sortie 12V :** Dédiée à la puissance (Pompe et Ventilation).
* **Sortie 5V :** Dédiée à la logique (Arduino, Capteurs, Écran) et à la bande LED.
* **Sortie 3.3V :** Disponible pour une future extension IoT.

Utiliser les ULN pour les moteurs. Utiliser servomoteur pour ouverture panneau aération.

---

## Particularités du prototype

1. **Tension d'alimentation :** Utilisation du **12V** pour la puissance (pompe/ventilation) et du **5V** pour la commande et la bande LED.
2. **Modularité :** Possibilité d'ajouter un module **ESP32-CAM** pour surveiller la croissance des plantes à distance (mais très peu probable pdt les 2 semaines...).
3. **Sympa :** L'ajout de la **bande LED RGB** permet d'aborder la synthèse additive des couleurs et l'influence des longueurs d'onde (Bleu/Rouge) sur la photosynthèse.

## Détails sur le matériel

* Ventilateurs 12V pc (pris sur un processeur) : 

	* Noir : GND (La masse / le -).
	* Jaune : +12V (L'alimentation).
	* Vert : Tachymètre (mesure vitesse de rotation en RPM). Rajouter une rés. de pull-up en entrée.
	* Bleu : PWM (Le fil de contrôle). C'est lui qui permet de régler la vitesse sans couper l'alimentation.


## 🚀 Simulation du prototype

<div style="border: 1px solid #dee2e6; border-radius: 8px; padding: 10px; background: #f8f9fa; margin: 20px 0; text-align: center;">
    <iframe width="725" height="453" src="https://www.tinkercad.com/embed/jU2lx74vJWN?editbtn=1" frameborder="0" marginwidth="0" marginheight="0" scrolling="no"></iframe>
    <p><em>Mise en œuvre du prototype (les moteur CC simulent la pompe et le ventilo...). La commande est en tout ou rien, et la décision est faite de manière soft : l'objectif des ateliers est de proposer des outils pour améliorer cela (asservissement et logique de décision câblée). </em></p>
</div>