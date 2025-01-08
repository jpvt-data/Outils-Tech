[⬅ Page Précédente](../README.md)

# Introduction au HTML et CSS

Cette fiche a pour objectif de fournir une introduction aux deux principaux outils utilisés pour la création de pages web : le HTML (HyperText Markup Language) et le CSS (Cascading Style Sheets).

L'objectif est de comprendre les bases de leur fonctionnement, leur interaction, et comment les utiliser pour construire une page web simple mais fonctionnelle. La distinction entre HTML et CSS sera clarifiée afin de pouvoir réaliser sa première page web en les utilisant conjointement.

## Objectifs de la fiche

- Comprendre le rôle du HTML et du CSS dans la création d'une page web.
- Savoir utiliser les balises HTML pour structurer le contenu d'une page.
- Apprendre à séparer la structure (HTML) de la présentation (CSS).
- Créer une page web de base en HTML et la styliser avec CSS.

## HTML : Structure d'une Page Web

### Définition et rôle
Le HTML est le langage qui structure le contenu d'une page web. Il sert à décrire les éléments de la page, comme les titres, les paragraphes, les images, les liens, etc., et à indiquer leur organisation. Une page HTML est composée d’un ensemble de balises qui indiquent comment le contenu doit être interprété et structuré par le navigateur.

### Structure de base d'une page HTML

La structure d'une page HTML est relativement simple. Voici un exemple de base :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ma première page web</title>
</head>
<body>
    <h1>Bienvenue sur ma première page</h1>
    <p>Ceci est un paragraphe de texte sur ma page web.</p>
</body>
</html>
```

### Explication des éléments

- `<!DOCTYPE html>` : Cette déclaration informe le navigateur qu'il s'agit d'une page HTML5.
- `<html lang="fr">` : Définit la langue de la page (ici le français).
- `<head>` : Contient des informations métadonnées comme le titre de la page et la configuration du charset.
- `<body>` : Contient le contenu visible de la page (titres, textes, images, etc.).
- `<h1>` : Balise de titre de niveau 1, généralement utilisée pour le titre principal.
- `<p>` : Balise de paragraphe, utilisée pour insérer du texte.

### Notion de balises
Les balises HTML sont toujours entourées de signes `<` et `>`. Certaines balises, comme `<h1>` ou `<p>`, nécessitent une balise de fermeture correspondante, c’est-à-dire `</h1>` ou `</p>`. L’indentation n’est pas obligatoire, mais elle rend le code plus lisible.

Exemple d’une page avec plusieurs paragraphes :

```html
<body>
    <h1>Ma page avec plusieurs paragraphes</h1>
    <p>Ceci est le premier paragraphe.</p>
    <p>Ceci est le deuxième paragraphe.</p>
</body>
```

## CSS : La Présentation de la Page Web

### Définition et rôle
Le CSS est utilisé pour décrire l'apparence des éléments HTML. Il permet de définir le style de la page : couleurs, polices, mises en page, espacements, etc. Le CSS est séparé du HTML, ce qui permet de modifier l'apparence de toutes les pages d'un site en modifiant un seul fichier CSS.

### Syntaxe de base du CSS

Le CSS est constitué de règles. Chaque règle est composée d'un sélecteur (qui indique quel élément HTML sera modifié) et d'un ou plusieurs déclarations (qui indiquent ce qui doit être modifié). Une règle CSS ressemble à ceci :

```css
h1 {
    color: blue;
    text-align: center;
}
```

Ici, la règle CSS modifie l'apparence des éléments `<h1>` de la page :
- `color: blue;` change la couleur du texte en bleu.
- `text-align: center;` centre le texte.

### Exemple complet de HTML et CSS

Voici un exemple d'une page HTML avec un fichier CSS associé pour la mise en forme :

**HTML (index.html)**
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Stylisée</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Bienvenue sur ma page stylisée</h1>
    <p>Ceci est un paragraphe avec du style.</p>
</body>
</html>
```

**CSS (style.css)**
```css
body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
}

h1 {
    color: darkblue;
    text-align: center;
}

p {
    color: darkgreen;
    font-size: 16px;
}
```

### Séparation du fond et de la forme
L'idée principale derrière l'utilisation de HTML et CSS est la séparation du **fond** (structure de la page) et de la **forme** (style de la page). Cette séparation permet une maintenance plus facile, car il suffit de modifier le fichier CSS pour changer l'apparence de plusieurs pages HTML.

### Exemple pratique
Si on souhaite que tous les titres h1 d’un site deviennent verts avec un fond gris, il suffira de modifier le CSS :

```css
h1 {
    color: green;
    background-color: grey;
}
```

Toutes les pages utilisant ce fichier CSS seront automatiquement mises à jour.

## Conclusion

L'HTML et le CSS sont les fondements de toute page web. HTML structure le contenu, tandis que CSS en définit l'apparence. Ensemble, ils permettent de créer des pages web à la fois fonctionnelles et visuellement attrayantes. Une bonne maîtrise de ces deux technologies est essentielle pour la création de sites web.

[⬅ Page Précédente](../README.md)