installer mkdocs (pip install mkdocs mkdocs-material)
Félicitations ! Votre site est officiellement en ligne à l'adresse https://pjlapray.github.io/Site_web/.

git add .
git commit -m "1"
git push

L'Action GitHub s'occupera du reste et votre site sera à jour 30 secondes plus tard.

Titre de niveau 1	# Titre	\section{Titre}
Titre de niveau 2	## Titre	\subsection{Titre}
Titre de niveau 3	### Titre	\subsubsection{Titre}
Gras	**Texte**	\textbf{Texte}
Italique	*Texte*	\textit{Texte}
Liste à puces	- Élément

-----------------------------------------------------------------

En local (ens) :
python -m mkdocs serve --livereload

En local (rech) :
Lancer ruby 4.0 command
cd "C:\Users\Lapray\Google Drive\MCF\Enseignement\Site_web\rech"
bundle exec jekyll serve --livereload
http://localhost:4000/rech/