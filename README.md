# Introduction à Node.js

**Présentation :** [Lien vers la présentation](https://docs.google.com/presentation/d/1jf586G62z-13970_4TmWhnYsR9jZUjg8rGzMNwfTQkg/edit?usp=sharing)

## Crée ton premier code backend

### 1. Installe Node.js et NPM

Pour commencer, rends-toi sur la page officielle de [Node.js](https://nodejs.org/) et télécharge la version LTS (Long Term Support), qui est la version stable recommandée, pour Windows ou ta plateforme.

L'installateur pour Windows installe à la fois Node.js et NPM.

#### Vérification de l'installation

L'installation de Node.js ajoutera la commande `node` dans ton terminal (Windows, VSCode, etc.). Pour vérifier que tout est bien installé, ouvre un terminal et tape les commandes suivantes :

```sh
node -v
npm -v
```

Ces commandes devraient afficher les versions de Node.js et NPM installées.

#### Utilisation du terminal
Nous utiliserons souvent le terminal pour exécuter des programmes Node.js. La commande node te permettra de lancer des programmes Node.js directement depuis le terminal.

NPM (Node Package Manager) te permettra d'ajouter des bibliothèques (ou "paquets") à ton projet. Il installe également la commande npm.

### 2. Initialise ton projet backend
Crée un dossier de projet : Ouvre un nouveau dossier vide dans VSCode.
Ouvre un terminal dans VSCode : Va dans le menu Terminal > Nouveau Terminal.
Dans le terminal qui apparaît, tape la commande suivante :

```sh
npm init
```

Réponds aux questions posées. Cela créera un fichier package.json à la racine de ton dossier. Ce fichier contiendra la liste des bibliothèques que tu installeras.

### 3. Installe le paquet Express.js
Express.js est une bibliothèque qui facilite la création de serveurs web avec Node.js.

#### Installe Express.js : 
Dans le terminal, tape la commande suivante :

```sh
npm install express
```

#### Crée un fichier index.js : 
À la racine de ton dossier, crée un fichier index.js et copie-colle le code suivant depuis le site officiel : Express Hello World.

#### Lance ton programme Node.js : 
Dans le terminal, tape :

```sh
node index.js
```

Si tout fonctionne, tu devrais pouvoir accéder à l'adresse http://localhost:3000.

### 4. Fais ta première route GET /ma-page
En backend, une "route" est simplement une adresse web. On peut interroger une adresse web de deux façons : GET ou POST.

#### Création d'une nouvelle route GET
Le but de cet exercice est de créer une nouvelle route en GET avec l'adresse /ma-page, ce qui donnera l'URL http://localhost:3000/ma-page. Ajoute ce code dans ton fichier index.js :

```js
app.get('/ma-page', (req, res) => {
    res.send('Bienvenue sur ma page!');
});
```

Pour tester ta nouvelle route, relance le serveur en arrêtant le précédent (Ctrl+C dans le terminal) et en relançant la commande :

```sh
node index.js
```

Puis, visite http://localhost:3000/ma-page.

### 5. Aller plus loin en manipulant les fichiers
Nous allons maintenant créer un formulaire HTML sur /ma-page et traiter les données soumises pour créer un fichier.

#### Afficher un formulaire HTML
Remplace le contenu de la route /ma-page par ceci :

```js
app.get('/ma-page', (req, res) => {
    res.send('<form action="/creer-fichier"><input type="text" name="mon_input"><button type="submit">Envoyer</button></form>');
});
```

#### Créer une route pour traiter le formulaire
Ajoute cette nouvelle route à ton fichier index.js :

```js
app.get('/creer-fichier', (req, res) => {
    const fs = require('fs');
    const content = req.query.mon_input;

    try {
        fs.writeFileSync('test.txt', content);
        res.send("Fichier créé !");
    } catch (err) {
        console.error(err);
        res.send("Échec de création du fichier.");
    }
});
```

Maintenant, envoie une phrase via le formulaire sur /ma-page et observe la création d'un fichier test.txt contenant le texte saisi.

#### Créer un fichier différent à chaque fois
Pour créer un fichier unique à chaque soumission, utilise un nom de fichier dynamique :

```js
app.get('/creer-fichier', (req, res) => {
    const fs = require('fs');
    const content = req.query.mon_input;
    const fileName = `file_${Date.now()}.txt`; // Utilise un timestamp pour le nom du fichier

    try {
        fs.writeFileSync(fileName, content);
        res.send(`Fichier ${fileName} créé !`);
    } catch (err) {
        console.error(err);
        res.send("Échec de création du fichier.");
    }
});
```

Maintenant, chaque soumission créera un nouveau fichier avec un nom unique.
