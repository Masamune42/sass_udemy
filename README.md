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