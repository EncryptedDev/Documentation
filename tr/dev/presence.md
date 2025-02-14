---
title: Servis Geliştirme
description:
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2020-06-11T18:04:02.843Z
---

> Tüm servisler artık [https://github.com/PreMiD/Presences](https://github.com/PreMiD/Presences) adresinde saklanmaktadır. 
> 
> {.is-info}

`2.x` sürümleri, [servis mağazası](https://premid.app/store) özelliği ile birlikte gelir. Kullanıcılar bundan sonra kendi oluşturdukları servisleri [mağazaya](https://premid.app/store) ekletebilecek ve diğer kullanıcıların kullanımına sunabilecek.

> Başlamadan önce servis kılavuzlarına uymanız şiddetle tavsiye edilir. 
> 
> {.is-warning}

- [Kurallar](https://docs.premid.app/dev/presence/guidelines)
{.links-list}

# Yapı

Tüm servisler [TypeScript](https://www.typescriptlang.org/) ile kodlanır. [TypeScript](https://www.typescriptlang.org/)'in içerisinde bulundurduğu bir çok tanımlamalar ile kodunuzdaki hataları bulmak çok daha kolay olacaktır.

## Yükleme

1. [Git](https://git-scm.com/)'i yükleyin.
2. [Node](https://nodejs.org/en/)'u yükleyin.
3. Konsolunuzu açın ve [TypeScript](https://www.typescriptlang.org/index.html#download-links)'i yüklemek için `npm install -g typescript` yazın.

## Projeyi klonlama

1. Bir konsol açın ve `git clone https://github.com/PreMiD/Presences` yazın.
2. Bir klasör seçin.
3. Klasörü kullandığınız editör ile açın.

## Klasörleri ve dosyaları oluşturma

1. Servisinizin **name** (URL adresinin değil) kısmında belirtilen isminin ilk harfinin bulunduğu `websites` klasörünün içerisindeki klasöre girin.
2. Servisin **adı** (URL'si değil) ile bir klasör oluşturun.
3. Bir `presence.ts` ve bir `tsconfig.json` dosyası oluşturun.
4. Ana klasörün içine `dist` adında bir klasör oluşturun.
5. `dist` klasörünün içine de bir `metadata.json` dosyası oluşturun.

## tsconfig.json dosyasını doldurma

Aşağıda gördüğünüz kodu `tsconfig.json` dosyasının içine yapıştırın.

```json
{
  "extends": "../../../tsconfig.json",
  "compilerOptions": {
    "outDir": "./dist/"
  }
}
```

TypeScript konfigürasyonu hakkında daha fazla bilgi almak için [buraya](/dev/presence/tsconfig) tıklayın.

## metadata.json dosyasını doldurma

Bu dosyayla fazla uğraşmak istemeyenler için bir `metadata.json` dosyası oluşturucu formu yaptık, görmek için [buraya](https://eggsy.xyz/projects/premid/mdcreator) tıklayabilirsiniz. Eğer isterseniz bu kısmı okuyarak bu dosyanın nasıl çalıştığını anlayabilirsiniz.

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

Yukarıdaki kodu kopyalayın ve `metadata.json` dosyanıza yapıştırın. Bundan sonra belirtilen verileri düzenlemeniz gerekecektir. Eğer aşağıda "opsiyonel" olarak belirtilen kısımları kullanmayacaksanız lütfen bu alanları `metadata.json` dosyanızdan kaldırın.

- `contributors`
- `altnames`
- `regExp`
- `iframe`
- `iFrameRegExp`
- `readLogs`
- `settings`

**Bu veriler hakkında daha fazla bilgi istiyorsanız:**

<table>
  <thead>
    <tr>
      <th style="text-align:left">Değişken</th>
      <th style="text-align:left">Açıklama</th>
      <th style="text-align:left">Tür</th>
      <th style="text-align:left">Opsiyonel</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>author</b></td>
      <td style="text-align:left">Servis geliştiricisinin <code>isim</code> ve <code>id</code> bilgileri bulunan bir Obje içermelidir. <code>name</code> etiketinizin (#0000) olmadığı Discord kullanıcı adınızdır. Kullanıcı <code>id</code>'leri Discord'da geliştirici modunu aktifleştirerek alınabilir.</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>Hayır</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>contributors</b></td>
      <td style="text-align:left">Servis geliştiricisinin <code>name</code> ve <code>id</code> bilgileri bulunan bir Object içermelidir. <code>name</code> etiketinizin (#0000) olmadığı Discord kullanıcı adınızdır. Kullanıcı <code>id</code>'leri Discord'da geliştirici modunu aktifleştirerek alınabilir.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>Evet</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>service</b></td>
      <td style="text-align:left">Servisin başlığı. Başlık servisin tüm dosyalarının içinde bulunduğu klasör ile aynı isimde olmalıdır.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Hayır</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>altnames</b></td>
      <td style="text-align:left">Servisi ararken alternatif isimlerle aranabilmesi için kullanabileceğiniz alan. Farklı dillerde veya farklı şekilde yazılan (örneğin Pokémon ve 포켓몬스터) servisler ve isminde özel karakter içeren servisler için kullanılabilir.</td>
      <td style="text-align:left"><code>Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Evet</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>description</b></td>
      <td style="text-align:left">Servis hakkında kısa bir açıklama, eğer aklınıza bir fikir gelmiyorsa servisin kendi açıklamasını kullanabilirsiniz. Açıklamalarınız dilin kodu ve bu dille yazılmış açıklamanın kendisini içermelidir. Sadece <i>bildiğiniz</i> dillerin çevirisini yapın, geri kalanları ilerleyen zamanlarda çevirmen ekibimiz halledecektir.</td>
      <td style="text-align:left"><code>Object</code></td>
      <td style="text-align:left"><code>Hayır</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>url</b></td>
      <td style="text-align:left">Servisin adresi.<br><b>Example:</b><code>youtube.com.tr</code><br>
      <b>Buraya girdiğiniz adres servisin adres ile uyuşmalıdır, bu sayede yazdığınız kod sayfaya enjete edilecek ve çalıştırılacaktır..</b><br> <b>Hiçbir</b> durumda adreslerin başına <code>https://</code> veya <code>http://</code>, sonuna ise <code>/</code> eklemeyin:
      <code>https://premid.app/</code> -> <code>premid.app</code><br>
      <b>Not</b>: Bazı servisler resmi olarak adreslerinin başında <code>www.</code> kullanabilir. Onu eklemeyi de unutmamalısınız!<br>
      Şu yöntemi kullanarak servisinizin birden fazla adreste çalışmasını sağlayabilirsiniz:<br>
      <code>["URL1", "URL2", "VS."]</code><br>
      Gerekirse regExp (Regex) yöntemini de kullanabilirsiniz. Bunun hakkında daha fazla bilgiye aşağıdan erişebilirsiniz.</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Hayır</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>regExp</b></td>
      <td style="text-align:left">Adresleri tanımlamak için kullanılacak olan regex biçimindeki sözcük dizimi.<br>
      regExp veya Regex, birden çok alt alanadı bulunduran servisler için kullanılabilir.<br>
      Bu durumda şu regex dizimini kullanabilirsiniz:<br>
      <code>([a-z0-9]+)[.]alanadı[.]TLD"</code><br>
      TLD burada Top Level Domain kısaltması olarak kullanılamkta ve şunları ifade etmektedir: .com .net<br>
      <code>([a-z0-9]+)</code> a'dan z'ye ve 0'dan 9'a olan tüm karakterlerin bu dizime yakalanacağı anlamına gelmektedir.<br>
      Kullanımını daha iyi anlamak için <a href="https://youtu.be/sXQxhojSdZM">bu videoyu</a> izleyebilirsiniz.<br>
      Kullanacağınız regExp'i <a href="https://regex101.com/">Regex101</a> sitesinde test edebilirsiniz.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Evet</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>version</b></td>
      <td style="text-align:left">Servisinizin sürümü.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Hayır</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>logo</b></td>
      <td style="text-align:left">Servisin logosunu içeren resim bağlantısı.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Hayır</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>thumbnail</b></td>
      <td style="text-align:left">Mağazada gözükecek arka plan resminin bağlantısı.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Hayır</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>color</b></td>
      <td style="text-align:left"><code>#HEX</code> değeri. Servisin kullandığı renkleri kullanmanızı tavsiye ediyoruz.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Hayır</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>tags</b></td>
      <td style="text-align:left">Servisinize ait etiketleri içeren bir Array, bu etiketler servisinizin aramalarda çıkmasını kolaylaştırır.</td>
      <td style="text-align:left"><code>String, Array&lt;String&gt;</code></td>
      <td style="text-align:left"><code>Hayır</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>category</b></td>
      <td style="text-align:left">Servisinizin ait olduğu kategori. Geçerli kategorileri görmek için <a href="https://docs.premid.app/dev/presence/metadata#presence-categories">buraya</a> tıklayabilirsiniz.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Hayır</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iframe</b></td>
      <td style="text-align:left"><code>iframe</code>'lerin kullanılıp kullanılmayacağını belirler.</td>
      <td style="text-align:left"><code>Boolean</code></td>
      <td style="text-align:left"><code>Evet</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>iFrameRegExp</b></td>
      <td style="text-align:left">Iframe verisinin alınacağı kaynakları yakalayacak regex verisi. Daha fazla bilgi için regExp kısmına bakın.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Evet</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>readLogs</b></td>
      <td style="text-align:left">Servisinizin konsol kayıtlarını okuyup okumayacağını belirler.</td>
      <td style="text-align:left"><code>String</code></td>
      <td style="text-align:left"><code>Evet</code></td>
    </tr>
    <tr>
      <td style="text-align:left"><b>settings</b></td>
      <td style="text-align:left">Kullanıcıların değiştirebileceği ayarlar array'ı. Daha fazla bilgi için <a href="https://docs.premid.app/dev/presence/metadata#presence-settings">buraya</a> gözatın.</td>
      <td style="text-align:left"><code>Array&lt;Object&gt;</code></td>
      <td style="text-align:left"><code>Evet</code></td>
    </tr>
  </tbody>
</table>

## Başlarken

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
  /*UpdateData is always firing, and therefore should be used as your refresh cycle, or `tick`. Bu olay, mümkün olduğunca bir saniye içerisinde birkaç kez çağrılacaktır.

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

Bunu `presence.ts` dosyanıza kopyalayıp değerleri düzenleyebilirsiniz. Değerleri ayarlama işlemi updateData eventi içinde gerçekleşir.

Örnekler için 1337x veya 9GAG gibi servislerin kodlarını incelemenizi öneririz. `Presence` sınıfı hakkında daha fazla bilgi almak için [buradaki](/dev/presence/class) sayfayı ziyaret edebilirsiniz.

Since v2.2.0 there are now Slideshows, this allows you to show multiple `PresenceData` interfaces on an interval, for more information click about the `Slideshow` class [here](/dev/presence/slideshow).

## İstediğiniz veriyi alamıyor musunuz?!

Bir çok site [iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) ([inlineframes](https://en.wikipedia.org/wiki/HTML_element#Frames)) kullanır. Bu HTML etiketleri videolar gibi bir çok kaynak bulundurabilir. Ancak her zaman aynı sonucu vermez. Bazıları gizlidir veya aktif olarak kullanılmaz. Check if you can extract the information you need without them before you do unnecessary work.

1. Tarayıcınızın konsolundan kontrol edin (**Elements** sekmesinde olduğunuza emin olun).
2. Search (<kbd>CTRL</kbd>+<kbd>F</kbd> (Windows) or <kbd>CMD</kbd>+<kbd>F</kbd> (MacOS)).
3. Konsoldan devam etmek için konsola `document.querySelectorAll("iframe")` yazabilir ve sayfadaki iframe kaynaklarını görebilirsiniz.

İstediğiniz verilerin bir iFrame'de olduğunu bulursanız aşağıdakileri yapmanız gerekir:

1. Bir `iframe.ts` dosyası oluşturun.
2. "metadata" dosyasında `iFrame` kısmını `true` olarak ayarlayın.
3. iFrame dosyanızı şu şekilde dolurun:

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

4. Yukarıdaki gibi gönderilen bir veriyi servis kodunun içinde alabilmek için aşağıdaki yöntemi kullanın.

```ts
presence.on("iFrameData", (data) => {
  iFrameVideo = data.video;
  currentTime = data.time;
});
```

**Note:** This needs to be placed outside of the updateData event.

## Derleme

Open a console in your folder and type `tsc -w` to compile the `presence.ts` into the `/dist` folder.

# Servisi test etme

1. Eklenti penceresini açın ve klavyenizdeki <kbd>Shift</kbd> tuşuna basılı tutun.
2. Servisler kısmının hemen sağında **Servis Yükle** yazısı çıkacaktır.
3. <kbd>Shift</kbd>'e basılı tutarken bu yazıya tıklayın.
4. Servisinizin dist klasörünü bulun ve seçin.

# Bazı yararlı şeyler

## Anında yenileme

Servisinizin çalıştığı sayfalar, yerel dosyalarınızda yaptığınız herhangi bir değişiklikte otomatik olarak yenilenecektir.

## Hata ayıklama

- Kodunuzun çalışıp çalışmadığınızı test edebilmek için kodunuzun bir yerine basitçe `console.log("Test");` koyabilir ve konsola çıktı verip vermediğini kontrol edebilirsiniz. Eğer çıktı veriyorsa, devam edin. Eğer vermiyorsa, kod bu satırdan önce hataya geçmiş veya hiç bu satıra ulaşamamış demektir.
- Eğer bunların hiçbiri işe yaramadıysa, [Discord sunucumuzdan](https://discord.premid.app/) bir servis geliştiricisiyle iletişime geçebilirsiniz.

# Dosyaların açıklamaları

- [Presence Sınıfı](/dev/presence/class)
- [Slideshow Sınıfı](/dev/presence/slideshow)
- [iFrame Sınıfı](/dev/presence/iframe)
- [Metadata Dosyası](/dev/presence/metadata)
- [TypeScript Konfigürasyonu](/dev/presence/tsconfig ""){.links-list}
