---
title: Presence تطوير الـ
description:
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2020-06-11T18:04:02.843Z
---

> كل الpresences الان تخزن هنا: https://github.com/PreMiD/Presences 
> 
> {.is-info}

الإصدار `2.x` يقدم [متجر الpresence](https://premid.app/store). الأن لدى المستخدمين القدرة لاضافة وحذف الpresences المفضلين لهم يدويا من خلال واجهة المستخدم في [الموقع](https://premid.app/).

> قبل البدء، يوصى بشدة أن تنظروا إلى المبادئ التوجيهية للـ Presence الخاصة بنا. 
> 
> {.is-warning}

- [الإرشادات](https://docs.premid.app/dev/presence/guidelines)
{.links-list}

# الهيكل

كل الpresences مبرمجة علي [TypeScript](https://www.typescriptlang.org/). [TypeScript](https://www.typescriptlang.org/) لديها بعض التعاريف الإضافية على جافا سكريبت، لذلك فإن إصلاح وتحديد الأخطاء أسهل بكثير.

## تثبيت

1. قم بتثبيت [ Git ](https://git-scm.com/).
2. تثبيت [ Node ](https://nodejs.org/en/) (يأتي مع [ npm ](https://www.npmjs.com/)).
3. قم بتثبيت [ TypeScript ](https://www.typescriptlang.org/index.html#download-links) (افتح محطة و `npm install -g typescript`).

## استنساخ المشروع

1. قم بفتح لوحة التحكم و اكتب `git clone https://github.com/PreMiD/Presences`.
2. اختيار مجلد من اختيارك.
3. افتح على محرر الكود الخاص بك.

## إنشاء المجلدات والملفات

1. إنتقل إلى مجلد `المواقع` ثم إنتقل إلى المجلد الذي يحتوي على الحرف الأول من **الإسم** (ليس رابط) الخدمة التي تريد دعمها.
2. إنشاء مجلد باسم **** (ليس عنوان URL) للخدمة التي تريد دعمها.
3. قم بإنشاء ملف `presence.ts` و `tsconfig.json` داخله.
4. إنشاء مجلد اسمه `dist` في الداخل.
5. إنشاء ملف `metadata.json` داخل مجلد `dist`.

## ملء ملف tsconfig.json

الرجاء وضع الكود التالي داخل ملف `tsconfig.json`.

```json
{
  "extends": "../../../tsconfig.json",
  "compilerOptions": {
    "outDir": "./dist/"
  }
}
```

لمعرفة المزيد حول طريقة تعديل TypeScript انقر [هنا](/dev/presence/tsconfig).

## ملء ملف metadata.json

We've made a `metadata.json` file creator for the lazy peeps [here](https://eggsy.xyz/projects/premid/mdcreator). لا يزال من المقترح قراءة هذا من أجل معرفة كيف يعمل.

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

Please copy the code above and put it in your `metadata.json` file. تحتاج الآن إلى تعديل قيم الخصائص. Please note that the following properties are optional to have in your `metadata.json` file, if you do not plan on using them you need to remove them.

- `contributors`
- `altnames`
- `regExp`
- `iframe`
- `iFrameRegExp`
- `readLogs`
- `settings`

**توضيح بعض قيم الخصائص:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">متغير</th>
      <th style="text-align:left">الوصف</th>
      <th style="text-align:left">النوع</th>
      <th style="text-align:left">اختياري</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>author</b></td>
      <td style="text-align:left">Should contain an Object with the <code>name</code> and <code>id</code> of the presence developer. <code>اسم</code> هو اسمك في الديسكورد بدون المعرف(#0000). يمكن نسخ معرف المستخدم <code></code> من ديسكورد عن طريق تمكين وضع المطور
        والنقر الأيمن على ملفك الشخصي.</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>لا</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>contributors</b></td>
      <td style="text-align:left">يجب أن يحتوي الجسم على <code>إسم</code> و <code>أي-دي</code> مطور الـ presence. <code>اسم</code> هو اسمك في الديسكورد بدون المعرف(#0000). يمكن نسخ معرف المستخدم <code></code> من ديسكورد عن طريق تمكين وضع المطور
        والنقر الأيمن على ملفك الشخصي.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>نعم</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>service</b></td>
      <td style="text-align:left">The title of the service that this presence supports.<br>
      (Must be the same name as the folder where everything is in)</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>لا</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>altnames</b></td>
      <td style="text-align:left">Be able to search the presence using an alternative name.<br>
      Meant to be used for presences that have different names in different languages (e.g. Pokémon and 포켓몬스터).<br>
      You can also use it for presences that have special characters so you don't have to type those (e.g. Pokémon and Pokemon).</td>
      <td style="text-align:left"><code>Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>نعم</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>description</b></td>
      <td style="text-align:left">Small description of the presence, you can use description of the service if you are out of ideas. يجب أن يحتوي الوصف الخاص بك على قيم أزواج رئيسية تشير إلى اللغة، والوصف في تلك اللغة المحددة. اصنع وصفاً باللغات <i>التي تعرفها</i>، سوف يقوم مترجمونا بإجراء تغييرات على ملف البيانات الوصفية الخاص بك.</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>لا</code></td>
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
      <td style="text-align:left"><code>لا</code></td>
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
      <td style="text-align:left"><code>نعم</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>version</b></td>
      <td style="text-align:left">نسخة من الـ presence الخاصة بك.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>لا</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>logo</b></td>
      <td style="text-align:left">رابط الخدمة&apos;لـ شعار</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>لا</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>thumbnail</b></td>
      <td style="text-align:left">رابط للصورة المصغره لالpresence الخاص بك.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>لا</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>color</b></td>
      <td style="text-align:left">قيمة <code>#HEX</code>. نوصي باستخدام لون أساسي من الخدمة
        التي يدعمها وجودك.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>لا</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>tags</b></td>
      <td style="text-align:left">مصفوفة مع العلامات، ستساعد المستخدمين على البحث عن وجودك على الموقع.</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>لا</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>category</b></td>
      <td style="text-align:left">وتندرج تحت هذا البند سلسلة تستخدم لتمثيل الفئة التي يوجد فيها. مشاهدة الأخاديد الصالحة <a href="https://docs.premid.app/dev/presence/metadata#presence-categories">هنا</a>.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>لا</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iframe</b></td>
      <td style="text-align:left">يحدد ما إذا كان <code>iFrames</code> يستخدم.</td>
      <td style="text-align:left"><code>Boolean</code></td>
      <td style="text-align:left"><code>نعم</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iFrameRegExp</b></td>
      <td style="text-align:left">محدد تعبير عادي يحدد إطارات ifram للحقن. انظر regExp لمزيد من المعلومات.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>نعم</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>readLogs</b></td>
      <td style="text-align:left">يحدد ما إذا كان يجب أن يكون الملحق قادراً على قراءة السجلات.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>نعم</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>settings</b></td>
      <td style="text-align:left">An array of settings the user can change.<br>
      Read more about presence settings <a href="https://docs.premid.app/dev/presence/metadata#presence-settings">here</a>.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>نعم</code></td>
    </tr>
  </tbody>
</table>

## البدء

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
  /*UpdateData is always firing, and therefore should be used as your refresh cycle, or `tick`. يتم استدعاء هذا عدة مرات في الثانية حيثما أمكن.

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

You can copy this into your `presence.ts` file and edit the values. يتم تعيين جميع القيم داخل حدث updateData.

For examples we suggest to look at the code of presences like: 1337x or 9GAG. For more information about the `Presence` class click [here](/dev/presence/class).

Since v2.2.0 there are now Slideshows, this allows you to show multiple `PresenceData` interfaces on an interval, for more information click about the `Slideshow` class [here](/dev/presence/slideshow).

## لا يمكنك الحصول على بيانات معينة؟!

A lot of websites are using [iframes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) ([Inlineframes](https://en.wikipedia.org/wiki/HTML_element#Frames)). يمكن أن تحتوي علامات html هذه على مصادر متعددة مثل الفيديو. لكنها ليست لها صلة في كل مرة. بعضها مخفي أو لم يتم استخدامه بفعالية. Check if you can extract the information you need without them before you do unnecessary work.

1. Check for them in your browsers console (be sure that you are on the **Elements** tab).
2. Search (<kbd>CTRL</kbd>+<kbd>F</kbd> (Windows) or <kbd>CMD</kbd>+<kbd>F</kbd> (MacOS)).
3. تنفيذ `document.querySelectorAll("iframe")`.

إذا وجدت أن بياناتك في iFrame تحتاج إلى القيام بما يلي:

1. أنشى ملف `iframe.ts`.
2. عيّن الـ iFrame إلى `true` في ملف بيانات التعريف الخاص بك.
3. ملء ملف الـ iFrame الخاص بك.

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

4. جعل ملف الـ Presence يتلقى البيانات من ملف iFrame.

```ts
presence.on("iFrameData", (data) => {
  iFrameVideo = data.video;
  currentTime = data.time;
});
```

**Note:** This needs to be placed outside of the updateData event.

## تجميع

Open a console in your folder and type `tsc -w` to compile the `presence.ts` into the `/dist` folder.

# تحميل الـ presence

1. Open the extension popup in the browser and hold the <kbd>Shift</kbd> button on your keyboard.
2. **سوف يظهر تحميل الـ Presences ** في قسم الـ Presences.
3. انقر عليه بينما لا تزال تضغط زر <kbd>Shift</kbd>.
4. حدد مجلد /dist للـ presence الخاص بك.

# بعض الأشياء المفيدة

## إعادة التحميل

The website you are developing on is automatically reloading every time you save a file in your folder.

## تصحيح الأخطاء

- You can put `console.log("Test");` between your code and see if your browser console gives you that output. إذا كان الجواب نعم، حاول مرة أخرى بعد الدالة القادمة. إذا لم يكن فهناك خطأ أعلاه.
- If that doesn't help you either then ask a presence developer on our [Discord server](https://discord.premid.app/) for help.

# الملفات الموضحة

- [فئة الpresence](/dev/presence/class)
- [فئة عرض الشريحة](/dev/presence/slideshow)
- [فئة iFrame](/dev/presence/iframe)
- [ملف بيانات التعريف](/dev/presence/metadata)
- [إعدادات TypeScript](/dev/presence/tsconfig ""){.links-list}
