### Introduction à NodeJS

Présentation : https://docs.google.com/presentation/d/1jf586G62z-13970_4TmWhnYsR9jZUjg8rGzMNwfTQkg/edit?usp=sharing

# Créé ton premier code backend

## 1. Installe NodeJS et NPM

Pour commencer, va sur la page officielle de NodeJS.org et téléchargez la version LTS ( qui veut dire la dernière version stable ) pour Windows ou ta plateforme.
L'installeur spécial Windows installe à la fois NodeJS et NPM.

L'installation de NodeJS va ajouter la commande `node` dans ton terminal Windows/Vscode. 
Lorsqu'on fait du backend, on utilise souvent le terminal. Il va falloir s'habituer ! 

La commande `node` te permettra alors d'executer les programmes NodeJS. Et oui, les programmes NodeJS ne s'executent que dans le terminal, même si bien sûr on va continuer de faire des sites qui apparaissent dans le navigateur. 

NPM permet d'ajouter des librairies, que l'on appelle 'paquets' dans le jargon. 

Tout comme NodeJS installe la commande `node`, NPM installera la commande `npm`.

## 2. Initialise ton projet backend

Ouvre un nouveau dossier vide dans VSCode.
Dans ton éditeur VSCode, ouvre un nouveau terminal.
Dans le terminal qui apparaît, tape la commande suivante : `npm init` et répond aux questions.
Ceci va créer un fichier `package.json` à la racine de ton dossier, c'est normal ! 
Le but du fichier `package.json` est de contenir la liste des librairies que tu auras installé.

## 3. Installe le paquet ExpressJS

Suis les instructions du site officiel https://expressjs.com/

Créer un fichier index.js à la racine de ton dossier, et copie colle le code suivant : 

https://expressjs.com/en/starter/hello-world.html

Ensuite dans un nouveau terminal dans VSCode, tu n'as plus qu'à lancer la commande : 
`node index.js`

Ceci executer ton programme NodeJS. Est ce que ça marche ? 
Si ça marche, tu devrais pouvoir aller à l'adresse `http://localhost:3000`


## 4. Fais ta première route GET /ma-page

Dans le langage backend, une route c'est tout simplement une adresse web ! 
On peut interroger une adresse web de 2 façons : GET ou POST.

Le but de cet exercice est que tu arrives à créer une deuxieme route en GET qui aura pour adresse
"/ma-page" donc qui donnera l'url `http://localhost:3000/ma-page`.
Mets ce que tu veux comme contenu dans cette page.

> ⚠️ **Attention** ⚠️
> Lorsque tu modifies le code, il faut relancer le serveur en faisant CTRL+C dans le terminal et relancer `node index.js` 


# Aller plus loin en manipulant les fichiers

Essayons quelque chose de fun ! 
Au lieu d'afficher juste du texte dans ta page, tu vas mettre un code html d'input.

```js
app.get('/ma-page', (req, res) => {
    res.send('<form action="/creer-fichier"><input type="text" name="mon_input"></form>')
})
```


Essaye de créer une route capable de recevoir une phrase saisie depuis la page précédente et de créer un fichier automatiquement dans ton projet qui contiendra le texte saisi ! 

```js
app.get('/creer-fichier', (req, res) => {
    const fs = require('fs');

    const content = req.query.mon_input;

    try {
        fs.writeFileSync('test.txt', content);
        res.send("Fichier créé !");
    } catch (err) {
        console.error(err);
        res.send("Echec de création du fichier.");
    }
})
```

Essaye maintenant de trouver un code qui permet de créer un fichier différent à chaque fois. 