
État du projet — 20/05/2025

Le projet est désormais pratiquement terminé.

Cependant, lors de la rédaction de la documentation, j’en ai profité pour vérifier les différentes animations. Bien qu’elles soient fonctionnelles, je considère qu’elles pourraient être largement améliorées.

✅ Points d’amélioration identifiés :
Simplification du code : certaines animations peuvent être réécrites de manière plus concise et plus lisible.

Regroupement des éléments via ::before et ::after : cela permettrait de mieux structurer les composants, de faciliter leur réutilisation et de garantir une meilleure validation W3C (HTML/CSS).

Utilisation de opacity au lieu de transform pour certains effets, notamment pour les changements de couleur de fond. Cela permettrait de ne modifier le DOM qu'à l'étape 1, évitant des recalculs inutiles aux étapes 2 et 3.

Ces ajustements visent à améliorer les performances générales du site et à rendre le code plus maintenable à long terme.

------
- Réflexion sur l'optimisation du mixin btn
Dans une logique d'amélioration des performances, j'ai identifié que la gestion actuelle du box-shadow dans le mixin btn n'était pas optimale. En effet, appliquer directement un box-shadow dans le pseudo-état :hover peut entraîner des recalculs de styles coûteux, en particulier sur des interfaces riches en interactions ou sur des appareils moins performants.

- Proposition d'amélioration :
Remplacer la modification dynamique de box-shadow par une gestion via ::after, en superposant deux états visuels du bouton.

Utiliser uniquement la propriété opacity (GPU-accelerated) pour faire apparaître la version avec ombre au survol.

Avantage : évite le recalcul du DOM ou des styles, améliore les performances, et permet une transition plus fluide.

✅ Bénéfices attendus :
Meilleure fluidité des animations
Optimisation du rendu sur les navigateurs

----
- Réflexion sur l'optimisation de l'icone (heart)
La gestion actuelle des effets d’icônes dans les mixins icon-toggle-* repose sur plusieurs propriétés CSS complexes (clip, text-fill, Font Awesome, content, etc.). 
Bien que fonctionnelle, cette approche est lourde, difficile à maintenir, et peu optimale pour des transitions visuelles simples.

🔍 Problème identifié :
Le rendu visuel d’un “remplissage” d’icône au clic est simulé via des techniques avancées (clip-path, text-fill, gestion fine des caractères Unicode).

Cela complexifie inutilement le code, ralentit l’interprétation du DOM, et rend les animations moins fluides.

✅ Proposition d’amélioration :
Utiliser uniquement des pseudo-éléments ::before et ::after :

::before pour afficher l’icône vide (état par défaut)

::after pour superposer une version pleine de l’icône avec un transform: scale(0)

Au clic, passer scale(1) à ::after avec une transition douce, créant un effet de remplissage depuis le centre

Cette méthode permet une animation fluide et épurée, sans surcharge du DOM ou recours à des hacks CSS

----
Optimisation du composant .menu__clikablebox
Le composant interactif du menu fonctionne actuellement, mais présente plusieurs points perfectibles .

🔍 Problèmes identifiés :
La réduction de la largeur de .menu__clikablebox--transformable est gérée via width, ce qui provoque des recalculs de mise en page .

L’élément .menu__clikablebox--beyond reste partiellement visible même lorsqu’il est censé être caché, malgré une tentative de camouflage via un border blanc côté 
(solution de contournement).

La nomenclature "beyond" est inadaptée : elle évoque une notion d’extérieur ou d’entourage alors qu’il s’agit en réalité d’un élément en arrière-plan ou masqué.

✅ Propositions d'amélioration :
Utiliser transform: scaleX() à la place de width :

Ajout d’un transform-origin: left; pour faire rétrécir l’élément depuis la gauche, sans altérer son alignement.

Permet une transition plus fluide, mieux optimisée .

Cacher réellement l’élément .beyond :

Remplacer le camouflage par un display: none .

Cela supprime tout résidu visuel (coins visibles) et améliore les performances.

Renommer .menu__clikablebox--beyond → .menu__clikablebox--hidden :

Nommage plus clair et logique : l’élément est derrière et masqué par défaut.

Facilite la lecture et la maintenance du code.

État du projet — 22/05/2025
Finaliser les animations, le slide du menu, l’icône du cœur et les ombres via la mixin du bouton.

Refonte de la structure HTML des cartes des restaurants.

Validation HTML et CSS via le W3C.

La base du projet est terminée.
