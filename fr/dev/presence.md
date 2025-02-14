---
title: Développement de la presence
description:
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2020-06-11T18:04:02.843Z
---

> Toutes les presences sont maintenant stockées ici : https://github.com/PreMiD/Presences 
> 
> {.is-info}

La version `2.x` introduit le [magasin de presence](https://premid.app/store). Les utilisateurs ont maintenant la possibilité d'ajouter et de supprimer manuellement leurs presences favorites via l'interface utilisateur du [site web](https://premid.app/).

> Avant de commencer, il est fortement recommandé de consulter nos directives par rapport aux Presences. 
> 
> {.is-warning}

- [Instructions](https://docs.premid.app/dev/presence/guidelines)
{.links-list}

# Structure

Toutes les présences sont codées en [TypeScript](https://www.typescriptlang.org/). [TypeScript](https://www.typescriptlang.org/) a quelques définitions de types supplémentaires épicés, donc la correction et l'identification des bugs est beaucoup plus facile.

## Installation

1. Installez [Git](https://git-scm.com/).
2. Installez [Node](https://nodejs.org/en/) (fourni avec [npm](https://www.npmjs.com/)).
3. Installez [TypeScript](https://www.typescriptlang.org/index.html#download-links) (ouvrez un terminal et `npm installez -g typescript`).

## Cloner le projet

1. Ouvrez un terminal et tapez `git clone https://github.com/PreMiD/Presences`.
2. Choisissez un dossier.
3. Ouvrez-le dans votre éditeur de code.

## Création de dossiers et de fichiers

1. Allez dans le dossier `websites` puis allez dans le dossier avec la première lettre du **nom** (et non une URL) du service que vous voulez supporter.
2. Créez un dossier avec le **name** (pas une URL) du service que vous voulez supporter.
3. Créez un fichier `presence.ts` et un fichier `tsconfig.json` à l'intérieur.
4. Créer un dossier nommé `dist` à l'intérieur.
5. Créer un fichier `metadata.json` dans le dossier `dist`.

## Remplir le fichier tsconfig.json

Veuillez mettre le code suivant dans le fichier `tsconfig.json`.

```json
{
  "extends": "../../../tsconfig.json",
  "compilerOptions": {
    "outDir": "./dist/"
  }
}
```

Pour en savoir plus sur la configuration de TypeScript, cliquez [ici](/dev/presence/tsconfig).

## Remplir le fichier metadata.json

Nous avons fait un créateur de fichier `metadata.json` pour les paresseux [ici](https://eggsy.xyz/projects/premid/mdcreator). Il est toujours suggéré de lire ceci afin que vous sachiez comment cela fonctionne.

```json
{
  "$schema": "https://schemas.premid.app/metadata/1.5",
  "author": {
    "name": "UTILISATEUR",
    "id": "ID"
  },
  "contributors": [
    {
      "name": "UTILISATEUR",
      "id": "ID"
    }
  ],
  "service": "SERVICE",
  "altnames": ["SERVICE"],
  "description": {
    "en": "DESCRIPTION"
  },
  "url": "URL",
  "version": "VERSION",
  "logo": "URL",
  "thumbnail": "URL",
  "color": "#HEX000",
  "tags": ["TAG1", "TAG2"],
  "category": "CATEGORIE",
  "regExp": "REGEXP",
  "iFrameRegExp": "REGEXP",
  "iframe": false,
  "readLogs": false,
  "settings": [
    {
      "id": "ID",
      "multiLanguage": true
    },
    {
      "id": "ID",
      "title": "TITRE AFFICHE",
      "icon": "ICONE FONTAWESOME",
      "value": true
    },
    {
      "id": "ID",
      "if": {
        "ID": true
      },
      "title": "TITRE AFFICHE",
      "icon": "ICONE FONTAWESOME",
      "value": "\"%song%\" by %artist%",
      "placeholder": "utiliser %song% ou %artist%"
    },
    {
      "id": "ID",
      "title": "TITRE AFFICHE",
      "icon": "ICONE FONTAWESOME",
      "value": 0,
      "values": ["1", "2", "ect."]
    }
  ]
}
```

Veuillez copier le code ci-dessus et le mettre dans votre fichier `metadata.json`. Vous devez maintenant modifier les valeurs des propriétés. Veuillez noter que les propriétés suivantes sont optionnelles à avoir dans vos métadonnées `. son` fichier, si vous ne prévoyez pas de les utiliser, vous devez les supprimer.

- `contributors`
- `altnames`
- `regExp`
- `iframe`
- `iFrameRegExp`
- `readLogs`
- `settings`

**Clarification de certaines valeurs prédéfinies :**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Facultatif</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>author</b></td>
      <td style="text-align:left">Doit contenir un Objet avec le <code>nom</code> et l'<code>id</code> du développeur de la Presence. <code>name</code> est votre nom d'utilisateur Discord sans l'identifiant(#0000). L'<code>id</code> utilisateur peut être copié depuis Discord en activant le mode développeur
        et en faisant un clic droit sur votre profil.</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>Non</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>contributors</b></td>
      <td style="text-align:left">Doit contenir un Objet avec le <code>nom</code> et l'<code>id</code> du développeur de la Presence. <code>name</code> est votre nom d'utilisateur Discord sans l'identifiant(#0000). Votre <code>id</code> d'utilisateur peut être obtenu sur Discord en activant le mode développeur et en faisant un clic droit sur votre profil.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>Oui</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>service</b></td>
      <td style="text-align:left">Le titre du service que cette présence supporte.<br>
      (Doit être du même nom que le dossier où tout se trouve)</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Non</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>altnames</b></td>
      <td style="text-align:left">Soyez en mesure de rechercher la presence en utilisant un nom alternatif.<br>
      Destiné à être utilisé pour les presences qui ont des noms différents dans des langues différentes (par ex. Pokémon et 포켓몬스터).<br>
      Vous pouvez également l'utiliser pour les presences qui ont des caractères spéciaux afin que vous n'ayez pas à les taper (par ex. Pokémon et Pokemon).</td>
      <td style="text-align:left"><code>Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Oui</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>description</b></td>
      <td style="text-align:left">Petite description de la presence, vous pouvez utiliser la description du service si vous n'avez pas d'idées. Votre description doit avoir des valeurs de paire de clés qui indiquent la langue, et la description dans cette langue spécifique. Faites les descriptions avec les langues <i>que vous connaissez</i>, nos traducteurs apporteront des modifications à votre fichier metadata.</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>Non</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>url</b></td>
      <td style="text-align:left">URL du service.<br><b>Exemple :</b><code>vk.com</code><br>
        <b>Cette URL doit correspondre à l'URL du site car elle détectera si oui ou non c'est le site Web auquel il faut injecter le script.</b><br> 
<b>Ne pas</b> ajouter <code>https://</code> ou <code>http://</code> à l'intérieur de l'URL ni un slash à la fin :
<code>https://premid.app/</code> -> <code>premid.app</code><br>
<b>Note</b>: Certaines URLs peuvent avoir <code>www.</code> ou quelque chose d'autre devant leur domaine. N'oubliez <b>PAS</b> de l'ajouter !<br>
      Vous pouvez ajouter plusieurs URL en faisant ce qui suit :<br>
      <code>["URL1", "URL2", "ETC. ]</code><br>
      Vous pouvez également utiliser regExp aussi connu sous le nom de Regex pour cette tâche, expliqué plus loin ci-dessous.</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Non</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>regExp</b></td>
      <td style="text-align:left">Une expression régulière utilisée pour faire correspondre les URLs.<br>
      regExp aussi connu sous le nom de Regex peut être utilisé si un site web a plusieurs sous-domaines.<br>
      Vous pouvez utiliser le regExp suivant pour cela :<br>
      <code>([a-z0-9]+)[.]domaine[.]TLD"</code><br>
      TLD signifie Top Level Domain (Domaine de Premier Niveau), par exemple : .com .net (ne mettez pas le point).<br>
      <code>([a-z0-9]+)</code> signifie "tout de a à z et de 0 à 9.<br>
      Vous pouvez vous renseigner sur les bases en regardant cette <a href="https://youtu.be/sXQxhojSdZM">vidéo</a>.<br>
      Vous pouvez tester votre regExp sur <a href="https://regex101.com/">Regex101</a>.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Oui</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>version</b></td>
      <td style="text-align:left">Version de votre presence.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Non</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>logo</b></td>
      <td style="text-align:left">Lien vers le logo du service.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Non</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>thumbnail</b></td>
      <td style="text-align:left">Lien vers votre miniature de presence.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Non</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>color</b></td>
      <td style="text-align:left">Valeur <code>#HEX</code> (hexadécimale). Nous vous recommandons d'utiliser une des couleurs primaires du service
        pour lequel vous développez votre presence.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Non</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>tags</b></td>
      <td style="text-align:left">Tableau avec des tags, ils aideront les utilisateurs à rechercher votre presence sur le site Web.</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Non</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>category</b></td>
      <td style="text-align:left">Une chaîne utilisée pour représenter la catégorie à laquelle appartient la presence. Voir les catergories valides <a href="https://docs.premid.app/dev/presence/metadata#presence-categories">ici</a>.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Non</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iframe</b></td>
      <td style="text-align:left">Définit si des <code>iFrames</code> sont utilisés.</td>
      <td style="text-align:left"><code>Boolean</code></td>
      <td style="text-align:left"><code>Oui</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iFrameRegExp</b></td>
      <td style="text-align:left">Un sélecteur d'expression régulière qui sélectionne les iframes à injecter. Voir regExp pour plus d'informations.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Oui</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>readLogs</b></td>
      <td style="text-align:left">Définit si l'extension doit lire les logs.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Oui</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>settings</b></td>
      <td style="text-align:left">Un tableau de paramètres que l'utilisateur peut modifier.<br>
      En savoir plus sur les paramètres de présence <a href="https://docs.premid.app/dev/presence/metadata#presence-settings">ici</a>.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>Oui</code></td>
    </tr>
  </tbody>
</table>

## Pour commencer

```ts
const presence = new Presence({
  //The client ID of the Application created at https://discordapp.com/developers/applications
  clientId: "000000000000000000"
  }),
  //You can use this to get translated strings in their browser language
  strings = presence.getStrings({
    play: "presence.playback.playing",
    pause: "presence.playback.paused"
  });

/*
function myOutsideHeavyLiftingFunction(){
    //Grab and process all your data here

    // element grabs //
    // api calls //
    // variable sets //
}

setInterval(myOutsideHeavyLiftingFunction, 10000);
//Run the function separate from the UpdateData event every 10 seconds to get and set the variables which UpdateData picks up
*/

presence.on("UpdateData", async () => {
  /*UpdateData is always firing, and therefore should be used as your refresh cycle, or `tick`. Cela est appelé plusieurs fois par seconde dans la mesure du possible.

    It is recommended to set up another function outside of this event function which will change variable values and do the heavy lifting if you call data from an API.*/

  const presenceData: PresenceData = {
    //The key (file name) of the Large Image on the presence. These are uploaded and named in the Rich Presence section of your application, called Art Assets
    largeImageKey: "key",
    //The key (file name) of the Small Image on the presence. These are uploaded and named in the Rich Presence section of your application, called Art Assets
    smallImageKey: "key",
    //The text which is displayed when hovering over the small image
    smallImageText: "Some hover text",
     //The upper section of the presence text
    details: "Browsing Page Name",
    //The lower section of the presence text
    state: "Reading section A",
    //The unix epoch timestamp for when to start counting from
    startTimestamp: 3133657200000,
    //If you want to show Time Left instead of Elapsed, this is the unix epoch timestamp at which the timer ends
    endTimestamp: 3133700400000
    //Optionally you can set a largeImageKey here and change the rest as variable subproperties, for example presenceData.type = "blahblah"; type examples: details, state, etc.
  };
  //Update the presence with all the values from the presenceData object
  if (presenceData.details) presence.setActivity(presenceData);
  //Update the presence with no data, therefore clearing it and making the large image the Discord Application icon, and the text the Discord Application name
  else presence.setActivity();
});
```

Vous pouvez copier ceci dans votre fichier `presence.ts` et modifier les valeurs. Le réglage de toutes les valeurs se fait dans l'événement updateData.

Pour avoir des exemples, nous vous recommandons de jeter un œil au code de différentes presences comme 1337x ou 9GAG. Pour plus d'informations à propos de la classe `Presence`, cliquez [ici](/dev/presence/class).

Depuis la v2.2. il y a maintenant des Slideshows, cela vous permet d'afficher plusieurs interfaces `PresenceData` sur un intervalle, pour plus d'informations cliquez sur la classe `Slideshow` [ici](/dev/presence/slideshow).

## Impossible d'obtenir certaines données?!

Beaucoup de sites web utilisent des [iframes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) ([Inlineframes](https://en.wikipedia.org/wiki/HTML_element#Frames)). Ces balises html peuvent contenir plusieurs choses telles que des vidéos. Mais ils ne sont pas tout le temps très accessibles. Certains sont cachés ou tout simplement pas utilisés activement. Vérifiez si vous pouvez extraire l'information dont vous avez besoin sans les utiliser avant de faire du travail inutile.

1. Vérifiez les dans la console de vos navigateurs (assurez-vous que vous êtes sur l'onglet **Éléments**).
2. Recherchez (<kbd>CTRL</kbd>+<kbd>F</kbd> (Windows) ou <kbd>CMD</kbd>+<kbd>F</kbd> (MacOS)).
3. Exécutez `document.querySelectorAll("iframe")`.

Si vous trouvez que vos données sont dans un iFrame vous devez faire ce qui suit :

1. Créer un fichier `iframe.ts`.
2. Définissez iFrame à `true` dans votre fichier de métadonnées.
3. Remplir votre fichier iFrame.

```ts
const iframe = new iFrame();
iframe.on("UpdateData", async () => {
  //Get all the data you need out of the iFrame save them in variables and then send them using iframe.send
  iframe.send({
    //sending data
    video: video,
    time: video.duration
  });
});
```

4. Faire en sorte que votre fichier de présence reçoive les données du fichier iFrame.

```ts
presence.on("iFrameData", (data) => {
  iFrameVideo = data.video;
  currentTime = data.time;
});
```

**Note :** Le code ci-dessus doit être placé en dehors de l'événement updateData.

## Compilation

Ouvrez un invite de commande dans votre dossier et tapez `tsc -w` pour compiler le fichier `presence.ts` dans le dossier `/dist`.

# Chargement de la présence

1. Ouvrez l'extension dans le navigateur et maintenez le bouton <kbd>Shift</kbd>sur votre clavier.
2. **Charger les présences** apparaîtra dans la section Présences.
3. Cliquez dessus pendant que vous maintenez le bouton <kbd>Maj</kbd>.
4. Sélectionnez le dossier /dist de votre présence.

# Quelques éléments utiles

## Rechargement rapide

Le site web sur lequel vous travaillez se recharge automatiquement à chaque fois que vous sauvegardez un fichier quelconque dans votre espace de travail.

## Débogage

- Vous pouvez mettre `console.log("Test");` entre votre code et voir si votre console de navigateur vous donne cette sortie. Si oui, continuez et réessayez après la fonction suivante. Si ce n'est pas le cas, il y a une erreur ci-dessus.
- Si cela ne vous aide pas non plus, demandez à un développeur de presence sur notre serveur [Discord](https://discord.premid.app/) pour obtenir de l'aide.

# Explications des fichiers

- [Classe Presence](/dev/presence/class)
- [Classe Slideshow](/dev/presence/slideshow)
- [Classe l'iFrame](/dev/presence/iframe)
- [Fichier de métadonnées](/dev/presence/metadata)
- [Configuration de TypeScript](/dev/presence/tsconfig ""){.links-list}
