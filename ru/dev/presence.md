---
title: Разработка презенсов
description:
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2020-06-11T18:04:02.843Z
---

> Все презенсы теперь хранятся здесь: https://github.com/PreMiD/Presences 
> 
> {.is-info}

Версия `2.x` представляет [магазин презенсов](https://premid.app/store). Теперь у пользователей есть возможность вручную добавлять и удалять свои любимые презенсы через [сайт](https://premid.app/).

> Прежде чем приступить к работе, настоятельно рекомендуем ознакомиться с нашими руководящими принципами по разработке презенсов. 
> 
> {.is-warning}

- [Рекомендации](https://docs.premid.app/dev/presence/guidelines)
{.links-list}

# Структура

Все презенсы написаны на [TypeScript](https://www.typescriptlang.org/). В отличии от JavaScript [TypeScript](https://www.typescriptlang.org/) имеет несколько дополнительных определений типов, поэтому выявлять и исправлять ошибки намного проще.

## Установка

1. Установите [Git](https://git-scm.com/).
2. Установите [Node](https://nodejs.org/ru/) (идёт вместе с [npm](https://www.npmjs.com/)).
3. Установите [TypeScript](https://www.typescriptlang.org/index.html#download-links) (откройте терминал и введите команду `npm install -g typescript`).

## Клонирование проекта

1. Откройте терминал и введите команду `git clone https://github.com/PreMiD/Presences`.
2. Выберите папку по вашему выбору.
3. Откройте его в редакторе кода.

## Создание папок и файлов

1. Откройте папку `websites`, а затем ту папку, название которой соответствует первой букве **названия** (не ссылки) сервиса, для которого вы собираетесь сделать презенс.
2. Создайте папку, назвав его **названием** (не ссылкой) сервиса, для которого вы собираетесь сделать презенс.
3. Создайте внутри созданной вами папки файлы `presence.ts` и `tsconfig.json`.
4. Теперь создайте папку, назвав его `dist`.
5. Внутри папки `dist` создайте файл `metadata.json`.

## Заполнение файла tsconfig.json

Пожалуйста, поместите следующий код в файл `tsconfig.json`.

```json
{
  "extends": "../../../tsconfig.json",
  "compilerOptions": {
    "outDir": "./dist/"
  }
}
```

Нажмите [сюда](/dev/presence/tsconfig), чтобы узнать больше о настройке TypeScript.

## Заполнение файла metadata.json

Мы сделали [создатель файлов](https://eggsy.xyz/projects/premid/mdcreator) `metadata.json` для ленивых людей. Но вы всё равно рекомендуем прочитать это, чтобы вы знали, как это работает.

```json
{
  "$schema": "https://schemas.premid.app/metadata/1.5",
  "author": {
    "name": "ПОЛЬЗОВАТЕЛЬ",
    "id": "ID"
  },
  "contributors": [
    {
      "name": "ПОЛЬЗОВАТЕЛЬ",
      "id": "ID"
    }
  ],
  "service": "СЕРВИС",
  "altnames": ["СЕРВИС"],
  "description": {
    "en": "ОПИСАНИЕ"
  },
  "url": "ССЫЛКА",
  "version": "ВЕРСИЯ",
  "logo": "ССЫЛКА",
  "thumbnail": "ССЫЛКА",
  "color": "#HEX000",
  "tags": ["ТЕГ1", "ТЕГ2"],
  "category": "КАТЕГОРИЯ",
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
      "title": "ОТОБРАЖАЕМЫЙ ЗАГОЛОВОК",
      "icon": "ЗНАЧОК FONTAWESOME",
      "value": true
    },
    {
      "id": "ID",
      "if": {
        "ID": true
      },
      "title": "ОТОБРАЖАЕМЫЙ ЗАГОЛОВОК",
      "icon": "ЗНАЧОК FONTAWESOME",
      "value": "«%song%» — %artist%",
      "placeholder": "используйте %song% или %artist%"
    },
    {
      "id": "ID",
      "title": "ОТОБРАЖАЕМЫЙ ЗАГОЛОВОК",
      "icon": "ЗНАЧОК FONTAWESOME",
      "value": 0,
      "values": ["1", "2", "и т. д."]
    }
  ]
}
```

Пожалуйста, скопируйте код выше и поместите его в файл `metadata.json`. Теперь нужно изменить значения свойств. Пожалуйста, обратите внимание, что следующие свойства необязательны для использования в метаданных `. son` файл, если вы не планируете его использовать.

- `contributors`
- `altnames`
- `regExp`
- `iframe`
- `iFrameRegExp`
- `readLogs`
- `settings`

**Уточнение некоторых конфигураций значений:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Переменная</th>
      <th style="text-align:left">Описание</th>
      <th style="text-align:left">Тип</th>
      <th style="text-align:left">Опционально</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>author</b></td>
      <td style="text-align:left">Должен содержать Object с <code>name</code> и <code>id</code> участника. <code>name</code> — ваше имя пользователя Discord без идентификатора (#0000). Пользователь <code>id</code> может быть скопирован из Discord, включив разработчик
        режим и правый клик на вашем профиле.</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>Нет</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>contributors</b></td>
      <td style="text-align:left">Должен содержать Object с <code>name</code> и <code>id</code> участника. имя пользователя Discord без идентификатора (#0000). Пользователь <code>id</code> может быть скопирован из Discord, включив разработчик
        режим и правый клик на вашем профиле.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>Да</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>service</b></td>
      <td style="text-align:left">Название службы, поддерживаемой этим присутствием.<br>
      (Должно быть таким же именем, как папка, в которой находится все)</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Нет</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>altnames</b></td>
      <td style="text-align:left">Уметь искать присутствие, используя альтернативное имя.<br>
      Предназначен для использования для присутствий с разными названиями на разных языках. (e.g. Pokémon and 포켓몬스터).<br>
      Вы также можете использовать его для присутствий со специальными символами, поэтому вам не нужно их вводить (e.g. Pokémon and Pokemon).</td>
      <td style="text-align:left"><code>Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Да</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>description</b></td>
      <td style="text-align:left">Небольшое описание присутствия, вы можете использовать описание услуги, если у вас нет идей. Ваше описание должно иметь значения пары ключей, которые указывают на язык, и описание на этом языке. Сделайте описания языков <i>, которые вы знаете</i>, наши переводчики внесут изменения в ваш файл метаданных.</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>Нет</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>url</b></td>
      <td style="text-align:left">URL службы.<br><b>Пример:</b><code>vk. om</code><br>
        <b>Этот URL должен соответствовать URL сайта, так как он определит, является ли это сайт инъекцией скрипта.</b><br> Do <b>NOT</b> add <code>https://</code> или <code>http://</code> внутри URL или слэш в конце:
<code>https://premid. pp/</code> -> <code>premid.app</code><br>
<b>Примечание</b>: Некоторые URL могут иметь <code>www.</code> или что-то еще перед их доменом. Делать <b>не</b> забудьте добавить!<br>
Вы можете добавить несколько URL-адресов, выполнив следующие действия:<br>
<code>["URL1", "URL2", "ETC."]</code><br>
Вы также можете использовать regExp, также известное как Regex, для этой задачи, более подробно объясненное ниже.</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Нет</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>regExp</b></td>
      <td style="text-align:left">Строка регулярного выражения, используемая для сопоставления URL-адресов.<br>
      regExp или также известный как Regex, можно использовать, если веб-сайт имеет несколько поддоменов.<br>
      Для этого вы можете использовать следующий regExp:<br>
      <code>([a-z0-9]+)[.]domain[.]TLD"</code><br>
      TLD standing for Top Level Domain для примера: .com .net (но не вводите точку).<br>
      <code>([a-z0-9]+)</code> означает что угодно от a до z и от 0 до 9.<br>
      Вы можете быстро начать, посмотрев это <a href="https://youtu.be/sXQxhojSdZM">video</a>.<br>
      Вы можете проверить свой regExp на <a href="https://regex101.com/">Regex101</a>.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Да</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>version</b></td>
      <td style="text-align:left">Версия вашего присутствия.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Нет</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>logo</b></td>
      <td style="text-align:left">Ссылка на сервис&apos;с логотипом.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Нет</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>thumbnail</b></td>
      <td style="text-align:left">Ссылка на миниатюру вашего присутствия.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Нет</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>color</b></td>
      <td style="text-align:left"><code>#HEX</code> значение. Мы рекомендуем использовать основной цвет сервиса,
        что ваше присутствие поддерживает.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Нет</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>tags</b></td>
      <td style="text-align:left">Массив меток, они помогут пользователям найти ваше присутствие на сайте.</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Нет</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>category</b></td>
      <td style="text-align:left">Строка, используемая для представления категории присутствия. Смотрите действительные катергории <a href="https://docs. premid. app/dev/presence/metadata#presence-categories">здесь</a>.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Нет</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iframe</b></td>
      <td style="text-align:left">Определяет, используются ли <code>iFrames</code>.</td>
      <td style="text-align:left"><code>Boolean</code></td>
      <td style="text-align:left"><code>Да</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iFrameRegExp</b></td>
      <td style="text-align:left">Регулярный селектор выражений, который выбирает iframes для инъекции. Подробнее см. в regExp.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Да</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>readLogs</b></td>
      <td style="text-align:left">Определяет, должно ли расширение читать журналы.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Да</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>settings</b></td>
      <td style="text-align:left">Массив настроек, которые пользователь может изменить.<br>
      Подробнее о настройках присутствия <a href="https://docs.premid.app/dev/presence/metadata#presence-settings">здесь</a>.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>Да</code></td>
    </tr>
  </tbody>
</table>

## Начало работы

```ts
const presence = new Presence({
  //ID клиента Приложения, созданного по адресу https://discordapp.com/developers/applications
  clientId: "000000000000000000"
  }),
  //Вы можете использовать это для получения переведенных строк на языке браузера
  strings = presence.getStrings({
    play: "presence.playback.playing",
    pause: "presence.playback.paused"
  });

/*
function myOutsideHeavyLiftingFunction(){
    //Захватите и обработайте все свои данные здесь

    // захваты элементов //
    // вызовы api //
    // наборы переменных //
}

setInterval(myOutsideHeavyLiftingFunction, 10000);
//Запускайте функцию отдельно от события UpdateData каждые 10 секунд, чтобы получить и задать переменные, которые собирает UpdateData
*/

presence.on("UpdateData", async () => {
  /*UpdateData всегда срабатывает, и поэтому должен использоваться в качестве цикла обновления или «тика». Это вызывается несколько раз в секунду, когда это возможно.

    Рекомендуется настроить другую функцию вне этой функции событий, которая будет изменять значения переменных и выполнять тяжелую работу, если вы вызываете данные из API.*/

  const presenceData: PresenceData = {
    //Ключ (имя файла) Большого изображения о наличии. Они загружаются и называются в разделе Rich Presence приложения, называемом Art Assets.
    largeImageKey: "key",
    //Ключ (имя файла) Маленького изображения о наличии. Изображения загружены и названы в разделе приложения «Rich Presence», подраздел «Art Assets»*/,
    smallImageText: "Некоторый всплывающий текст", //Текст, который будет показан при наведении на маленькое изображение
    details: "Название просматриваемой страницы", //Заголовок презенса
    state: "Прочитываемый раздел А", //Описание презенса
    startTimestamp: 1577232000, //Временная метка в формате unix, начиная с которой будет отчитываться время в презенсе
    endTimestamp: 1577151472000 //Если вы хотите указать сколько времени осталось, вместо того, чтобы указывать сколько времени прошло, то укажите здесь временную метку в формате unix в которое время будет конец отчёта.
  }; /*Если хотите, вы можете не устанавливать значение для largeImageKey и изменять остальные параметры как подсвойства, например, presenceData.type = "бла-бла-бла"; примеры типов: details, state и т. п.*/

  if (!presenceData.details) presence.setActivity(); /*Обновляет презенс без данных, то есть очищает его и устанавливает больше изображение как иконка приложения и всплывающий текст как название приложения*/
  else presence.setActivity(presenceData); //Обновляет презенс используя значения из объекта presenceData
});
  };
  //Обновите сведения о присутствии всеми значениями из объекта presenceData, если (presenceData.details) presence.setActivity(presenceData);
  //Обновите присутствие без данных, очислив его и сделав большое изображение значком приложения Discord, а текст — именем приложения Discord.
  else presence.setActivity(); 
});
```

Вы можете скопировать это в свой `presence.ts` файл и редактирование значений. Установка всех значений выполняется внутри события updataData.

Для примеров, мы предлагаем ознакомиться с кодом присутствия: 1337x или 9GAG. Для получения дополнительной информации о классе `Presence` нажмите [здесь](/dev/presence/class).

Начиная с версии 2.2. есть слайд-шоу, это позволяет показать несколько интерфейсов `PresenceData` на интервале, для получения дополнительной информации нажмите на `Слайд-шоу` класс [здесь](/dev/presence/slideshow).

## Не удается получить определенные данные?!

Многие веб-сайты используют [iframes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) ([Inlineframes](https://en.wikipedia.org/wiki/HTML_element#Frames)). Эти html-теги могут содержать несколько источников, таких как видео. Но они не актуальны каждый раз. Некоторые из них скрыты или просто не используются активно. Проверьте, можете ли вы извлечь необходимую информацию без них, прежде чем выполнять ненужную работу.

1. Проверить их в консоли браузера (убедитесь, что вы находитесь на вкладке **Элементы**).
2. Поиск (<kbd>CTRL</kbd>+<kbd>F</kbd> (Windows) или <kbd>CMD</kbd>+<kbd>F</kbd> (MacOS)).
3. Выполнить `document.querySelectorAll("iframe")`.

Если вы обнаружили, что ваши данные находятся в iFrame вам необходимо сделать следующее:

1. Создайте файл `iframe.ts`.
2. Установите iFrame в `true` в вашем файле метаданных.
3. Заполнение файла iFrame.

```ts
const iframe = new iFrame();
iframe.on("UpdateData", async () => {
  //Получите все необходимые данные из iFrame, сохраните их в переменные, а затем отправьте их используя iframe.send
  iframe.send({
    //отправка данных
    video: video,
    time: video.duration
  });
});
```

4. Создание файла присутствия позволяет получать данные из файла iFrame .

```ts
presence.on("iFrameData", (данные) => {
  iFrameVideo = data.video;
  currentTime = data.time;
});
```

**Примечание** Это должно быть помещено вне события updateData.

## Компиляция

Откройте консоль в своей папке и введите `tsc -w` to compile the `presence.ts` в `/dist` папка.

# Загрузка присутствия

1. Откройте всплывающее окно расширения в браузере и удерживайте кнопку <kbd>Shift</kbd> на вашей клавиатуре.
2. **Load Presence** появится в секции Prestions.
3. Нажмите на неё, пока вы все еще держите кнопку <kbd>Shift</kbd>.
4. Выберите папку /dist вашего присутствия.

# Полезные советы

## Горячая загрузка

Веб-сайт, на котором вы находитесь, автоматически перезагружается каждый раз, когда вы сохраняете файл в вашей папке.

## Отладка

- Вы можете поместить `console.log("Тест");` между вашим кодом и посмотреть, выводит ли консоль вашего браузера. Если да, то войдите и повторите попытку после следующей функции. Если нет, то произошла ошибка выше.
- Если это тоже не поможет вам, то наш [Сервер Discord](https://discord.premid.app/) Для помощи.

# Файлы разъяснены

- [Класс Состояния](/dev/presence/class)
- [Класс слайд-шоу](/dev/presence/slideshow)
- [класс iFrame](/dev/presence/iframe)
- [Файл Метаданных](/dev/presence/metadata)
- [Настройка TypeScript](/dev/presence/tsconfig ""){.links-list}
