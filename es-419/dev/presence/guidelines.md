---
title: Reglas de las Presence
description: Reglas que todos los desarrolladores de presences deben seguir para que su presence sea añadida.
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2021-09-07T01:44:53.883Z
---

<div align="center">
    <img src="https://github.com/PreMiD.png?size=2048" width="128px" style="max-width:100%;">
    <h3 style="font-size: 2rem; margin-bottom: 0">Reglas de las presence</h3>
    <h4 style="margin-top: 0">Revisión 3</h4>
    <br />
</div>

# Directrices

Al publicar Presences en [nuestro repositorio de GitHub](https://github.com/PreMiD/Presences), necesitamos que sigas un conjunto de reglas. Para algunos, estás reglas pueden parecer estrictas. Sin embargo, la implementación de estos conjuntos de reglas nos impedirá a nosotros y a los usuarios encontrarse con cualquier problema.

# Creación

Las reglas generales del desarrollo de una presence son las siguientes:

- Las presences **deben** estar relacionadas con el sitio web que has elegido.
- Las presences **no pueden** ser para sitios ilegales. (Por ejemplo: Stressors, marketing de drogas, pornografía infantil, etc.)
- La estructura de los archivos debe ser limpia y gestionada, no incluyas archivos que no estén especificados. (Por ejemplo: Vscode y capetas git, imágenes y archivos de texto, etc.)
- Necesitas tener una estructura de archivo adecuada, los borradores **no** están permitidos.
- Presences para sitios web con TLDs (dominios de nivel superior) `.onion` o sitios web con dominios/hosts gratuitos (por ejemplo, `.TK` [todos los dominios Freenom gratuitos], `.RF`, `GD`, etc.) ** no ** están permitidos, se pueden hacer excepciones si se presentan pruebas de que se ha pagado por el dominio.
- El dominio de la presence debe tener al menos una antigüedad de 2 meses.
- Presences que tienen como destino páginas internas del navegador (como Chrome Web Store, `chrome://`, páginas `about:`, etc.) **no** están permitidas ya que requieren que se habilite una configuración experimental en el lado del usuario y podría causar daños al navegador.
- Las presences con soporte para un solo subdominio **no** se permitirán, ya que pueden parecer rotas para otras páginas (como la página de inicio), se pueden hacer excepciones para la política y las paginas de contacto (contenido que no se usa con frecuencia) o sitios donde el otro contenido no este relacionado. (por ejemplo, páginas de wikia)
- Las presences para radios en línea sólo están permitidas si la radio tiene al menos 100 oyentes semanales y 15 simultáneos. Además de esto debe tener alguna características extra aparte de mostrar el título del álbum/canción, etc.
- No se permite a las Presences ejecutar código JS con su propia función para obtener variables. Si Firefox tiene problemas con la función integrada dentro de la clase `Presence`, tienes permitido implementar tu propia función. En cuyo caso tendrás que indicarlo en la descripción del Pull Request.
- **No** se permiten presences de baja calidad o que tengan poco contexto (p. ejemplo., mostrar solo un logotipo y texto pero nunca volver a cambiarlo).
- Presences para servicios como listas de bots/servidores de Discord deben seguir estos requisitos adicionales:
  - El dominio debe tener al menos **6 meses** de antigüedad.
  - Visitantes únicos por día:
    - For 6 to 12 month old domains: **20,000 unique visitors/day**.
    - Para dominios de 12 o más meses de antigüedad: **45.000 visitas únicas por día**.
  - El sitio web no puede estar en un dominio barato como `.xyz` o `.club`.
  - El sitio web debe tener una muy buena calidad, diseño, etc.
- Las presences deben utilizar [detalles comunes](https://api.premid.app/v2/langFile/presence/en) (strings que empiezan por "general."). Puedes conseguirlo usando `multilenguaje` con las strings proporcionadas. Si tu presence requiere cadenas de texto personalizadas, entonces no deberías usar `multiLanguage` hasta que la presence reciba 1000 usuarios. Puedes encontrar un ejemplo [aquí](https://docs.premid.app/dev/presence/class#getstringsobject).
- Incluyendo la carpeta `dist`, los archivos `presence.ts`, `iframe.ts` y `metadata.json` son obligatorios. Obteniendo algo como el siguiente esquema:

```bash
presence
├── dist
│   └── metadata.json
├── presence.ts
└── tsconfig.json
```

o si estas usando un archivo `iframe.ts`:

```bash
presence
├── dist
│   └── metadata.json
├── presence.ts
├── iframe.ts
└── tsconfig.json
```

## [**metadata.json**](https://docs.premid.app/dev/presence/metadata)

> Para la conveniencia de nuestros desarrolladores de presences, hemos proporcionado un esquema que puedes usar para validar la integridad de tu archivo `metadata`. Esto es completamente opcional y no es requerido durante el proceso de revisión.

> Es altamente recomendado que organices tu archivo `metadata` en el formato mostrado abajo, y debes tener nombres de servicio, descripciones, etiquetas y campos de ajustes gramaticalmente correctos. Cualquier cosa que no esté organizada según las especificaciones, **no** será permitida.

> Presences de sitios web que tienen contenido explícito **deben** tener la etiqueta `nsfw` y el logo y etiqueta **no** deben contener contenido explícito.

Cada presence tiene un archivo para describirla llamado `metadata.json`, el metadata tiene un estándar estricto y un ejemplo de este archivo se puede ver abajo:

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
      "id": "multiLanguage",
      "multiLanguage": true
    }
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

> Si un campo está estipulado como opcional en la [documentación](https://docs.premid.app/en/dev/presence/metadata) o está marcado con un `*` al lado de la clave y tu presence usa el valor por defecto para ella, no la incluyas en el archivo `metadata`. (por ejemplo, una presence sin soporte para iframe no debe contener el campo `iframe`.)

> Todas las imágenes en el archivo de `metadata` deben estar alojadas en `i.imgur.com`. Usar contenido alojado en el sitio web **no** está permitido, ya que pueden cambiar su ubicación sin querer.

Una lista de los campos y sus reglas están listadas abajo:

### **`$schema`**

- La _llave_ del esquema **debe** incluir un signo de dolar al inicio, esto indicará a su editor de texto que tu quieres validar tu archivo JSON contra un modelo. _Tal y como se ha dicho anteriormente, no necesitas incluir un esquema, pero en caso de que lo hagas, debes tomar esto en cuenta._

### **`author`**

- El _valor_ del ID **debe** ser el snowflake de tu ID de Discord. Puedes obtenerlo activando el [modo de desarrollador](https://support.discord.com/hc/es/articles/206346498-Where-can-I-find-my-User-Server-Message-ID-). _Por favor **no** confundas esto con la ID de la aplicación, la cual es solo para tu presence._

### **`*contributors`**

- **No** te agregues ni a ti, ni a nadie más como contribuidores al menos que hayan ayudado con la presence.

### **`service`**

- El nombre del servicio **debe** ser el nombre del directorio de la presence. Por ejemplo, si la presence esta ubicada en `/websites/Y/YouTube/`, el nombre del servicio debe ser `YouTube`.
- **No puedes** usar la url como el nombre del servicio al menos que el sitio web use la url como su nombre oficial. Si el nombre no es descriptivo y puede ser considerado impreciso, usar la url es **requerido**. (Por ejemplo: `YouTube` es permitido porque este es el nombre oficial y es descriptivo, mientras que `youtube.com` no lo es. `Top` es un nombre no descriptivo, así que usar la url `top.gg` es **requerido**.)
- Si el servicio contiene algunas reglas explicitas en su nombre, usted debe seguirlas.

### **`*altnames`**

- Usa esto **solo** en el caso de que el sitio web aparezca bajo distintos nombres (ejemplo. Versiones *acortadas* del servicio aparecerán como `etiquetas`.

### **`description`**

- **Todas** las presences **requieren** una descripción en Inglés sin importar el idioma preferido del sitio web.
- **No** intentes traducir la descripción por tu cuenta a menos que conozcas el idioma, traductores modificaran tu `metadata.json.` y cambiaran la descripción de ser necesario.

### **`url`**

- La url **debe** ser un "string" si el sitio web solo usa un dominio. Si el sitio web usa múltiples, usa un array y especifica cada una.
- **No** incluyas protocolos en la url (por ejemplo.`http` o `https`, y no incluyas parámetros "query" en la url (por ej.,`www.google.com/search?gws_rd=ssl` debería ser `www.google.com`)

### **`version`**

- Asegúrate de que el número de versión sigue [los estándares semánticos de versionado](https://semver.org/lang/es/), que se traducen al siguiente esquema: `<NUEVA-CARACTERISTICA>.<SOLUCION-DE-MULTIPLES-BUGS>.<SOLUCION-DE-PEQUEÑOS-BUGS-O-CAMBIOS-EN-METADATA>`. Cualquier cosa como `1.0.0.1`, `1.0`, `1`, `1.0.0-BETA` o cambiando `1.0.0` a `2.0.0` en una corrección de errores/cambio pequeño **no** está permitido.
- La versión **debe** empezar siempre con `1.0.0` a menos que se diga lo contrario, otras versiones **no** serán permitidas.

### **`logo`**

- El logo **debe** ser una imagen cuadrada con una relación de aspecto `1:1`.
- La imagen **requiere** una resolución mínima de `512x512` píxeles. Puedes aumentar el tamaño de la imagen usando una herramienta como [waifu2x](http://waifu2x.udp.jp/).

### **`thumbnail`**

- La miniatura **debería** ser preferiblemente una [tarjeta promocional amplia](https://i.imgur.com/3QfIc5v.jpg) o una [captura de pantalla](https://i.imgur.com/OAcBmwW.png) si la primera **no** está disponible.

### **`color`**

- El color **debe** ser un valor hexadecimal entre `#000000` y `#FFFFFF`.
- La cadena de color **debe** estar precedida con un numeral (#).

### **`tags`**

- **Todas** las presences requieren por lo menos _una_ etiqueta.
- Las etiquetas **no** deben tener espacios, slash, comillas simples o dobles, caracteres Unicode y siempre deberían ser en minúscula.
- Las etiquetas **deberían** incluir preferiblemente nombres de servicio alternativos para hacer su búsqueda mas fácil ( por ejemplo, si una presencia Amazon hubiese incluido soporte para AWS, debería tener sus etiquetas como `amazon-web-services` y `aws`)
- Estás **obligado** a añadir una etiqueta `NSFW` si la presence es para un sitio web con contenido para adultos.

### **`category`**

- La categoría **debe ser una de las siguientes que aparecen en la [documentación](https://docs.premid.app/dev/presence/metadata#presence-categories).</li>
- La presence debe utilizar una categoría que coincida con el contenido del sitio web. (por ejemplo, no utilices `anime` cuando el sitio web no esté relacionado con anime).</ul>

### **`*regExp`** <br /> **`*iFrameRegExp`**

- Las expresiones regulares **deben** ser válidas. Por favor prueba tus expresiones con las herramientas listadas en la [documentación](https://docs.premid.app/dev/presence/metadata#testing).

### **`readLogs`**

- Debe ser un valor `boolean` (por ejemplo `true` o `false`).
- Habilite los registros de su presencia.

### **`warning`**

- Habilita un icono de advertencia indicando al usuario que la presence requiere de pasos adicionales además de añadirla.
- Una presence de ejemplo usando esta variable de metadata es `VLC`.

### **`settings`**

- Si decides formatear un string (por ejemplo., `%song% por%artist%`), debes rodear las variables por símbolos de porcentaje en cada lado. Variables como `%var`, `var%`, `%%var%%` o cualquier cosa intermedia **no** está permitido por el bien de la estandarización.
- El nombre de la configuración **no** debe estar completamente en mayúsculas. Por ejemplo, nombre como `MOSTRAR ESTADO` **no** serán permitidos. En cambio nombre como `Mostrar Estado` o `Mostrar estado` sí están permitidos.
- Si estás usando la opción `multiLanguage` deberías saber:
  - Un valor de tipo **boolean** habilitará sólo strings de [`general.json`](https://github.com/PreMiD/Localization/blob/master/src/Presence/general.json) del repositorio de Localization o del archivo de la presence (por ejemplo. cuando el nombre de la presence es YouTube, la extensión obtendrá también valores de `youtube.json`)
  - Un valor de tipo **string** (por ejemplo. `youtube`) especifica el nombre del archivo del cual se obtendrán los strings.
  - Un valor de tipo **Array<String>** (por ejemplo. `["youtube", "discord"`) especifica los nombres de los archivos de los cuales obtener los strings.

## [**presence.ts**](https://docs.premid.app/dev/presence/class)

> El código que escribas **debe** estar _bien escrito_ y **debe** ser _entendible_ y todas las palabras deben ser gramaticalmente correctas (errores gramaticales de páginas webs pueden ser ignoradas).

> Cada presence sigue un estricto conjunto de reglas de linting que serán comprobadas durante el proceso de revisión. Un par de recomendaciones pueden ser vistas a continuación. - [Recomendaciones de plugins de TypeScript para verificaciones "Strict Type Checking"](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/eslint-plugin/docs/rules) - [recomendaciones de ESlint](https://eslint.org/docs/rules) [Recomendaciones de ESlint](https://eslint.org/docs/rules). [Recomendaciones de ESlint](https://eslint.org/docs/rules). [Prettier (formateo de código)](https://prettier.io/).

Aquí hay una lista de reglas que debes seguir al escribir tu archivo `presence.ts`:

- **Siempre** declare una nueva instancia de la clase `Presence` antes de cualquier otra variable para evitar problemas raros que puedan ocurrir; no es un requisito por diseño, podría ser ser eliminado en el futuro.
- **Nunca** utilices funciones personalizadas cuando [variantes nativas estén disponibles](https://docs.premid.app/dev/presence#files-explained); esto asegura que las correcciones en el nivel de extensión también se aplican a tus presences. Eres libre de usar lo que sea que necesites, si no lo encuentras listado en la documentación.
- Está **prohibido** codificar las presences de un sitio sin agregar soporte a su idioma principal(ejemplo., una presence de YouTube codificada con soporte solo para portugués y japonés, pero no inglés en sí.)
- Los campos `smallImageKey` y `smallImageText` están destinados a proporcionar contexto adicional/secundario (como `reproduciendo/pausado` para sitios de streaming, `navegando` para sitios normales, y otros casos) no para promover perfiles de Discord ni nada que no esté relacionado con PreMiD.
- **No** estás autorizado para acceder a `localStorage`.
- Al acceder a las cookies de los datos almacenados, por favor prefije la clave con `PMD_`.
- Solo podrás hacer peticiones HTTP/HTTPS a `premid.app` o el sitio para API de su presence. Si está utilizando dominios externos, tendrá que explicar por qué son necesarios. Únicamente la API permitida para realizar solicitudes es [`Obtener API`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).
- **No** establezcas campos de la instancia presenceData como undefined una vez declarado, utiliza en su lugar la palabra clave `delete`. (por ejemplo, usa `delete data.startTimestamp` en vez de `data.startTimestamp = undefined`)
- **No** tienes permitido escribir presences que puedan cambiar la funcionalidad de un sitio web. Esto incluye la adición, eliminación o modificación de los elementos DOM.
- Presences que utilizan botones deben seguir estos requisitos adicionales:
  - Los redireccionamientos a la página principal están prohibidos.
  - No está permitido promover sitios web por medio de ello.
  - They can't display information you couldn't fit in other fields.
  - Está prohibida la redirección directa a streams de audio o vídeo.


## [**tsconfig.json**](https://docs.premid.app/dev/presence/tsconfig)

> **No** escribas tu propio `tsconfig.json`, usa el proporcionado en la [documentación](https://docs.premid.app/en/dev/presence/tsconfig).

## Modificación

> **Debes** cambiar la versión en **metadata.json** a un valor mayor de la versión anterior cuando hagas cambios en los archivos **presence.ts**, **iframe.ts** o**metadata.json**.

En algunas situaciones, las presences pueden comportarse inesperadamente o podrían realizar cambios menores para mejorar su funcionalidad. Aquí hay una lista de situaciones que **debes** tener en cuenta al modificar presences.

- If the presence author hasn't been contactable in over a month, you may contact a reviewer to see if you can modify the presence.
- Si haces modificaciones a una presence que afecte a al menos a un **un cuarto** del código base de la misma, tienes permitido añadirte como colaborador. Contacta a un verificador para más información sobre este tema.
- Anyone may create PRs to fix bugs. Do **not** change images if they are not outdated and are in specifications.

# Verificación

> **Todo** código contribuido será bajo la licencia `Mozilla Public License 2.0`.

> Si necesitas contactar con alguien, por favor usa nuestro servidor oficial de Discord. Todas los verificadores tiene el rol de `Reviewer` en su perfil.

> Por favor ten en cuenta que el trabajo de los verificadores es voluntario y gestionan otros repositorios además de este, tu pull request puede no ser revisada hasta horas o días después de haber sido creada.

> Ten **siempre** un fork actualizado antes de crear el pull request. Esto facilitará falsos positivos de los chequeos.

El proceso más importante de desarrollo de una presence es publicarla en la tienda. Esto se hace haciendo un [pull request](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request) en GitHub en el repositorio `PreMiD/Presences`. Nuestros verificadores confirmaran que tu presence cumple los estándares y será añadida en la tienda.

<div>
  <h2 style="font-size: 2rem; margin-bottom: 0;">Verificadores de Presences</h2>
  <a href="https://github.com/Bas950"><img src="https://github.com/Bas950.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a> <a href="https://github.com/Slowlife01"><img src="https://github.com/Slowlife01.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a> <a href="https://github.com/EncryptedDev"><img src="https://github.com/EncryptedDev.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
  <br />
</div>

## `Revisiones`

No te será permitido crear presences en en caso de ofensas repetitivas como romper las indicaciones, spamming de pull requests, amenazas o comportamiento inapropiado.

En este escenario, se producirán los siguientes cambios:

- Las presences bajo su gestión se transferirán al bot de PreMiD u otro usuario (decisión del verificador). La Id de la aplicación para cada presence se volverá a crear con el nombre del nuevo dueño.
- Todos tus issues y pull request (Creacion y contribucion de presences) creados luego del ban seran cerrados.
- Tickets creados bajo tu nombre con respecto al desarrollo de presences serán eliminados.

## `Revisiones`

Algunas cosas que deberías saber después de abrir una solicitud de pull request:

- Se necesitan 2 revisores para hacer un merge a un pull request.
- Si un pull request está incativo en un periodo de 7 días, será cerrado inmediatamente.
- Todas las revisiones **deben** pasar para ejecutar el merge.
- ⚠️**Debes** proporcionar nuevas capturas de pantalla sin alterar (tomadas por ti) mostrando una comparación lado a lado de tu perfil y el sitio web para demostrar que tu presence funciona. _Se le permite usar capturas de pantalla por placer visual_ Esto se aplica tanto a la creación como a la modificación.
- ⚠ También es **requerido** incluir capturas de pantalla de la configuración de la presence en la extensión si se proporciona. Se puede ver un ejemplo [aquí](https://imgur.com/a/OD3sj5R).

## `Verificaciones`

![Ejemplo de cambios](https://i.imgur.com/vF7QpBH.png)

Actualmente, una presence pasa por 2 etapas separadas de comprobaciones. Todas estas comprobaciones ayudan a que los verificadores determinen si su presence es adecuada para su implementación.

- `DeepScan` is a bot that checks for code quality. Si alguna vez recibes errores **debes** corregirlos. *Warning: DeepScan doesn't always give you errors. Por favor, mire las advertencias del CodeFactor en su lugar.*
- `CodeFactor` es un bot que comprueba la calidad del código. Si alguna vez recibes errores **debes** corregirlos.
- `Schema Validation` escaneará su archivo `metadata.json` en busca de cualquier error (por ejemplo, campos faltantes, tipos de valores no válidos, etc.). Si alguna vez recibes errores de nuevos problemas, **debes** corregirlos. Añadir un campo schema al archivo `metadata.json` permitirá a tu editor de texto (si es compatible) mostrar estos errores durante el desarrollo.

## `Reglas Adicionales`

- **Siempre** asegúrese de iniciar su presence en la carpeta más apropiada, si su nombre comienza con _cualquier_ letra latina entonces debe estar bajo su coincidencia alfabética (por ejemplo. `D/dアニメストア` o `G/Google`). Cualquier otro carácter Unicode/no latino **debe** estar bajo la carpeta `#` (por ejemplo, `#/巴哈姆特.`) y números bajo la carpeta `0-9` (por ejemplo, `0-9/4anime`).

Después de cumplir con todas las directrices, revisiones y comprobaciones adecuadas, su presence será añadida.

# Sugerencias

La `revisión 2` de las indicaciones fueron escritas y contribuidas por los siguientes individuos:

# Contribuidores

La `revisión 1` fue mantenida por los siguientes individuos:

<div>
<a href="https://github.com/PreMiD"><img src="https://github.com/PreMiD.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
</div>

La `revisión 2` de las indicaciones fueron escritas y contribuidas por los siguientes individuos:

<div>
<a href="https://github.com/CobyPowers"><img src="https://github.com/CobyPowers.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
</div>

`Revision 1` fue mantenido por los siguientes individuos:

<div>
<a href="https://github.com/CobyPowers"><img src="https://github.com/CobyPowers.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
<a href="https://github.com/Bas950"><img src="https://github.com/Bas950.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
<a href="https://github.com/i1u5"><img src="https://github.com/i1u5.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
</div>
