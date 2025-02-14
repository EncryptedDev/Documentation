---
title: プレゼンスの開発
description:
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2020-06-11T18:04:02.843Z
---

> すべてのプレゼンスはここに保管されています。 https://github.com/PreMiD/Presences 
> 
> {.is-info}

Version `2.x` introduces the [presence store](https://premid.app/store). Users now have the ability to manually add and remove their favourite presences through the user interface of the [website](https://premid.app/).

> Before getting started, it is highly recommended that you look at our presence guidelines. 
> 
> {.is-warning}

- [ガイドライン](https://docs.premid.app/dev/presence/guidelines)
{.links-list}

# Structure

All presence are coded in [TypeScript](https://www.typescriptlang.org/). [TypeScript](https://www.typescriptlang.org/) has some extra spicy type definitions over JavaScript, so fixing and identifying bugs is way easier.

## インストール

1. [Git](https://git-scm.com/)をインストールする。
2. [Node](https://nodejs.org/en/)をインストールする。 ([npm](https://www.npmjs.com/)と一緒に)
3. [TypeScript](https://www.typescriptlang.org/index.html#download-links)をインストールする (ターミナルを開き、 `npm install -g typescript` と入力する)

## プロジェクトをクローンする

1. ターミナルを開き `git clone https://github.com/PreMiD/Presences` と入力する
2. 任意のフォルダーを選択する
3. ソースコードエディタで開く

## フォルダーとファイルを作成する

1. Go in the `websites` folder and then go into the folder with the first letter of the **name** (not an URL) of the service you want to support.
2. Create a folder with the **name** (not an URL) of the service you want to support.
3. Create a `presence.ts` and a `tsconfig.json` file inside.
4. Create a folder named `dist` inside.
5. Create a `metadata.json` file inside the `dist` folder.

## tsconfig.jsonファイルの記入

Please put the following code inside of the `tsconfig.json` file.

```json
{
  "extends": "../../../tsconfig.json",
  "compilerOptions": {
    "outDir": "./dist/"
  }
}
```

To learn more about TypeScript configuration click [here](/dev/presence/tsconfig).

## metadata.jsonファイルの記入

We've made a `metadata.json` file creator for the lazy peeps [here](https://eggsy.xyz/projects/premid/mdcreator). It's still suggested to read this through so you know how it works.

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

Please copy the code above and put it in your `metadata.json` file. You now need to edit values of the properties. Please note that the following properties are optional to have in your `metadata.json` file, if you do not plan on using them you need to remove them.

- `contributors`
- `altnames`
- `regExp`
- `iframe`
- `iFrameRegExp`
- `readLogs`
- `settings`

**一部の値の内容を説明します:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">変数</th>
      <th style="text-align:left">概要</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">省略可能</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>author</b></td>
      <td style="text-align:left">Should contain an Object with the <code>name</code> and <code>id</code> of the presence developer. <code>name</code>はあなたのDiscordタグから識別子(#0000)を取ったもので、 <code>id</code>はDiscord上で開発者モードをオンにし、プロフィールを右クリックするとコピーできるものです。</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>不可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>contributors</b></td>
      <td style="text-align:left">Should contain an Object with the <code>name</code> and <code>id</code> of the presence developer. <code>name</code>はあなたのDiscordタグから識別子(#0000)を取ったもので、 ユーザーの<code>id</code>はDiscord上で開発者モードをオンにし、プロフィールを右クリックするとコピーできます。</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>service</b></td>
      <td style="text-align:left">The title of the service that this presence supports.<br>
      (Must be the same name as the folder where everything is in)</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>不可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>altnames</b></td>
      <td style="text-align:left">Be able to search the presence using an alternative name.<br>
      Meant to be used for presences that have different names in different languages (e.g. Pokémon and 포켓몬스터).<br>
      You can also use it for presences that have special characters so you don't have to type those (e.g. Pokémon and Pokemon).</td>
      <td style="text-align:left"><code>Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>description</b></td>
      <td style="text-align:left">Small description of the presence, you can use description of the service if you are out of ideas. 説明文がどの言語かを示すコードと、その言語で書かれた説明文が必要です。 <i>あなたが書ける言語</i>だけで説明文を書いてください。 PreMiDの翻訳者があなたのmetadataファイルを後で編集します。</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>不可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>url</b></td>
      <td style="text-align:left">URL of the service.<br><b>Example:</b><code>vk.com</code><br>
      <b>This URL must match the URL of the website as it will detect whether or not this is the website to inject the script to.</b><br> Do <b>NOT</b> add <code>https://</code> or <code>http://</code> inside of the URL nor a slash at the end:
      <code>https://premid.app/</code> -> <code>premid.app</code><br>
      <b>Note</b>: Some URLs may have <code>www.</code> or something else in front of their domain. Do <b>NOT</b> forget to add it!<br>
      You can add multiple URLs by doing the following:<br>
      <code>["URL1", "URL2", "ETC."]</code><br>
      You could also use regExp also known as Regex for this task, explained further below.</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>不可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>regExp</b></td>
      <td style="text-align:left">A regular expression string used to match urls.<br>
      regExp or also known as Regex, can be used if a website has multiple subdomains.<br>
      You could use the following regExp for that:<br>
      <code>([a-z0-9]+)[.]domain[.]TLD"</code><br>
      TLD standing for Top Level Domain for example: .com .net (but do not enter the dot).<br>
      <code>([a-z0-9]+)</code> means anything from a to z and from 0 to 9.<br>
      You can get a quick starter by watching this <a href="https://youtu.be/sXQxhojSdZM">video</a>.<br>
      You can test your regExp at <a href="https://regex101.com/">Regex101</a>.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>version</b></td>
      <td style="text-align:left">プレゼンスのバージョンです。</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>不可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>logo</b></td>
      <td style="text-align:left">サービスのロゴの画像のURLです。</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>不可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>thumbnail</b></td>
      <td style="text-align:left">あなたのプレゼンスのサムネイルの画像のURLです。</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>不可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>color</b></td>
      <td style="text-align:left"><code>#HEX</code>コードで指定: あなたのプレゼンスが対応しているサービスのイメージ色を使うとよいでしょう。</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>不可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>tags</b></td>
      <td style="text-align:left">タグの配列を指定してください。タグは、ウェブサイト上でプレゼンスを見つけるのに役立ちます。</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>不可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>category</b></td>
      <td style="text-align:left">プレゼンスが当てはまるカテゴリー名の文字列です。 See the valid catergories <a href="https://docs.premid.app/dev/presence/metadata#presence-categories">here</a>.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>不可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iframe</b></td>
      <td style="text-align:left"><code>iFrames</code>が使われているかどうかの指定.</td>
      <td style="text-align:left"><code>Boolean</code></td>
      <td style="text-align:left"><code>可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iFrameRegExp</b></td>
      <td style="text-align:left">挿入するiframeを検出するのに使用する正規表現 See regExp for more info.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>readLogs</b></td>
      <td style="text-align:left">Defines whether the extension should be reading logs.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>可</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>settings</b></td>
      <td style="text-align:left">An array of settings the user can change.<br>
      Read more about presence settings <a href="https://docs.premid.app/dev/presence/metadata#presence-settings">here</a>.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>可</code></td>
    </tr>
  </tbody>
</table>

## 基本

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
  /*UpdateData is always firing, and therefore should be used as your refresh cycle, or `tick`. This is called several times a second where possible.

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

You can copy this into your `presence.ts` file and edit the values. Setting all the values is done inside of the updataData event.

For examples we suggest to look at the code of presences like: 1337x or 9GAG. For more information about the `Presence` class click [here](/dev/presence/class).

Since v2.2.0 there are now Slideshows, this allows you to show multiple `PresenceData` interfaces on an interval, for more information click about the `Slideshow` class [here](/dev/presence/slideshow).

## 特定のデータが入手できない？！

A lot of websites are using [iframes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) ([Inlineframes](https://en.wikipedia.org/wiki/HTML_element#Frames)). These html tags can contain multiple sources such as videos. But they're not relevant every time. Some are hidden or just not actively used. Check if you can extract the information you need without them before you do unnecessary work.

1. Check for them in your browsers console (be sure that you are on the **Elements** tab).
2. Search (<kbd>CTRL</kbd>+<kbd>F</kbd> (Windows) or <kbd>CMD</kbd>+<kbd>F</kbd> (MacOS)).
3. Execute `document.querySelectorAll("iframe")`.

If you find that your data is in a iFrame you need to do the following:

1. Create a `iframe.ts` file.
2. Set iFrame to `true` in your metadata file.
3. Filling in your iFrame file.

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

4. Making your presence file receive data from the iFrame file.

```ts
presence.on("iFrameData", (data) => {
  iFrameVideo = data.video;
  currentTime = data.time;
});
```

**Note:** This needs to be placed outside of the updateData event.

## コンパイル

Open a console in your folder and type `tsc -w` to compile the `presence.ts` into the `/dist` folder.

# プレゼンスをテストする

1. Open the extension popup in the browser and hold the <kbd>Shift</kbd> button on your keyboard.
2. **Load Presence** will appear in the Presences section.
3. Click on it while you are still holding the <kbd>Shift</kbd> button.
4. Select the /dist folder of your presence.

# お役立ち情報

## ホット・リロード

The website you are developing on is automatically reloading every time you save a file in your folder.

## デバッグ

- You can put `console.log("Test");` between your code and see if your browser console gives you that output. If yes then go on and try again after the next function. If not then there is an error above.
- If that doesn't help you either then ask a presence developer on our [Discord server](https://discord.premid.app/) for help.

# ファイルの解説

- [Presenceクラス](/dev/presence/class)
- [スライドショーのクラス](/dev/presence/slideshow)
- [iFrameクラス](/dev/presence/iframe)
- [Metadataファイル](/dev/presence/metadata)
- [TypeScriptの構成](/dev/presence/tsconfig ""){.links-list}
