# Bienvenue

Ceci est le site web pédagogique de **Pierre-Jean Lapray**, enseignant-chercheur à l'**ENSISA**.

Vous trouverez ici des exemples et des bonnes pratiques pour mes modules d'enseignement de la spécialité Automatique et Systèmes Embarqués.
Ceci vient en complément du Moodle.

---

### 📚 Modules d'enseignement

<div class="grid cards" markdown>

-   :material-gate-nor: **Électronique Numérique**
    ---
    Bases de la logique combinatoire et séquentielle (1ère année - S5).
    [:octicons-arrow-right-24: Accéder aux ressources](en/generalites.md)

-   :material-chip: **Systèmes Embarqués Reconfigurables I**
    ---
    Introduction au langage VHDL et à la conception sur FPGA (2ème année - S7).
    [:octicons-arrow-right-24: Accéder aux ressources](ser1/fpga.md)

-   :material-cpu-32-bit: **Systèmes Embarqués Reconfigurables II**
    ---
    Conception avancée : IP, SoC et bus (2ème année - S8).
    [:octicons-arrow-right-24: Accéder aux ressources](ser2/soc_fpga.md)

-   :material-wall: **Immersion**
    ---
    Découverte éléctronique, automatique et micro-informatique (1ère année - S5).
    [:octicons-arrow-right-24: Accéder aux ressources](immersion/index.md)

</div>

---

!!! info "Objectifs pédagogiques"
    Ce portail centralise les exemples et les guides méthodologiques pour accompagner les étudiants pendant les TD et TP.
	
---

### 🔍 Démo interactive : Traitement d'images (Avant / Après)

Glissez le curseur pour remplacer dynamiquement l'image originale par le résultat du traitement, sans déformation.

<div class="viewer-container" style="position: relative; width: 100%; max-width: 600px; aspect-ratio: 4/3; overflow: hidden; user-select: none; border-radius: 8px; box-shadow: 0 4px 10px rgba(0,0,0,0.15); margin: 20px auto;">
  
  <img src="https://picsum.photos/id/1015/600/400" style="position: absolute; top:0; left:0; width:100%; height:100%; object-fit: cover;" draggable="false">
  
  <div class="viewer-split-pane" style="position: absolute; top:0; left:0; width: 50%; height:100%; overflow:hidden; border-right: 3px solid #ffffff;">
    <img src="https://picsum.photos/id/1016/600/400" class="viewer-src-img" style="position: absolute; top:0; left:0; height:100%; object-fit: cover; max-width: none;" draggable="false">
  </div>
  
  <div class="viewer-handle" style="position: absolute; top:0; left: 50%; width: 40px; height:100%; cursor: ew-resize; transform: translateX(-50%); display: flex; align-items: center; justify-content: center;">
    <div style="width: 32px; height: 32px; background: #ffffff; border-radius: 50%; display: flex; align-items: center; justify-content: center; box-shadow: 0 2px 6px rgba(0,0,0,0.4); font-weight: bold; color: #333;">↔</div>
  </div>
</div>

<script>
  document.addEventListener("DOMContentLoaded", function() {
    const container = document.querySelector('.viewer-container');
    const splitPane = container.querySelector('.viewer-split-pane');
    const handle = container.querySelector('.viewer-handle');
    const srcImg = container.querySelector('.viewer-src-img');
    
    // Aligne la taille de l'image masquée sur celle du conteneur global dès le départ
    function resizeImage() {
      srcImg.style.width = container.offsetWidth + 'px';
    }
    
    function moveSlider(x) {
      const rect = container.getBoundingClientRect();
      let position = (x - rect.left) / rect.width;
      if (position < 0) position = 0;
      if (position > 1) position = 1;
      
      splitPane.style.width = (position * 100) + '%';
      handle.style.left = (position * 100) + '%';
    }
    
    // Gestion du responsive si la fenêtre change de taille
    window.addEventListener('resize', resizeImage);
    resizeImage();
    
    // Événements Souris
    container.addEventListener('mousemove', (e) => {
      if (e.buttons === 1) moveSlider(e.clientX);
    });
    container.addEventListener('mousedown', (e) => moveSlider(e.clientX));
    
    // Événements Tactiles
    container.addEventListener('touchmove', (e) => {
      moveSlider(e.touches[0].clientX);
    });
    container.addEventListener('touchstart', (e) => moveSlider(e.touches[0].clientX));
  });
</script>