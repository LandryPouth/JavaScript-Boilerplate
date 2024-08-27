# JavaScript-Boilerplate
Un boilerplate et guide détaillé pour la configuration optimale d'un projet vanilla JavaScript

## 1. Initialisation du projet

Crée un nouveau dossier pour ton projet et initialise un projet npm :

```bash
mkdir mon-projet-js
cd mon-projet-js
npm init -y
```

## 2. Installation des dépendances

Installe Webpack, Babel, et les autres dépendances nécessaires :

```bash
npm install --save-dev webpack webpack-cli webpack-dev-server babel-loader @babel/core @babel/preset-env html-webpack-plugin clean-webpack-plugin sass-loader sass
```

## 3. Structure du projet

Voici une structure recommandée pour ton projet :

```
mon-projet-js/
│
├── src/
│   ├── index.js
│   ├── styles/
│   │   └── style.scss
│   └── index.html
│
├── dist/
│   └── (ce dossier sera généré par Webpack)
│
├── .babelrc
├── webpack.config.js
└── package.json
```

## 4. Configuration de Babel

Crée un fichier `.babelrc` à la racine du projet :

```json
{
  "presets": ["@babel/preset-env"]
}
```

## 5. Configuration de Webpack

Crée un fichier `webpack.config.js` à la racine du projet :

```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const { CleanWebpackPlugin } = require('clean-webpack-plugin');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
        },
      },
      {
        test: /\.scss$/,
        use: ['style-loader', 'css-loader', 'sass-loader'],
      },
    ],
  },
  plugins: [
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
  ],
  devServer: {
    static: './dist',
    hot: true, // Active le Hot Module Replacement pour JS et CSS
    open: true, // Ouvre automatiquement le navigateur
    watchFiles: ['src/**/*.html'], // Surveille les changements dans les fichiers HTML
  },
  mode: 'development', // Change to 'production' for production builds
};
```

## 6. Création du fichier `index.html`

Dans le dossier `src`, crée un fichier `index.html` avec le contenu suivant :

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mon Projet Vanilla JS</title>
</head>
<body>
  <h1>Hello, World!</h1>
  <script src="bundle.js"></script>
</body>
</html>
```

## 7. Scripts dans `package.json`

Ajoute les scripts suivants dans ton `package.json` pour faciliter le développement et la construction de ton projet :

```json
"scripts": {
  "start": "webpack serve --open",
  "build": "webpack --mode production"
}
```

## 8. Utilisation de SCSS dans ton projet

Tu peux maintenant écrire du SCSS dans `style.scss` et l'importer dans ton `index.js` :

```javascript
// src/index.js

import './styles/style.scss';

// Ton code JavaScript ici

if (module.hot) {
  module.hot.accept();
}
```

## 9. Lancer le projet

Pour démarrer ton projet en mode développement avec Webpack Dev Server :

```bash
npm start
```

Pour construire ton projet pour la production :

```bash
npm run build
```

