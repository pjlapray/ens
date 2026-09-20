# 🧩 Les Tableaux de Karnaugh : De la Vérité au Schéma Simplifié

Bienvenue dans ce guide ! L'objectif d'un **Tableau de Karnaugh** (ou *K-Map*) est de **simplifier au maximum une équation logique** sans faire de longs calculs d'algèbre de Boole.

---

## 💡 Le Principe de Base : Le Code de Gray

Le secret du tableau de Karnaugh réside dans l'agencement des cases. On utilise le **Code de Gray** (un seul bit change d'une case à sa voisine).

!!! tip "Règle d'or de l'adjacence"
    Deux cases adjacentes (horizontalement ou verticalement) ne diffèrent que par **un seul état logique**. Cela permet d'appliquer la règle booléenne :
    $A \cdot B + A \cdot \bar{B} = A(B + \bar{B}) = A \cdot 1 = A$

---

## 📏 Les 4 Règles d'Or du Regroupement

Pour extraire une équation minimale depuis un tableau de Karnaugh, respectez toujours ces 4 consignes :

1. **Taille des groupes :** Toujours une puissance de 2 ($1, 2, 4, 8, 16$ cases).
2. **Forme des groupes :** Rectangles ou carrés uniquement (jamais de diagonales ou de L).
3. **Taille maximale :** Créez les groupes **les plus grands possibles** (moins il y a de groupes, plus l'équation est simple).
4. **Effet Torique :** Les bords du tableau se touchent ! La colonne de gauche est voisine de celle de droite, tout comme la ligne du haut touche celle du bas.

---

## 🎛️ Simulateur Interactif 4x4

Sélectionnez les cases à **1** en cliquant dessus. L'équation simplifiée ainsi que les regroupements optimaux sont calculés dynamiquement en temps réel.

<div style="background-color: var(--md-code-bg-color, #f8f9fa); padding: 1.5rem; border-radius: 8px; border: 1px solid #ccc; margin: 1em 0; color: #222;">
  <h3 class="arithmatex" style="margin-top: 0; text-align: center;">Tableau de Karnaugh à 4 Variables : $S(A, B, C, D)$</h3>
  
  <div style="overflow-x: auto;">
    <table id="kmap-table" style="margin: 15px auto; text-align: center; border-collapse: collapse; background: transparent;">
      <thead>
        <tr>
          <th class="arithmatex" style="border: none; padding: 8px;">AB \ CD</th>
          <th class="arithmatex" style="padding: 8px 12px; border-bottom: 2px solid #333;"><b>00</b> (\(\bar{C}\bar{D}\))</th>
          <th class="arithmatex" style="padding: 8px 12px; border-bottom: 2px solid #333;"><b>01</b> (\(\bar{C}D\))</th>
          <th class="arithmatex" style="padding: 8px 12px; border-bottom: 2px solid #333;"><b>11</b> (\(CD\))</th>
          <th class="arithmatex" style="padding: 8px 12px; border-bottom: 2px solid #333;"><b>10</b> (\(C\bar{D}\))</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="arithmatex" style="padding: 8px 12px; border-right: 2px solid #333; font-weight: bold;"><b>00</b> (\(\bar{A}\bar{B}\))</td>
          <td><button class="kmap-btn" data-r="0" data-c="0" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="0" data-c="1" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="0" data-c="2" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="0" data-c="3" onclick="toggleCell4x4(this)">0</button></td>
        </tr>
        <tr>
          <td class="arithmatex"style="padding: 8px 12px; border-right: 2px solid #333; font-weight: bold;"><b>01</b> (\(\bar{A}B\))</td>
          <td><button class="kmap-btn" data-r="1" data-c="0" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="1" data-c="1" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="1" data-c="2" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="1" data-c="3" onclick="toggleCell4x4(this)">0</button></td>
        </tr>
        <tr>
          <td class="arithmatex"style="padding: 8px 12px; border-right: 2px solid #333; font-weight: bold;"><b>11</b> (\(AB\))</td>
          <td><button class="kmap-btn" data-r="2" data-c="0" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="2" data-c="1" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="2" data-c="2" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="2" data-c="3" onclick="toggleCell4x4(this)">0</button></td>
        </tr>
        <tr>
          <td class="arithmatex"style="padding: 8px 12px; border-right: 2px solid #333; font-weight: bold;"><b>10</b> (\(A\bar{B}\))</td>
          <td><button class="kmap-btn" data-r="3" data-c="0" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="3" data-c="1" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="3" data-c="2" onclick="toggleCell4x4(this)">0</button></td>
          <td><button class="kmap-btn" data-r="3" data-c="3" onclick="toggleCell4x4(this)">0</button></td>
        </tr>
      </tbody>
    </table>
  </div>

  <div style="text-align: center; margin: 15px 0;">
    <button onclick="resetKmap4x4()" style="padding: 6px 14px; background-color: #f44336; color: white; border: none; border-radius: 4px; cursor: pointer; font-weight: bold;">Réinitialiser (Tout à 0)</button>
    <button onclick="presetXnorExample()" style="padding: 6px 14px; background-color: #2196F3; color: white; border: none; border-radius: 4px; cursor: pointer; font-weight: bold; margin-left: 8px;">Exemple d'exercice</button>
  </div>

  <div style="background: #ffffff; padding: 12px; border-radius: 6px; border: 1px solid #ddd; margin-top: 15px; color: #111;">
    <div class="arithmatex" style="font-size: 1.1rem; font-weight: bold; margin-bottom: 6px;">Équation simplifiée :</div>
    <div class="arithmatex" id="equation-output" style="font-size: 1.3rem; font-family: monospace; color: #d32f2f; min-height: 30px;">S = 0</div>
    <div class="arithmatex" id="groups-details" style="margin-top: 10px; font-size: 0.95rem; color: #555;"></div>
  </div>
</div>

<style>
.kmap-btn {
  font-size: 1.1rem;
  font-weight: bold;
  width: 50px;
  height: 45px;
  cursor: pointer;
  border-radius: 6px;
  border: 1px solid #bbb;
  background-color: #ffffff;
  color: #333;
  transition: all 0.2s ease;
}
.kmap-btn.active {
  background-color: #4CAF50;
  color: white;
  border-color: #388E3C;
  box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
}
</style>

<script>
const rowMap = [
  { A: 0, B: 0 },
  { A: 0, B: 1 },
  { A: 1, B: 1 },
  { A: 1, B: 0 }
];

const colMap = [
  { C: 0, D: 0 },
  { C: 0, D: 1 },
  { C: 1, D: 1 },
  { C: 1, D: 0 }
];

function toggleCell4x4(btn) {
  if (btn.innerText === "0") {
    btn.innerText = "1";
    btn.classList.add("active");
  } else {
    btn.innerText = "0";
    btn.classList.remove("active");
  }
  solveKmap4x4();
}

function resetKmap4x4() {
  document.querySelectorAll('.kmap-btn').forEach(btn => {
    btn.innerText = "0";
    btn.classList.remove("active");
  });
  solveKmap4x4();
}

function presetXnorExample() {
  resetKmap4x4();
  const activeCoords = [[0,0], [0,3], [1,1], [1,2], [2,1], [2,2], [3,0], [3,3]];
  activeCoords.forEach(([r, c]) => {
    const btn = document.querySelector(`.kmap-btn[data-r="${r}"][data-c="${c}"]`);
    if(btn) {
      btn.innerText = "1";
      btn.classList.add("active");
    }
  });
  solveKmap4x4();
}

function solveKmap4x4() {
  const grid = Array(4).fill(0).map(() => Array(4).fill(0));
  let onesCount = 0;

  document.querySelectorAll('.kmap-btn').forEach(btn => {
    const r = parseInt(btn.getAttribute('data-r'));
    const c = parseInt(btn.getAttribute('data-c'));
    const val = parseInt(btn.innerText);
    grid[r][c] = val;
    if (val === 1) onesCount++;
  });

  const eqOutput = document.getElementById('equation-output');
  const detailsDiv = document.getElementById('groups-details');

  if (onesCount === 0) {
    eqOutput.innerHTML = "S = 0";
    detailsDiv.innerHTML = "<em>Aucun regroupement (toutes les cases sont à 0).</em>";
    return;
  }

  if (onesCount === 16) {
    eqOutput.innerHTML = "S = 1";
    detailsDiv.innerHTML = "<em>Un seul groupe de 16 cases couvre l'ensemble du tableau.</em>";
    return;
  }

  const validRects = [];
  const heights = [1, 2, 4];
  const widths = [1, 2, 4];

  for (let h of heights) {
    for (let w of widths) {
      for (let r = 0; r < 4; r++) {
        for (let c = 0; c < 4; c++) {
          if (allOnes(grid, r, c, h, w)) {
            validRects.push({ r, c, h, w, size: h * w });
          }
        }
      }
    }
  }

  validRects.sort((a, b) => b.size - a.size);

  let uncovered = new Set();
  for (let r = 0; r < 4; r++) {
    for (let c = 0; c < 4; c++) {
      if (grid[r][c] === 1) uncovered.add(`${r},${c}`);
    }
  }

  const selectedGroups = [];

  for (let rect of validRects) {
    let coversNew = false;
    for (let dr = 0; dr < rect.h; dr++) {
      for (let dc = 0; dc < rect.w; dc++) {
        const nr = (rect.r + dr) % 4;
        const nc = (rect.c + dc) % 4;
        if (uncovered.has(`${nr},${nc}`)) {
          coversNew = true;
        }
      }
    }

    if (coversNew) {
      selectedGroups.push(rect);
      for (let dr = 0; dr < rect.h; dr++) {
        for (let dc = 0; dc < rect.w; dc++) {
          const nr = (rect.r + dr) % 4;
          const nc = (rect.c + dc) % 4;
          uncovered.delete(`${nr},${nc}`);
        }
      }
    }
  }

  const terms = [];
  const groupDescriptions = [];

  selectedGroups.forEach((g, index) => {
    const term = getTermForGroup(g);
    terms.push(term);
    // On entoure le terme de \(et\) pour le rendu LaTeX
    groupDescriptions.push(`• <b>Groupe ${index + 1}</b> (${g.size} cases) : \\(${term}\\)`);
  });

  // Injection dans le DOM avec délimiteurs LaTeX \(...\)
  if (terms.length > 0) {
    eqOutput.innerHTML = "S = \\(" + terms.join(" + ") + "\\)";
  } else {
    eqOutput.innerHTML = "S = 0";
  }

  detailsDiv.innerHTML = "<b>Regroupements détectés :</b><br>" + groupDescriptions.join("<br>");

  // OBLIGATOIRE : Déclenche le rendu MathJax sur les éléments dynamiques
  if (window.MathJax && MathJax.typesetPromise) {
    MathJax.typesetPromise([eqOutput, detailsDiv]);
  }
}

function allOnes(grid, r, c, h, w) {
  for (let dr = 0; dr < h; dr++) {
    for (let dc = 0; dc < w; dc++) {
      const nr = (r + dr) % 4;
      const nc = (c + dc) % 4;
      if (grid[nr][nc] !== 1) return false;
    }
  }
  return true;
}

function getTermForGroup(g) {
  let aVal = null, bVal = null, cVal = null, dVal = null;
  let aSame = true, bSame = true, cSame = true, dSame = true;

  for (let dr = 0; dr < g.h; dr++) {
    for (let dc = 0; dc < g.w; dc++) {
      const r = (g.r + dr) % 4;
      const c = (g.c + dc) % 4;

      const rInfo = rowMap[r];
      const cInfo = colMap[c];

      if (aVal === null) aVal = rInfo.A; else if (aVal !== rInfo.A) aSame = false;
      if (bVal === null) bVal = rInfo.B; else if (bVal !== rInfo.B) bSame = false;
      if (cVal === null) cVal = cInfo.C; else if (cVal !== cInfo.C) cSame = false;
      if (dVal === null) dVal = cInfo.D; else if (dVal !== cInfo.D) dSame = false;
    }
  }

  let term = "";
	if (aSame) term += aVal === 1 ? "A" : "\\bar{A}";
	if (bSame) term += bVal === 1 ? "B" : "\\bar{B}";
	if (cSame) term += cVal === 1 ? "C" : "\\bar{C}";
	if (dSame) term += dVal === 1 ? "D" : "\\bar{D}";

  return term === "" ? "1" : term;
}

document.addEventListener("DOMContentLoaded", () => {
  solveKmap4x4();
});
</script>

---

## 📊 Exemple Pratique Détaillé (4 Variables : A, B, C, D)

Voici un tableau à 4 variables pré-rempli :

| AB \ CD | 00 ($\bar{C}\bar{D}$) | 01 ($\bar{C}D$) | 11 ($CD$) | 10 ($C\bar{D}$) |
| :---: | :---: | :---: | :---: | :---: |
| **00** ($\bar{A}\bar{B}$) | <span style="background:#ffcdd2; color:#000; padding:4px 8px; border-radius:4px; font-weight:bold;">1</span> | 0 | 0 | <span style="background:#ffcdd2; color:#000; padding:4px 8px; border-radius:4px; font-weight:bold;">1</span> |
| **01** ($\bar{A}B$) | 0 | <span style="background:#c8e6c9; color:#000; padding:4px 8px; border-radius:4px; font-weight:bold;">1</span> | <span style="background:#c8e6c9; color:#000; padding:4px 8px; border-radius:4px; font-weight:bold;">1</span> | 0 |
| **11** ($AB$) | 0 | <span style="background:#c8e6c9; color:#000; padding:4px 8px; border-radius:4px; font-weight:bold;">1</span> | <span style="background:#c8e6c9; color:#000; padding:4px 8px; border-radius:4px; font-weight:bold;">1</span> | 0 |
| **10** ($A\bar{B}$) | <span style="background:#ffcdd2; color:#000; padding:4px 8px; border-radius:4px; font-weight:bold;">1</span> | 0 | 0 | <span style="background:#ffcdd2; color:#000; padding:4px 8px; border-radius:4px; font-weight:bold;">1</span> |

??? note "🔍 Décomposition étape par étape des regroupements"

    ### 🟢 Groupe Vert (4 cases au centre)
    - **Cases couvertes** : (01,01), (01,11), (11,01), (11,11)
    - **Variable A** : change ($0 \to 1$) $\Rightarrow$ **Éliminée**
    - **Variable B** : vaut toujours $1$ $\Rightarrow$ **$B$**
    - **Variable C** : change ($0 \to 1$) $\Rightarrow$ **Éliminée**
    - **Variable D** : vaut toujours $1$ $\Rightarrow$ **$D$**
    - **Terme extrait :** **$B \cdot D$**

    ---

    ### 🔴 Groupe Rouge (4 coins du tableau - effet torique !)
    - **Cases couvertes** : (00,00), (00,10), (10,00), (10,10)
    - **Variable A** : change ($0 \to 1$) $\Rightarrow$ **Éliminée**
    - **Variable B** : vaut toujours $0$ $\Rightarrow$ **$\bar{B}$**
    - **Variable C** : change ($0 \to 1$) $\Rightarrow$ **Éliminée**
    - **Variable D** : vaut toujours $0$ $\Rightarrow$ **$\bar{D}$**
    - **Terme extrait :** **$\bar{B} \cdot \bar{D}$**

    ---

    ### 🎯 Équation Finale Simplifiée :
    $S = B \cdot D + \bar{B} \cdot \bar{D}$
		*(Remarque : cette équation correspond à une porte logique **XNOR** entre $B$ et $D$ !)*