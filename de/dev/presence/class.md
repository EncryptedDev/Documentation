---
title: Presence-Klasse
description: Die Hauptklasse für jede PreMiD-Presence
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2021-09-07T01:44:50.164Z
---

# Presence-Klasse

## Einführung

Die Klasse `Presence` ist sehr nützlich, da sie grundlegende Methoden zum Erstellen einer Presence enthält.

Wenn du eine Klasse erstellst, musst du die Eigenschaft `clientId` angeben.

```ts
const presence = new Presence({
  clientId: "514271496134389561" // Beispiel clientid
});
```

### Eigenschaften

Für die `Presence`-Klasse, gibt es drei verfügbare Eigenschaften.

#### `clientId`

Diese Eigenschaft wird benötigt, damit deine Presence funktioniert, weil es die Anwendungs-Id benutzt, um Logo und Elemente anzuzeigen. Du bekommst dies auf deiner[Anwendungsseite](https://discordapp.com/developers/applications).

#### `injectOnComplete` - *Veraltet seit 2.2.4*

Beim setzen von `InjectOnComplete` zu `true`, wird das erste `UpdateData` Event für beide, die `presence.ts` und `iframe.js` Dateien erst gestartet, wenn die Seite fertig geladen ist.

#### `appMode` - *Veraltet seit 2.2.4*

Beim setzen von `appMode` zu `true` und die Presence sollte leere `PresenceData` senden, zeigt die App die Anwendung (Bild und Name) auf dem Benutzerprofil, anstatt nichts.

## Methoden

### `getActivity()`

Wirft ein `PresendeData` Objekt zurück, was die Presence anzeigt.

### `setActivity(PresenceData | Slideshow, Boolean)`

Legt Ihre Profilaktivität gemäß den bereitgestellten Daten fest.

Der erste Parameter benötig eine [`PresenceData`](#presencedata-interface) Schnittstelle oder eine [`Slideshow`](/dev/presence/slideshow) Klasse um alle Informationen zu erhalten, die Sie in Ihrem Profil anzeigen möchten.

Der zweite Parameter definiert, wann Presence etwas spielt oder nicht. Verwende immer `true`, wenn Sie einen Zeitstempel in `PresenceData` verwenden.

### `clearActivity()`

Löscht deine akutelle Aktivität und den Tray-Titel.

### `setTrayTitle(String)` - *Deprecated since 2.2.3*

> Diese Methode funktioniert nur unter Mac OS. 
> 
> {.is-warning}

Legt den Tray-Titel in der Menüleiste fest.

### `createSlideshow()`

Erstellt eine neue `Slideshow` Klasse.

```ts
const slideshow = presence.createSlideshow();
```

Es wird empfohlen, dies direkt nach dem erstellen der `Presence` Klasse zu tun:

```ts
const presence = new Presence({
    clientId: "514271496134389561" // Beispiel clientId
  }),
  slideshow = presence.createSlideshow();
```

Die Dokumentation für die `Slideshow` Klasse kannst du [hier](/dev/presence/slideshow) finden.

### `getStrings(Object)`

Eine asynchrone Methode, mit der du übersetzte Zeichenketten von der Erweiterung erhalten kannst.

Sie müssen ` Object ` mit Schlüsseln versehen, die der Schlüssel für die Zeichenfolge sind. ` keyValue ` ist der Zeichenfolgenwert. Eine Zusammenstellung der übersetzten Zeichenketten kann mit diesem Endpunkt gefunden werden: `https://api.premid.app/v2/langFile/presence/en/`

```ts
// Gibt `Playing` und `Paused` Strings
// der Erweiterung wieder.
const strings = await presence.getStrings({
  play: "general.playing",
  pause: "general.paused"
});

const playString = strings.play; // Ergebnis:  Playing
const pauseString = strings.pause; // Ergebnis: Paused
```

Seit v2.2.0 der Erweiterung können Sie nun die Zeichenketten einer bestimmten Sprache erhalten. Dies funktioniert gut mit der neu hinzugefügten `multiLanguage` Einstellung.

Wir empfehlen Ihnen, den folgenden Code zu verwenden, damit die PresenceData automatisch aktualisiert, wenn der Benutzer die ausgewählte Sprache ändert;

```ts
async function getStrings() {
  return presence.getStrings(
    {
      play: "general.playing",
      pause: "general.paused"
    },
    // The ID is the ID of the multiLanguage setting.
    await presence.getSetting("ID").catch(() => "en");
  );
}

let strings = getStrings(),
  // The ID is the ID of the multiLanguage setting.
  oldLang: string = await presence.getSetting("ID").catch(() => "en");

//! The following code must be inside the updateData event!
// The ID is the ID of the multiLanguage setting.
const newLang = await presence.getSetting("ID").catch(() => "en");
if (oldLang !== newLang) {
  oldLang = newLang;
  strings = getStrings();
}

const playString = (await strings).play, // result: Playing
  pauseString = (await strings).pause; // result: Paused
```

### `getPageletiable(String)`

Gibt eine Variable von der Webseite zurück, falls sie vorhanden ist.

**Warnung: Diese Funktion kann eine hohe CPU-Auslastung verursachen & Wenn es zu oft ausgeführt wird, dann kann dies Sitelagging verursachen.**

```ts
const pageVar = getPageletiable(".pageVar");
console.log(pageVar); // Das loggt den "Variableninhalt"
```

### `getExtensionVersion(Boolean)`

Gibt den Wert der Einstellung zurück.

```ts
getExtensionVersion(onlyNumeric?: boolean): string | number;

const numeric = presence.getExtensionVersion();
console.log(numeric); // Wird 210 loggen
const version = presence.getExtensionVersion(false);
console.log(version); // Wird 2.1.0 loggen
```

### `getSetting(String)`

Versteckt die Einstellung.

```ts
var setting = await presence.getSetting("pdexID"); // pdexID mit der Id von der Einstellung ersetzen
console.log(setting); // Dies loggt den Wert der Einstellung
```

### `hideSetting(String)`

Zeigt angegebene Anstellung an (Funktioniert nur, wenn die Einstellung schon versteckt war).

```ts
presence.hideSetting("pdexID"); // Ersetze pdexID mit der ID der Einstellung
```

### `showSetting(String)`

Gibt die Protokolle der Webseiten-Konsole wieder.

```ts
presence.showSetting("pdexID"); // Ersetze pdexID mit der id der Einstellung
```

### `getLogs()`

**Hinweis:** Benötigt `readLogs` auf `true` in der `metadata.json` Datei.

```ts
const logs = await presence.getLogs();
console.log(logs); // Dies logt die neusten 100 Logs (in einem Array).
```

Gibt die angegebene Meldung in der Konsole in einem Format aus, das auf die Presence im `info` Style basiert.

### `info(String)`

Gibt die angegebene Meldung in der Konsole in einem Format aus, das auf die Presence im `erfolgreich` Style basiert.

```ts
presence.info("Test") // Dies loggt "test" im korrekten Stil.
```

### `success(String)`

Gibt die angegebene Meldung in der Konsole in einem Format aus, das auf die Presence im `Fehler` Style basiert.

```ts
presence.success("Test") // Dies loggt "test" im korrekten Stil.
```

### `error(String)`

Wirft 2 `snowflake` Zeitstempel in einem `Array` zurück, die dann für `startTimestamp` und `endTimestamp` verwendet werden können.

```ts
presence.error("Test") // Dies loggt "test" im korrekten Stil.
```

### `getTimestampsfromMedia(HTMLMediaElement)`

**Hinweis:** Der gegebene `String` in querySelector ist nur ein Beispiel.

```ts
const timestamps = presence.getTimestampsfromMedia(document.querySelector(".video"));
presenceData.startTimestamp = timestamps[0];
presenceData.endTimestamp = timestamps[1];
```

Wirft 2 `snowflake` Zeitstempel in einem `Array` zurück, die dann für `startTimestamp` und `endTimestamp` verwendet werden können.

### `getTimestamps(Number, Number)`

**Hinweis:** Der gegebene `String` in querySelector ist nur ein Beispiel.

```ts
const video = document.querySelector(".video"),
  timestamps = presence.getTimestamps(video.currentTime, video.duration);
presenceData.startTimestamp = timestamps[0];
presenceData.endTimestamp = timestamps[1];
```

Konvertiert eine Zeichenkette in das Format `HH:MM:SS` oder `MM:SS` oder `SS` in einen Integer (Gibt keinen snowflake Zeitstempel zurück).

### `timestampFromFormat(String)`

**Hinweis:** Der gegebene `String` in querySelector ist nur ein Beispiel.

```ts
const currentTime = presence.timestampFromFormat(document.querySelector(".video-now").textContent),
  duration = presence.timestampFromFormat(document.querySelector(".video-end").textContent),
  timestamps = presence.getTimestamps(currentTime, duration);
presenceData.startTimestamp = timestamps[0];
presenceData.endTimestamp = timestamps[1];
```

Die `PresenceData`-Schnittstelle wird empfohlen, wenn Sie die `SetActivity()` Methode verwenden.

## `PresenceData`-Schnittstelle

Diese Schnittstelle hat folgende Variablen, die alle optional sind.

Dieses Interface hat folgende Variablen, welche alle optional sind.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable</th>
      <th style="text-align:left">Beschreibung</th>
      <th style="text-align:left">Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">details</td>
      <td style="text-align:left">Die erste Zeile in deiner Presence, die normalerweise als Überschrift verwendet wird.</td>
      <td style="text-align:left"><code>String</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">state</td>
      <td style="text-align:left">Zweite Zeile in deiner Presence.</td>
      <td style="text-align:left"><code>String</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">startTimestamp</td>
      <td style="text-align:left">Legt die aktuelle Uhrzeit fest.<br>
        Wird verwendet, wenn du anzeigen möchtest, wie viel <code>Stunden: Minuten: Sekunden</code> übrig sind.
          <br>Du musst deine Zeit in <code>Zeitstempel</code> umwandeln, sonst erhälst du einen falschen Countdown.
      </td>
      <td style="text-align:left"><code>Number</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">endTimestamp</td>
      <td style="text-align:left">Definiert die volle Dauer.
        <br>Wird verwendet, wenn du anzeigen möchtest, wie viel <code>Stunden: Minuten: Sekunden</code> übrig sind.
          <br>Du musst deine Zeit in einen <code>Zeitstempel</code> konvertieren, sonst erhältst du einen falschen Countdown.
      </td>
      <td style="text-align:left"><code>Number</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">largeImageKey</td>
      <td style="text-align:left">Definiert das Logo für die Presence.</td>
      <td style="text-align:left"><code>String</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">smallImageKey</td>
      <td style="text-align:left">Definiert das kleine Symbol neben dem Logo der Anwesenheit&apos;.</td>
      <td style="text-align:left"><code>String</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">smallImageText</td>
      <td style="text-align:left">Definiert den Text, der dem Benutzer angezeigt wird, wenn er mit der Maus über das kleine
        Symbol fährt.</td>
      <td style="text-align:left"><code>String</code>
      </td>
    </tr>
        <tr>
      <td style="text-align:left">buttons</td>
      <td style="text-align:left">Array von Schaltflächen, max. 2, label ist der Schaltflächentext, und url ist der Link.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code>
      </td>
    </tr>
  </tbody>
</table>

```ts
const presenceData: PresenceData = {
  Details: "Mein Titel",
  state: "Meine Beschreibung",
  largeImageKey: "service_logo",
  smallImageKey: "small_service_icon",
  smallImageText: "Du schwebst über mir und was jetzt?" ,
  StartTimestamp: 1564444631188,
  endTimestamp: 1564444634734
};
```

## Events

Events ermöglicht dir, einige Änderungen oder Calls zu erkennen und zu bearbeiten. Du kannst Events mit der Methode `on` abonnieren.

```ts
presence.on("UpdateData", async () => {
  // Tut etwas, wenn Daten aktualisiert werden.
});
```

Dieses Ereignis wird jedes Mal aktualisiert, wenn die Anwesenheit ebenfalls aktualisiert wird.

#### `UpdateData`

Wird ausgelöst, wenn Daten vom iFrame-Skript empfangen werden.

#### `iFrameData`

Wird ausgelöst, wenn Daten vom iFrame-Skript empfangen werden.
