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
À la racine de ton dossier, crée un fichier index.js et copie-colle le code suivant depuis le site officiel : [Express Hello World](https://expressjs.com/fr/starter/hello-world.html).

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

### Explication du code ci-dessus

```js
/* 1. Requête GET : Pour récupérer les données envoyées via le formulaire, tu dois utiliser req.query
    pour accéder aux paramètres de la requête. Par exemple, pour accéder au contenu de l'input
    nommé mon_input, utilise req.query.mon_input.

    2. Utilisation de fs : La bibliothèque fs (file system) de Node.js permet de manipuler les fichiers.
    Tu peux l'importer avec const fs = require('fs');.

    3. Créer un fichier : Utilise la méthode fs.writeFileSync pour écrire dans un fichier.
    Cette méthode prend deux arguments : le nom du fichier et le contenu à écrire.

    4. Retourner une réponse : Une fois le fichier créé, envoie une réponse au client
    en utilisant res.send.
*/
```

### Créer un fichier différent à chaque fois
Pour créer un fichier unique à chaque soumission, utilise un nom de fichier dynamique.
Voici un guide détaillé :

1. Importer fs : const fs = require('fs');
2. Récupérer le contenu de l'input : const content = req.query.mon_input;
3. Générer un nom de fichier unique : const fileName = \file_${Date.now()}.txt`;`
4. Écrire dans le fichier : fs.writeFileSync(fileName, content);
5. Envoyer une réponse : res.send(\Fichier ${fileName} créé !`);`


Maintenant, chaque soumission créera un nouveau fichier avec un nom unique.

Bravo! Passsons à quelques exercices simples.

## Exercices 

### Exercice 1 : Afficher une page HTML
Crée une nouvelle route en GET avec l'adresse `/page-html` qui affiche une page HTML contenant un titre `<h1>` et un paragraphe `<p>` avec un texte de ton choix.

### Exercice 2 : Afficher une liste de courses
Crée une nouvelle route en GET avec l'adresse `/courses` qui affiche une liste de courses sous forme de texte. Tu peux stocker les éléments de la liste dans un tableau et les afficher en utilisant une boucle `forEach`.

### Exercice 3 : Afficher l'heure actuelle
Crée une nouvelle route en GET avec l'adresse `/heure` qui affiche l'heure actuelle au format HH:MM:SS. Utilise la fonction `new Date()` pour obtenir l'heure actuelle et formate-la de manière appropriée.
