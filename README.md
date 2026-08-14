# KnowledgePulse

> Maquette d'une plateforme d'apprentissage en ligne, intégrée en HTML et Tailwind CSS, sans framework ni JavaScript.

Site vitrine de cinq pages entièrement responsives. Tous les composants interactifs — menu mobile, accordéons, carrousel de témoignages, sous-menu déroulant — sont réalisés **sans une ligne de JavaScript**, en s'appuyant sur des éléments HTML natifs et les variants d'état de Tailwind.

## Sommaire

- [Aperçu](#aperçu)
- [Fonctionnalités](#fonctionnalités)
- [Technologies](#technologies)
- [Prise en main](#prise-en-main)
- [Structure du projet](#structure-du-projet)
- [Charte graphique](#charte-graphique)
- [Limitations connues](#limitations-connues)
- [Pistes d'amélioration](#pistes-damélioration)
- [Crédits](#crédits)

## Aperçu

| Page | Fichier | Contenu |
| --- | --- | --- |
| Accueil | `pages/index.html` | Hero, partenaires, catalogue de cours, fonctionnement, mentors, témoignages |
| Formateurs | `pages/mentor.html` | Bannière « Our Vision », fonctionnement, mentors, témoignages |
| Cours | `pages/enroll.html` | Fiche de cours, programme, carte d'inscription, derniers cours |
| FAQ | `pages/faq.html` | Accordéon de questions fréquentes |
| Article | `pages/about.html` | Article de blog, image de couverture, articles liés |

Toutes les pages partagent la même barre de navigation, le même bloc newsletter et le même pied de page.

## Fonctionnalités

- **Responsive mobile-first** — trois paliers : mobile (par défaut), tablette (`md`, 768 px), desktop (`lg`, 1024 px).
- **Menu mobile** avec bouton burger qui bascule en croix.
- **Sous-menu déroulant** « Pages » au survol, en desktop.
- **Accordéons exclusifs** pour la FAQ et le programme de cours : un seul panneau ouvert à la fois.
- **Carrousel de témoignages** avec sélection par avatar.
- **Carrousels de cartes** à défilement horizontal avec calage automatique (scroll snap).
- **État de navigation actif** signalé visuellement et via `aria-current="page"`.
- **Accessibilité** : libellés `sr-only` sur tous les champs, `aria-label` sur les liens iconographiques, `aria-hidden` sur les éléments décoratifs, navigation complète au clavier.

## Technologies

| Outil | Version | Rôle |
| --- | --- | --- |
| HTML5 | — | Structure sémantique |
| [Tailwind CSS](https://tailwindcss.com) | 4.x (CDN navigateur) | Totalité de la mise en forme |
| SVG inline | — | Icônes et formes décoratives |

Aucune dépendance à installer, aucun build, aucune bibliothèque JavaScript.

## Prise en main

### Prérequis

Un navigateur récent (voir [Compatibilité navigateurs](#compatibilité-navigateurs)) et une connexion internet au premier chargement, le temps que le CDN Tailwind soit mis en cache.

### Installation

```bash
git clone https://github.com/Eunock-web/KnowledgePulse.git
cd KnowledgePulse
```

### Lancement

Le projet étant entièrement statique, il suffit d'ouvrir `pages/index.html` dans un navigateur.

Pour un rechargement automatique pendant le développement :

- **VS Code** — extension *Live Server*, puis clic droit sur `pages/index.html` → *Open with Live Server* ;
- **Python** — depuis la racine du projet :

  ```bash
  python3 -m http.server 5500
  ```

  puis ouvrir <http://localhost:5500/pages/index.html>.

## Structure du projet

```
Elearning/
├── images/              # Visuels (photos de cours, portraits, avatars)
├── pages/               # Les cinq pages du site
│   ├── index.html       # Accueil
│   ├── mentor.html      # Formateurs
│   ├── enroll.html      # Fiche de cours
│   ├── faq.html         # Questions fréquentes
│   └── about.html       # Article de blog
├── css/                 # Réservé à une future feuille de styles
├── js/                  # Réservé à de futurs scripts
├── src/                 # Réservé à une compilation locale de Tailwind
└── README.md
```


## Charte graphique

### Couleurs

| Usage | Valeur | Aperçu |
| --- | --- | --- |
| Fond des sections claires | `#E8F7F3` | Vert d'eau très pâle |
| Fond des blocs sombres | `#083C3B` | Vert sapin |
| Texte et liens principaux | `#0F7362` | Vert profond |
| Boutons et accents | `#12786A` | Vert émeraude |
| Texte secondaire sur fond sombre | `#b5cac8` | Gris-vert clair |
| Accent décoratif | `#D9F55C` | Jaune citron |
| Formes décoratives | `#A6CCC2`, `#C6E3B8` | Verts pâles |


### Documentation des classes

Chacune des 397 classes Tailwind employées dans le projet est décrite — CSS produit et raison de son emploi — dans **[TAILWIND.md](TAILWIND.md)**.

### Conventions

- Interface et contenu en **anglais**, commentaires du code en **français**.
- Un seul `<h1>` par page ; les titres de sections sont des `<h2>`.
- Les couleurs de la charte sont écrites en valeurs arbitraires (`bg-[#083C3B]`), la palette Tailwind par défaut n'étant utilisée que pour les gris.



Défilement tactile natif avec calage sur le début de chaque carte. En desktop, la largeur calculée fait tenir les quatre cartes sans débordement : le carrousel devient une grille statique, sans changer de mécanique.

## Compatibilité navigateurs

| Fonctionnalité | Chrome / Edge | Firefox | Safari |
| --- | --- | --- | --- |
| Mise en page, scroll snap | ✅ | ✅ | ✅ |
| `:has()` (menu mobile, témoignages) | 105+ | 121+ | 15.4+ |
| Accordéon exclusif (`<details name>`) | 120+ | 130+ | 17.2+ |

Sur un navigateur antérieur, l'accordéon reste fonctionnel mais perd son exclusivité : plusieurs panneaux peuvent être ouverts simultanément. La dégradation est visuelle, jamais bloquante.

## Limitations connues

- **CDN Tailwind** — la compilation s'effectue dans le navigateur. Pratique en développement, à remplacer par une version compilée avant toute mise en production.
- **Duplication du balisage** — la barre de navigation et le pied de page sont recopiés dans les cinq pages. Toute modification doit être reportée partout.
- **Onglets du catalogue** — les catégories de cours de la page d'accueil sont décoratives et ne filtrent pas les résultats.
- **Flèches des carrousels** — ce sont des ancres qui sautent à la première ou à la dernière carte, pas un défilement pas à pas.
- **Contenus de démonstration** — textes, notes, nombres d'avis et logos partenaires sont fictifs. Les logos sont des reproductions typographiques, à remplacer par les fichiers officiels.
- **Formulaires** — la recherche et l'inscription à la newsletter ne sont reliées à aucun traitement.

## Pistes d'amélioration

- [ ] Compiler Tailwind localement et supprimer le CDN
- [ ] Factoriser navigation et pied de page (includes, Vite ou Eleventy)
- [ ] Rendre les onglets du catalogue fonctionnels
- [ ] Détourer la photo du hero en PNG transparent
- [ ] Remplacer les logos partenaires par les SVG officiels
- [ ] Ajouter les métadonnées Open Graph et un favicon

## Crédits

Maquette originale de **Rubel**. Intégration réalisée dans le cadre d'un projet de stage.

Images issues du dossier `images/`, utilisées à des fins de démonstration.
