# Cours Sass
## Initialiser un projet
SASS = Syntacticaly Awesome Style Sheets.
C'est un pré-processor : comme un logiciel qui va exécuter du code SCSS pour en ressortir du CSS, créé en Ruby.

SCSS : Façon d'écrire du Sass.

- 1ère méthode (SASS) : pas d'accolade ou de point virgule
- 2e méthode (SCSS) : Utilise les points virgule et accolades. S'écrit comme du CSS.

### Avantages des méthodes
 - Avantage de SASS :
    - Une syntaxe concise
    - Facile à lire
    - Plus de problème de points virgules
 - Avantage de SCSS :
    - Syntaxe plus précise
    - Encourage à écrire proprement
    - L'lintégration est largement plus facile avec du CSS
    - Nous connaissons déjà CSS
    - SCSS sera peut-être CSS4

### Installer Sass
2 méthodes :

1. Avec la console (recommandé + rapide, celle utilisée)
- rubyinstaller.org -> Télécharger ruby, la dernière version.
````console
$ gem install sass
````

2. En téléchargeant un logiciel
- https://scout-app.io/ -> Télécharger Sass
- Extraire sur le PC
- Lancer Scout-App.exe

### Histoire de Ruby
But : écrire un langage qui soit le plus simple et le plus court possible.

Yukihiri "Matz" Matsumoto a voulu créer un langage le plus intéressant et le plus propre pour les programmeurs.

````
"Ruby est simple en apparence, mais son architecture interne est très complexe - tout comme notre coprs peut l'être" - Yukihiri "Matz" Matsumoto
````

## Notions de base
### Architecture
Dans le projet créer :
- design/
    - css/
    - sass/
- img/
- index.html

Toutes les feuilles Sass vont être transformées en CSS.

### Générer la première feuille de style CSS
- design\css\default.css -> html
- Ecrire dans le fichier .scss
- Dans la console
````console
$ sass C:\wamp64\www\Sass_udemy\design\sass\default.scss C:\wamp64\www\Sass_udemy\design\css\default.css
````
- Création d'un fichier default.css à partir du default.scss
- Pour changer en continue les fichiers scss en css, dans la console :
````console
$ sass --watch C:\wamp64\www\Sass_udemy\design\sass\default.scss:C:\wamp64\www\Sass_udemy\design\css\default.css
````
OU (pour tout un dossier)
````console
$ sass --watch C:\wamp64\www\Sass_udemy\design\sass:C:\wamp64\www\Sass_udemy\design\css
````

### Les variables
````scss
// Déclaration d'une variable utilisable
$primaryColor: purple;

body {
    background-color: gray;
}

header{
    padding: 50px;
    background-color: $primaryColor;
    margin-bottom: 50px;
}

footer{
    padding: 50px;
    background-color: $primaryColor;
}
````
retranscrit en :
````css
body {
  background-color: gray; }

header {
  padding: 50px;
  background-color: purple;
  margin-bottom: 50px; }

footer {
  padding: 50px;
  background-color: purple; }

/*# sourceMappingURL=default.css.map */
````

### Les commentaires
- // -> Affiché en CSS
- /* */ -> Non affiché en CSS

### Les opérations simples
````scss
padding: 4px + 5px;

$maVariableA = "Hello ";
$maVariableB = "World";
$total = $maVariableA + $maVariableB // "Hello World"

padding: 200px / 20px; // ERREUR
padding: 200px / 20; // OK

padding: 200px * 20px; // ERREUR
padding: 200px * 20; // OK
````

## Utiliser Sass
### L'imbrication
````scss
footer {
    padding: 50px;
    background-color: $primaryColor;
    // le texte du span dans footer sera en blanc
    span {
        color: white;
    }
}
````

### Rôle de l'opérateur

### L'importation
On crée un fichier _header. l'underscore indique à SASS que l'on ne veut pas qu'il transforme ce fichier en CSS. Il faut ensuite l'importé.
````scss
// design/sass/default.scss
$primaryColor: purple;
// A placer après la déclaration des variables
@import 'header';
````

### L'héritage
A utiliser quand plusieurs sélecteur utilisent des paramètres identiques.
````scss
// bloc à hériter
%alert{
    border: 1px solid yellow;
    padding: 15px;
    color: white;
}

.alert-green{
    @extend %alert;
    background-color: green;

}

.alert-red{
    @extend %alert;
    background-color: red;
}
````

### Les mixins
Ce sont des fonctions (avec ou sans paramètres). A utiliser quand plusieurs sélecteur utilisent des paramètres différents.
````scss
// design/sass/default.scss
@mixin border-radius($degres) {
    -moz-border-radius: $degres;
    -webkit-border-radius : $degres;
    -ms-border-radius: $degres;
    border-radius: $degres;
}
// ...
%alert {
    border: 1px solid yellow;
    padding: 15px;
    color: white;
    @include border-radius(15px);
}
````

### Exercice : un mixin pour Google Fonts
````scss
@mixin googleFonts($font) {
    @import url('https://fonts.googleapis.com/css?family=#{$font}');
}
// ...
// Fonts
@include googleFonts(Roboto);
@include googleFonts("Noto+Sans+TC");
// ...
footer {
  // ...
  font-family: 'Noto Sans TC', 'Roboto';
  // ...
}
````

## Les fonctions
### Fonctions natives
https://sass-lang.com/documentation/modules

### Créer sa fonction
````scss
// Créer
@function thewallstreet($nombreA, $nombreB) {
    @return $nombreA / $nombreB + $nombreA * ($nombreB - $nombreA);
}
// ...
// Appeler
content: thewallstreet(10, 10);
````

### Conditions @if, @else if et @else
````scss
$theme: white;
// ...
%theme {
    @if ($theme == purple) {
        color: purple;
        background-color: white;
    }
    @else if($theme == white) {
        color: white;
        background-color: black;
    } @else {
        color: black;
        background-color: white;
    }
}
// ...
body {
    @extend %theme;
}
````

### Les boucles @for
````scss
// Création de classes multiples
// grid-1 -> width: 100px, grid-2 -> width: 200px...
@for $i from 1 through 6 {
    .grid-#{$i} {
        width: 100px * $i;
    }
}
````

### Les boucles @each
Utilisées en général quand on a plusieurs images à créer
````scss
// On crée une classe avec une image en background avec un nom différent
@each $name in mon-super-site, bootstrap, php, sass {
    .#{$name}-icon {
        background-image: url('/img/#{$name}.png');
    }
}
````

### Les boucles @while

````scss
$i: 0;
@while $i <= 6 {
    .grid-#{$i} {
        width: 100px * $i;
    }

    $i: $i+1;
}
````

## Astuces
### Les listes
````scss
// liste avec 4 éléments séparés par des virgules
// si un élément avec des espace, séparé par des "
$list: mon-super-site, bootstrap, php, sass;
````

### La fonction nth
````scss
// nbth(liste, élément) -> l'index commence par 1 et pas 0.
content: nth($list, 1);
````

### Ajouter des valeurs à une liste
````scss
$list: mon-super-site, bootstrap, php, sass;

$langage: symfony;

$list: append($list, $langage, comma);
````

### @at-root
````scss
// Exemple HS
// Pour garder un harmonie dans le code et mettre le fade sous l'avatar sur lequel il est défini
.avatar {
  background-color: red;
  height: 120px;
  margin: 40px;
  width: 120px;
 
  @at-root {
    @keyframes fade {
      0% { transform: scale(1.0); }
      25% { transform: scale(1.1); }
      50% { transform: scale(1.0); }
      75% { transform: scale(1.2); }
      100% { transform: scale(1.1); }
    }
  }
  &:hover {
    animation: fade .8s infinite ease-in alternate;
  }
}
````

### Les Maps
````scss
// Maps
// Déclaration
$default: (color: blue, font-size: 1em);
// ...
// Utilisation
color: map-get($default, color);
````

### Exercice : Générateur de classes de couleurs
1ère méthode :
````scss
$couleurs: (blue: blue, red: red, green: green, gray: gray, purple: purple);

@each $key, $value in $couleurs {
    .color-#{$value} {
        color: $value;
    }
}
````

2e méthode :
````scss
$couleurs: blue, red, green, gray, purple;

@each $value in $couleurs {
    .color-#{$value} {
        color: $value;
    }
}
````