---
title: Presence-Entwicklung
description:
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2020-06-11T18:04:02.843Z
---

> Alle Presences werden jetzt hier gespeichert: https://github.com/PreMiD/Presences 
> 
> {.is-info}

Version `2.x` führt den [Presence Store](https://premid.app/store) ein. Benutzer haben jetzt die Möglichkeit, ihre Lieblingspräsenzen manuell über die Benutzeroberfläche der [Website](https://premid.app/) hinzuzufügen und zu entfernen.

> Bevor du anfängst, solltest du dir unsere Presencerichtlinien anschauen. 
> 
> {.is-warning}

- [Richtlinien](https://docs.premid.app/dev/presence/guidelines)
{.links-list}

# Struktur

Alle Presences sind in [TypeScript](https://www.typescriptlang.org/) geschrieben. [TypeScript](https://www.typescriptlang.org/) enthält einige besonders strenge Typdefinitionen, sodass das Beheben und Erkennen von Fehlern viel einfacher ist.

## Installation

1. Installiere [Git](https://git-scm.com/).
2. Installiere [Node](https://nodejs.org/en/) ([npm](https://www.npmjs.com/) integriert).
3. Installiere [TypeScript](https://www.typescriptlang.org/index.html#download-links) (öffne ein Terminal und `npm install -g typescript`).

## Projekt klonen

1. Öffne ein Terminal und gib `git clone https://github.com/PreMiD/Presences` ein.
2. Wähle einen Ordner Deiner Wahl.
3. Öffne es in Deinem Code-Editor.

## Ordner und Dateien werden erstellt

1. Gehe in den `Webseiten` Ordner und dann in den Ordner mit dem ersten Buchstaben des **name** (keine URL) des Dienstes, den du unterstützen willst.
2. Erstelle einen Ordner mit dem **Namen** (keine URL) des Dienstes, den Du unterstützen möchtest.
3. Erstelle eine `presence.ts` und eine `tsconfig.json` Datei im Inneren.
4. Erstelle einen Ordner mit dem Namen `dist`.
5. Erstelle eine `metadata.json` im Ordner `dist`.

## Ausfüllen der tsconfig.json

Bitte gib den folgenden Code in die Datei `tsconfig.json` ein.

```json
{
  "extends": "../../../tsconfig.json",
  "compilerOptions": {
    "outDir": "./dist/"
  }
}
```

Um mehr über die TypeScript-Konfiguration zu erfahren, klicke [hier](/dev/presence/tsconfig).

## Ausfüllen der metadata.json

Wir haben eine `metadata.json`-Datei für die Lazy Peeps [hier](https://eggsy.xyz/projects/premid/mdcreator). Es wird immer noch empfohlen, dies durchzulesen, damit Du weißt, wie es funktioniert.

```json
{
  "$schema": "https://schemas.premid.app/metadata/1.5",
  "author": {
    "name": "USER",
    "id": "ID"
  },
  "contributors": [
    {
      "name": "USER",
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
  "category": "CATEGORY",
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
      "title": "DISPLAY TITLE",
      "icon": "FONTAWESOME ICON",
      "value": true
    },
    {
      "id": "ID",
      "if": {
        "ID": true
      },
      "title": "DISPLAY TITLE",
      "icon": "FONTAWESOME ICON",
      "value": "\"%song%\" by %artist%",
      "placeholder": "use %song% or %artist%"
    },
    {
      "id": "ID",
      "title": "DISPLAY TITLE",
      "icon": "FONTAWESOME ICON",
      "value": 0,
      "values": ["1", "2", "etc."]
    }
  ]
}
```

Bitte kopiere den obigen Code und füge ihn in Deine `metadata.json` ein. Du musst jetzt die Werte der Eigenschaften bearbeiten. Beachte, dass die folgenden Eigenschaften in Deiner `metadata.json` optional sind. Wenn Du sie nicht verwenden möchten, musst Du sie entfernen.

- `contributors`
- `altnames`
- `regExp`
- `iframe`
- `iFrameRegExp`
- `readLogs`
- `settings`

**Klarstellung einiger Wertvoreinstellungen:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable</th>
      <th style="text-align:left">Beschreibung</th>
      <th style="text-align:left">Typ</th>
      <th style="text-align:left">Optional</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>author</b></td>
      <td style="text-align:left">Sollte ein Objekt mit dem <code>name</code> und <code>id</code> des Presence-Entwickler enthalten. <code>name</code> ist dein Discord-Benutzername ohne den Identifikator (#0000). User <code>id</code> kann aus Discord kopiert werden, indem du den Entwicklermodus aktivierst und mit der rechten Maustaste auf dein Profil klickst.</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>contributors</b></td>
      <td style="text-align:left">Sollte ein Objekt mit dem <code>name</code> und <code>id</code> des Presence-Entwickler enthalten. <code>name</code> ist dein Discord-Benutzername ohne den Identifikator (#0000). User <code>id</code> kann aus Discord kopiert werden, indem du den Entwicklermodus aktivierst und mit der rechten Maustaste auf dein Profil klickst.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>Ja</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>service</b></td>
      <td style="text-align:left">Der Titel des Dienstes, der diese Presence unterstützt.<br>(Gib den Namen des Ordner an, in dem sich alles befindet)</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>altnames</b></td>
      <td style="text-align:left">Erlaubt es die Presence mit einem alternativen Namen zu suchen.<br>
      Soll für Presences, die verschiedene Namen in verschiedenen Sprachen haben, verwendet werden (z.B.: Pokémon und 포켓몬스터).<br>
      Dies kann auch genutzt werden für Presences, die spezielle Zeichen  haben, sodass diese nicht eingegeben werden müssen (z.B.: Pokémon und Pokemon).</td>
      <td style="text-align:left"><code>Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Ja</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>description</b></td>
      <td style="text-align:left">Kurze Beschreibung der Presence, du kannst die Beschreibung des Dienstes verwenden, wenn dir die Ideen ausgehen. Deine Beschreibung muss Schlüsselpaarwerte enthalten, die die Sprache angeben und die Beschreibung in dieser bestimmten Sprache. Erstelle Beschreibungen mit den Sprachen <i>die du kennst</i>, unsere Übersetzer werden Änderungen an der Metadatendatei vornehmen.</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>url</b></td>
      <td style="text-align:left">URL des Dienstes<br><b>Beispiel</b><code>vk.com</code><br>
<b>Diese URL muss mit der URL der Webseite übereinstimmen, da diese erkennt, ob es sich um die richtige Seite handelt, in der das Skript injiziiert werden soll.</b><br> Füge <b>KEIN</b> <code>https://</code> oder <code>http://</code> zu der URL hinzu, auch kein Slash am Ende:
<code> https://premid.app/</code> -> <code>premid.app</code><br>
<b>Hinweis:</b> Einige URLs haben vielleicht ein <code>www.</code> oder ähnliches vor der Domain. <b>NICHT</b> vergessen, es hinzuzufügen!<br>
Du kannst mehrere URLs hinzufügen, indem du folgendes tust:<br>
<code>["URL1", "URL2", "ETC."]</code><br>
Du kannst auch Regulare Ausdrücke, auch bekannt als RegEx, für diese Aufgabe verwenden, welches dir weiter unten erklärt wird.</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>regExp</b></td>
      <td style="text-align:left">Ein regulärer Ausdrucks-String zum übereinstimmen der URLs.<br>
regExp, auch bekannt als RegEx, kann genutzt werden, um zu überprüfen, ob eine Webseite mehere Subdomains hat.<br>
Du kannst das folgende regExp dafür verwenden:<br>
<code>"([a-z0-9]+)[.]domain[.]TLD"</code><br>
TLD steht für Top Level Domain, ein Beispiel: .com .net (aber nicht den Punkt mit eingeben).<br>
<code>([a-z0-9]+)</code> bedeutet alles von a bis z und 0 bis 9.<br>
Du kannst ein kleines Starter <a href="https://youtu.be/sXQxhojSdZM">Video</a> angucken.<br>
Deine regExp kannst du auf <a href="https://regex101.com/">Regex101</a> testen.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Ja</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>version</b></td>
      <td style="text-align:left">Version deiner Presence.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>logo</b></td>
      <td style="text-align:left">Link zum Logo des Dienstes.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>thumbnail</b></td>
      <td style="text-align:left">Link zu deinem Presence-Vorschaubild.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>color</b></td>
      <td style="text-align:left"><code>#HEX</code> Wert. Wir empfehlen eine primäre Farbe des Dienstes zu nutzen
        , die Ihre Presence unterstützt.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>tags</b></td>
      <td style="text-align:left">Ein Array mit Schlagwörtern. Diese unterstützen den Benutzer bei der Suche nach deiner Presence auf der Webseite.</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>category</b></td>
      <td style="text-align:left">Eine Zeichenkette, die die Kategorie entspricht, in die deine Kategorie fällt. Sehen Sie <a href="https://docs.premid.app/dev/presence/metadata#presence-categories">hier</a> die gültigen Kategorien.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iframe</b></td>
      <td style="text-align:left">Legt fest ob <code>iFrames</code> verwendet werden.</td>
      <td style="text-align:left"><code>Boolean</code></td>
      <td style="text-align:left"><code>Nein</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iFrameRegExp</b></td>
      <td style="text-align:left">Einen regulären Ausdrück-Selector, der iFrames auswählt, in die injiziiert werden soll. Siehe regExp für weitere Informationen.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Ja</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>readLogs</b></td>
      <td style="text-align:left">Legt fest, ob die Erweiterung Logs lesen soll.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Ja</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>settings</b></td>
      <td style="text-align:left">Ein Array von Einstellungen, die der Benutzer ändern kann.<br>
      Lese mehr über Presenceeinstellungen <a href="https://docs.premid.app/dev/presence/metadata#presence-settings">hier</a>.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>Ja</code></td>
    </tr>
  </tbody>
</table>

## Erste Schritte

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
  /*UpdateData is always firing, and therefore should be used as your refresh cycle, or `tick`. Dies wird nach Möglichkeit mehrmals eine Sekunde aufgerufen.

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

Du kannst dies in Deine `presence.ts` kopieren und die Werte bearbeiten. Die Einstellung aller Werte ist fertig innerhalb des updataData Events.

Du kannst dies in Deine `presence.ts` kopieren und die Werte bearbeiten. Die Einstellung aller Werte ist fertig innerhalb des updataData Events.

Seit v2.2.0 gibt es Slideshows, die es dir erlauben mehrere `PresenceData`-Schnittstellen in einem Intervall anzuzeigen, für mehr Information über die `Slideshow`-Klasse, klicke [hier](/dev/presence/slideshow).

## Du kannst bestimmte Daten nicht abrufen?!

Viele Websites verwenden [iframes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) ([Inlineframes](https://en.wikipedia.org/wiki/HTML_element#Frames)). Diese HTML-Tags können mehrere Quellen enthalten, z.B. Videos. Aber sie sind nicht immer relevant. Manche sind versteckt oder einfach nicht aktiv genutzt. Prüfe, ob Du die benötigten Informationen extrahieren kannst, bevor Du Dir unnötige Arbeiten machst.

1. Überprüfe sie über die Browserkonsole (stelle sicher, dass Du Dich auf dem **Elements** Tab) befindest.
2. Suche (<kbd>Strg</kbd>+<kbd>F</kbd> (Windows) oder <kbd>CMD</kbd>+<kbd>F</kbd> (MacOS)).
3. Führe `document.querySelectorAll("iframe")` aus.

Wenn feststellst, dass sich Deine Daten in einem iFrame befinden, musst Du folgende Schritte ausführen:

1. Erstelle eine `iframe.ts`-Datei.
2. Setze iFrame in Ihrer Metadatendatei auf `true`.
3. Fülle Deine iFrame-Datei aus.

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

4. Ermögliche Deiner Presence-Datei, Daten aus der iFrame-Datei zu empfangen.

```ts
presence.on("iFrameData", (data) => {
  iFrameVideo = data.video;
  currentTime = data.time;
});
```

**Note:** Dies muss außerhalb des updateData Ereignis platziert werden.

## Kompilieren

**Hinweis:** Das muss außerhalb des updateData-Ereignisses platziert werden.

# Presence laden

1. Öffne das Erweiterungs-Popup im Browser und halte die <kbd>Umschalt</kbd>-Taste auf deiner Tastatur gedrückt.
2. **Presence laden** wird im Presence-Bereich erscheinen.
3. Klicke darauf, während Du die Taste <kbd>Shift</kbd> weiterhin gedrückt hälst.
4. Wähle den Ordner /dist Deiner Presence.

# Einige hilfreiche Dinge

## Hot-Neuladen

Öffne eine Konsole in Deinem Ordner und gib `tsc -w` ein, um die `presence.ts` in den Ordner `/dist` zu kompilieren.

## Debugging

- Du kannst `console.log("Test");` zwischen Deinen Code setzten und prüfen, ob Deine Browserkonsole diese Ausgabe liefert. Wenn ja, fahre fort und versuchen es nach der nächsten Funktion erneut. Falls nicht, liegt oben ein Fehler vor.
- Sollte dies nicht helfen, kannst du einen Presence-Entwickler auf unserem [Discord Server](https://discord.premid.app/) um Hilfe fragen.

# Dateien erklärt

- [Presence Klasse](/dev/presence/class)
- [Diashow Klasse](/dev/presence/slideshow)
- [iFrame Klasse](/dev/presence/iframe)
- [Metadatendatei](/dev/presence/metadata)
- [TypeScript Konfiguration](/dev/presence/tsconfig ""){.links-list}
