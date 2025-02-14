---
title: Clase Presence
description: La clase principal para cada presence de PreMiD
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2021-09-07T01:44:50.164Z
---

# Clase Presence

## Introducción

La clase `Presence` es útil dado que contiene métodos básicos para construir una presence.

Cuando creas una clase has de especificar apropiadamente el campo `clientId`.

```ts
const presence = new Presence({
  clientId: "514271496134389561" // clientId de ejemplo
});
```

### Propiedades

Hay tres propiedades disponibles para la clase `Presence`.

#### `clientId`

Esta propiedad es necesaria para que funcione, ya que utiliza el id de aplicación para mostrar su logotipo entre otras imágenes. Puedes obtenerlo en tu [página de aplicaciones](https://discordapp.com/developers/applications).

#### `injectOnComplete` - *Obsoleto desde 2.2.4*

Al configurar `injectOnComplete` a `true` el primer evento `UpdateData` se lanzará, en ambos archivos `presence.ts` y `iframe.ts`, una vez haya terminado de cargar completamente la página.

#### `appMode` - *Obsoleto desde 2.2.4*

Al establecer `appMode` a `true` si la presence enviara un `PresenceData` vacío, la app mostrará la imagen y nombre de la aplicación en el perfil del usuario.

## Métodos

### `getActivity()`

Devuelve un objeto `PresenceData` con los datos que se están mostrando en la presence.

### `setActivity(PresenceData | Slideshow, Boolean)`

Establece la actividad de tu perfil de acuerdo a los datos proporcionados.

El primer parámetro requiere una interfaz [`PresenceData`](#presencedata-interface) o una clase [`Slideshow`](/dev/presence/slideshow) para obtener toda la información que deseas mostrar en tu perfil.

El segundo parámetro indica si la presence está reproduciendo algo o no. Utiliza siempre `true` si proporcionas marcas de tiempo (timestamps) en `PresenceData`.

### `clearActivity()`

Elimina la actividad actual y el titulo de la bandeja de trabajo.

### `setTrayTitle(String)` - *Obsoleto desde 2.2.3*

> Este método funciona sólo en Mac OS. 
> 
> {.is-warning}

Establece el título de la bandeja en la barra de menús.

### `createSlideshow()`

Crea una nueva instancia de la clase `Slideshow`.

```ts
const slideshow = presence.createSlideshow();
```

Se sugiere hacer esto al instanciar la clase `Presence`:

```ts
const presence = new Presence({
    clientId: "514271496134389561" // clientId de ejemplo
  }),
  slideshow = presence.createSlideshow();
```

Puedes encontrar la documentación para la clase `Slideshow` [aquí](/dev/presence/slideshow).

### `getStrings(Object)`

Un método asíncrono que te permite obtener strings traducidas de la extensión.

Debes proporcionar un `Object` donde las claves son la clave del string, `valorClave` es el valor del string. Puedes encontrar una lista de strings traducidas aquí: `https://api.premid.app/v2/langFile/presence/en/`

```ts
// Devuelve las strings `Playing` y `Paused`
// desde la extensión.
const strings = await presence.getStrings({
  reproduciendo: "general.playing",
  pausado: "general.paused"
}, "en");

const playString = strings.reproduciendo; // resultato: Playing
const pauseString = strings.pausado; // resultado: Paused
```

Desde la versión 2.2.0 de la extensión ahora puedes obtener strings dado un idioma. Esto funciona bien en conjunto de la configuración `multiLanguage` recientemente añadida.

Sugerimos que utilices el siguiente código para que se actualice automáticamente PresenceData si el usuario cambia el idioma;

```ts
async function getStrings() {
  return presence.getStrings(
    {
      play: "general.playing",
      pause: "general.paused"
    },
    // El ID es el ID de la configuración multiLanguage.
    await presence.getSetting("ID").catch(() => "en");
  );
}

let strings = getStrings(),
  // El ID es el ID de la configuración multiLanguage.
  oldLang: string = await presence.getSetting("ID").catch(() => "en");

//! ¡El siguiente código debe estar dentro del evento updateData!
// The ID is the ID of the multiLanguage setting.
const newLang = await presence.getSetting("ID").catch(() => "en");
if (oldLang !== newLang) {
  oldLang = newLang;
  strings = getStrings();
}

const playString = (await strings).play, // resultado: Playing
  pauseString = (await strings).pause; // resultado: Paused
```

### `getPageletiable(String)`

Devuelve una variable desde el sitio web si existe.

**Advertencia: Esta función puede causar un alto uso de CPU y retraso en el sitio cuando se ha ejecutado demasiadas veces.**

```ts
const pageVar = getPageletiable(".pageVar");
console.log(pageVar); // Esto mostrará en la consola "Contenido de la variable"
```

### `getExtensionVersion(Boolean)`

Devuelve la versión de la extensión que está usando el usuario.

```ts
getExtensionVersion(onlyNumeric?: boolean): string | number;

const numeric = presence.getExtensionVersion();
console.log(numeric); // Mostrará 210
const version = presence.getExtensionVersion(false);
console.log(version); // Mostrará 2.1.0
```

### `getSetting(String)`

Obtén el valor del ajuste.

```ts
const setting = await presence.getSetting("pdexID"); // Remplaza pdexID con el id del ajuste
console.log(setting); // Esto mostrará el valor del ajuste
```

### `hideSetting(String)`

Oculta el ajuste indicado.

```ts
presence.hideSetting("pdexID"); // Reemplaza pdexID con el ID de la configuración
```

### `showSetting(String)`

Muestra el ajuste indicado (solo funciona si el ajuste ha sido ocultado).

```ts
presence.showSetting("pdexID"); // Reemplaza pdexID con el ID de la configuración
```

### `getLogs()`

Devuelve los logs de la consola del sitio web.

```ts
const logs = await presence.getLogs();
console.log(logs); // Obtienes los últimos 100 logs (en un array).
```

**Nota:** Requiere establecer la propiedad `readLogs` a `true` en el archivo `metadata.json`.

### `info(String)`

Muestra el mensaje proporcionado en la consola en un formato basado en la presence bajo el estilo `info`.

```ts
presence.info("Test") // Esto logeará "test" con un estilo predeterminado.
```

### `success(String)`

Muestra el mensaje proporcionado en la consola en un formato basado en la presence bajo el estilo `satisfactorio`.

```ts
presence.success("Test") // Esto logeará "test" con un estilo predeterminado.
```

### `error(String)`

Muestra el mensaje proporcionado en la consola en un formato basado en la presence bajo el estilo `error`.

```ts
presence.error("Test") // Esto logeará "test" con un estilo predeterminado.
```

### `getTimestampsfromMedia(HTMLMediaElement)`

Devuelve 2 marcas de tiempo (timestamps) en un `array` que puede ser usado para `startTimestamp` y `endTimestamp`.

```ts
const timestamps = presence.getTimestampsfromMedia(document.querySelector(".video"));
presenceData.startTimestamp = timestamps[0];
presenceData.endTimestamp = timestamps[1];
```

**Nota:** El `String` dado en querySelector es un ejemplo.

### `getTimestamps(Number, Number)`

Devuelve 2 marcas de tiempo (timestamps) en un `array` que puede ser usado para `startTimestamp` y `endTimestamp`.

```ts
const video = document.querySelector(".video"),
  timestamps = presence.getTimestamps(video.currentTime, video.duration);
presenceData.startTimestamp = timestamps[0];
presenceData.endTimestamp = timestamps[1];
```

**Nota:** El `String` dado en querySelector es un ejemplo.

### `timestampFromFormat(String)`

Convierte una cadena con formato `HH:MM:SS` o `MM:SS` o `SS` en un entero (no devuelve un timestamp).

```ts
const currentTime = presence.timestampFromFormat(document.querySelector(".video-now").textContent),
  duration = presence.timestampFromFormat(document.querySelector(".video-end").textContent),
  timestamps = presence.getTimestamps(currentTime, duration);
presenceData.startTimestamp = timestamps[0];
presenceData.endTimestamp = timestamps[1];
```

**Nota:** El `String` dado en querySelector es un ejemplo.

## Interfaz `PresenceData`

Se recomienda utilizar la interfaz `PresenceData` cuando se está utilizando el método `setActivity()`.

Esta interfaz tiene las siguientes variables, todas ellas son opcionales.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Variable</th>
      <th style="text-align:left">Descripción</th>
      <th style="text-align:left">Tipo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">details</td>
      <td style="text-align:left">La primera línea en la presence, generalmente usada como cabecera.</td>
      <td style="text-align:left"><code>String</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">state</td>
      <td style="text-align:left">Segunda línea en la presence.</td>
      <td style="text-align:left"><code>String</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">startTimestamp</td>
      <td style="text-align:left">Define la hora actual.<br>
        Utilizado si quieres mostrar cuántas <code>horas:minutos:segundos</code> quedan.
          <br>Debes convertir tu tiempo a <code>timestamps</code> u obtendrás una cuenta atrás
          incorrecta.
      </td>
      <td style="text-align:left"><code>Number</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">endTimestamp</td>
      <td style="text-align:left">Define la duración completa.
        <br>Utilizado si deseas mostrar cuantas <code>horas:minutos:segundos</code> quedan.
          <br>Debes convertir la marca de tiempo a <code>timestamp</code> u obtendrás una cuenta atrás errónea.
      </td>
      <td style="text-align:left"><code>Number</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">largeImageKey</td>
      <td style="text-align:left">Define el logotipo de la presence.</td>
      <td style="text-align:left"><code>String</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">smallImageKey</td>
      <td style="text-align:left">Define el icono pequeño junto al logo de la presence.</td>
      <td style="text-align:left"><code>String</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">smallImageText</td>
      <td style="text-align:left">Define el texto que se mostrará al usuario al pasar el cursor sobre el icono 
        pequeño.</td>
      <td style="text-align:left"><code>String</code>
      </td>
    </tr>
        <tr>
      <td style="text-align:left">buttons</td>
      <td style="text-align:left">Array de botones, máximo 2, label es el texto del botón y url el enlace.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code>
      </td>
    </tr>
  </tbody>
</table>

```ts
const presenceData: PresenceData = {
  details: "Mi título",
  state: "Mi descripción",
  largeImageKey: "logo_servicio",
  smallImageKey: "icono_servicio_pequño",
  smallImageText: "Has puesto el cursor sobre mí, ¿ahora que?",
  startTimestamp: 1564444631188,
  endTimestamp: 1564444634734
  buttons: [
    {
            label: "Botón de prueba1",
            url: "https://premid.app/"
        },
        {
            label: "Botón de prueba2",
            url: "https://premid.app/contributors"
        }
    ]
};
```

## Eventos

Los eventos te permiten detectar y manejar algunos cambios o llamadas realizadas. Puedes suscribirte a eventos usando el método `on`.

```ts
presence.on("UpdateData", async () => {
  // Haz algo cuando se actualicen los datos.
});
```

Hay algunos eventos disponibles:

#### `UpdateData`

Este evento es lanzado cada vez que la presence es actualizada.

#### `iFrameData`

Lanzado cuando se obtienen datos del script iFrame.
