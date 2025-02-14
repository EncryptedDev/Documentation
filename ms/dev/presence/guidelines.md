---
title: Garis Panduan Presence
description: Peraturan yang kesemua pembangun Presence perlu ikut untuk membolehkan Presence mereka ditambah.
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2021-09-07T01:44:53.883Z
---

<div align="center">
    <img src="https://github.com/PreMiD.png?size=2048" width="128px" style="max-width:100%;">
    <h3 style="font-size: 2rem; margin-bottom: 0">Garis Panduan Presence</h3>
    <h4 style="margin-top: 0">Semakan 3</h4>
    <br />
</div>

# Garis Panduan

Apabila menerbitkan Presence ke [repositori Presence](https://github.com/PreMiD/Presences/), kami memerlukan anda mengikut beberapa panduan yang ditetapkan. Bagi sesetengah orang, peraturan ketat ini nampak agak kejam. Namun, pelaksanaan set peraturan ini akan bantu kami dan pengguna untuk mengelakkan terjadinya isu.

# Penciptaan

Peraturan am pembangunan Presence adalah seperti berikut:

- Presence **mestilah** berkait dengan laman sesawang dipilih.
- Presence **tidak boleh** dibuat untuk laman sesawang haram. (sbg.cth., ubat penegas, pemasaran dadah, pornografi kanak-kanak, dsb.)
- Struktur fail mestilah bersih dan teratur, jangan sertakan fail yang tidak dinyatakan. (sbg. cth., folder vscode dan git, fail imej dan teks, dsb.)
- Anda perlu mempunyai struktur fail yang wajar, draf **tidak** dibenarkan.
- Presence untuk laman sesawang dengan (TLD `.onion`) atau laman sesawang dengan domain/hos percuma (sbg. cth., `.TK` [semua domain percuma Freenom], `.RF`, `GD`, dll) adalah **tidak** dibenarkan, pengecualian boleh dibuat sekiranya terdapat bukti bahawa mereka bayar untuk domain tersebut.
- Domain bagi Presence mestilah berusia sekurang-kurangnya 2 bulan.
- Presence yang mensasarkan halaman pelayar dalaman (seperti Kedai Web Chrome, `chrome://`, halaman `about:`, dll) **tidak** dibenarkan kerana mereka perlukan bendera uji kaji untuk dibolehkan di pihak pengguna dan mampu menyebabkan kerosakan pada pelayar mereka.
- Presence dengan sokongan hanya untuk subdomain tunggal **tidak** akan dibenarkan, kerana ia akan tampak rosak untuk halaman lain (seperti halaman utama), pengecualian boleh dibuat untuk halaman polisi dan perhubungan (kandungan yang tidak kerap digunakan) atau laman di mana kandungan lainnya tidak mempunyai kaitan. (sbg. cth., laman wikia)
- Presence untuk radio dalam talian hanya dibenarkan sekiranya radio tersebut mempunyai sekurang-kurangnya 100 pendengar mingguan dan 15 pendengar serempak dan mesti mempunyai beberaa ciri selain daripada setakat menunjukkan tajuk lagu/album, dll.
- Presence tidak dibenarkan untuk menjalankan kod JS dengan fungsi tersendiri untuk mendapatkan pemboleh ubah. Sekiranya Firefox mempunyai masalah dengan fungsi terbina dalam kelas `Presence`, anda dibenarkan membuat fungsi anda sendiri dan anda perlu memberitahu kami mengenainya di perihalan Permintaan Tarikan (Pull Request) berkaitan.
- Presence kualiti rendah (atau yang mana dengan konteks kecil) adalah **tidak** dibenarkan (sbg. cth., hanya menunjukkan logo dan tulisan tetapi tidak mengubahnya lagi).
- Presence untuk perkhidmatan seperti Bot/Senarai Pelayan Discord mesti mengikut keperluan tambahan berikut:
  - Domain mestilah berusia sekurang-kurangnya **6 bulan**.
  - Pelawat unik setiap hari:
    - Untuk domain berusia 6 hingga 12 bulan: **20,000 pelawat unik sehari**.
    - Untuk domain berusia 12+ bulan: **45,000 pelawat unik sehari**.
  - Laman sesawang tidak boleh menggunakan domain murah seperti `.xyz`, `.club` dan lain-lain.
  - Laman sesawang tersebut sendirinya mestilah mempunyai kualiti, reka bentuk, dll yang sangat bagus.
- Presence patut gunakan [maklumat umum](https://api.premid.app/v2/langFile/presence/en) (rentetan yang bermula dengan "general."). Anda boleh melakukannya dengan menggunakan nilai `multiLanguage` bersama-sama rentetan yang diberi. Sekiranya Presence anda memerlukan rentetan tersuai, maka anda tidak patut gunakan `multiLanguage` sehingga Presence tersebut mencapai 1000 pengguna. Anda boleh lihat contoh [di sini](https://docs.premid.app/dev/presence/class#getstringsobject).
- Penyertaan folder `dist`, fail `presence.ts`, fail `iframe.ts`, dan fail `metadata.json` adalah diwajibkan supaya hasilnya nanti serupa seperti apa yang diwakilkan dalam skema berikut:

```bash
presence
├── dist
│   └── metadata.json
├── presence.ts
└── tsconfig.json
```

atau jika anda menggunakan fail `iframe.ts`:

```bash
presence
├── dist
│   └── metadata.json
├── presence.ts
├── iframe.ts
└── tsconfig.json
```

## [**metadata.json**](https://docs.premid.app/dev/presence/metadata)

> Untuk kemudahan para pembangun Presence kami, kami telah sediakan skema yang anda boleh gunakan untuk mengesahkan kewibawaan fail `metadata` anda. Ini kesemuanya pilihan dan tidak diperlukan ketika proses ulasan.

> Ia amat digalakkan untuk anda kemaskan fail `metadata` dalam format yang ditunjukkan di bawah, dan anda mesti mempunyai nama perkhidmatan, keterangan, tag dan medan tetapan yang betul tatabahasanya. Apa-apa yang tidak dikemaskan mengikut spesifikasi **tidak** akan dibenarkan.

> Presence untuk laman sesawang yang mempunyai kandungan dewasa **mesti** mempunyai tag `nsfw`, dan logo/lakaran kecil berkaitan **tidak** boleh mengandungi kandungan sebegini.

Setiap Presence mempunyai fail pemerihal dipanggil `metadata.json`, metadata tersebut mempunyai piawaian ketat dan contoh fail ini boleh dilihat di bawah:

```json
{
  "$schema": "https://schemas.premid.app/metadata/1.5",
  "author": {
    "name": "PENGGUNA",
    "id": "ID"
  },
  "contributors": [
    {
      "name": "PENGGUNA",
      "id": "ID"
    }
  ],
  "service": "PERKHIDMATAN",
  "altnames": ["PERKHIDMATAN"],
  "description": {
    "en": "KETERANGAN"
  },
  "url": "URL",
  "version": "VERSI",
  "logo": "URL",
  "thumbnail": "URL",
  "color": "#HEX000",
  "tags": ["TAG1", "TAG2"],
  "category": "KATEGORI",
  "regExp": "UNGKAPAN NALAR",
  "iFrameRegExp": "UNGKAPAN NALAR",
  "iframe": false,
  "readLogs": false,
  "settings": [
    {
      "id": "multiLanguage",
      "multiLanguage": true
    }
    {
      "id": "ID",
      "title": "TAJUK PAPARAN",
      "icon": "IKON FONTAWESOME",
      "value": true
    },
    {
      "id": "ID",
      "if": {
        "ID": true
      },
      "title": "TAJUK PAPARAN",
      "icon": "IKON FONTAWESOME",
      "value": "\"%song%\" by %artist%",
      "placeholder": "use %song% or %artist%"
    },
    {
      "id": "ID",
      "title": "TAJUK PAPARAN",
      "icon": "IKON FONTAWESOME",
      "value": 0,
      "values": ["1", "2", "dll."]
    }
  ]
}
```

> Sekiranya sesuatu medan disenaraikan sebagai pilihan dalam [pendokumenan](https://docs.premid.app/dev/presence/metadata) atau jika ada tanda `*` pada kekunci tersebut, dan Presence anda menggunakan nilai lalai untuknya, jangan sertakannya dalam fail `metadata`. (sbg. cth., sebuah Presence tanpa sokongan iframe tidak perlukan medan `iframe`.)

> Semua imej dalam fail `metadata` mestilah dihoskan di `i.imgur.com`. Penggunaan kandungan yang dihoskan di laman sesawang **tidak** dibenarkan kerana laluan dan fail boleh berubah tanpa jangkaan.

Senarai medan dan peraturan berkaitan disenaraikan di bawah:

### **`$schema`**

- _Kekunci_ skema ini **mestilah** menyertakan tanda dolar di awal kekunci, ini akan memberi isyarat kepada penyunting teks bahawa anda ingin mengesahkan fail JSON anda terhadap sesuatu model. _Seperti yang dinyatakan sebelum ini, anda tidak perlu sertakan skema, tetapi jika anda sertakannya anda mesti mengambil kira perkara ini._

### **`author`**

- _Nilai_ ID **mestilah** menggunakan ID emping salji Discord anda. Anda boleh dapatkannya dengan membolehkan [mod pembangun](https://support.discord.com/hc/en-us/articles/206346498-Where-can-I-find-my-User-Server-Message-ID-). _Tolong **jangan** kelirukan yang ini dengan ID aplikasi anda, yang hanya digunakan untuk Presence anda._

### **`*contributors`**

- **Jangan** tambah diri sendiri sebagai penyumbang, dan jangan tambah orang lain sebagai penyumbang melainkan mereka telah membantu dalam ciptaan Presence.

### **`service`**

- Nama perkhidmatan **mestilah** sama dengan nama direktori Presence tersebut. Sebagai contoh, jika Presence berada di `/websites/Y/YouTube/`, maka nama perkhidmatannya mestilah `YouTube`.
- Anda **tidak boleh** gunakan URL sebagai nama perkhidmatan melainkan laman sesawang itu sendiri menggunakan URL sebagai nama rasminya. Jika nama tidak deskriptif dan boleh dianggap kabur, penggunaan URL sebagai nama **diperlukan**. (sbg. cth., `YouTube` dibenarkan kerana ia nama rasmi dan deskriptif, manakala `youtube.com` tidak dibenarkan. `Top` pula bukan nama yang deskriptif, jadi penggunaan URL `top.gg` adalah **diperlukan**.)
- Jika perkhidmatan mempunyai peraturan penjenamaan khusus mengenai nama mereka, anda patut mengikut peraturan tersebut.

### **`*altnames`**

- **Hanya** gunakan ini dalam senario di mana laman sesawang menggunakan beberapa nama rasmi berlainan (spt. Pokémon dan 포켓몬스터). Versi _kependekan_ nama perkhidmatan diletakkan di bawah `tags`.

### **`description`**

- **Semua** Presence **mesti** mempunyai keterangan bahasa Inggeris tanpa mengira bahasa keutamaan laman sesawang.
- **Jangan** cuba untuk terjemah keterangan dengan sendiri melainkan anda tahu bahasa tersebut, penterjemah akan ubah `metadata.json` anda dan ubah keterangan jika diperlukan.

### **`url`**

- URL **mestilah** dalam bentuk rentetan sekiranya laman sesawang hanya gunakan satu domain. Jika laman sesawang menggunakan beberapa domain, letakkan nilai sebagai tatasusunan dan nyatakan setiap satunya.
- **Jangan** sertakan protokol di dalam URL (sbg. cth., `http` atau `https`), dan jangan sertakan parameter pertanyaan (sbg. cth., `www.google.com/search?gws_rd=ssl` yang mana sepatutnya ditulis sebagai `www.google.com`)

### **`version`**

- Sentiasa pastikan nombor versi mengikut [piawaian pemversian semantik](https://semver.org), yang diterjemah ke skema berikut: `<NEW-FEATURE>.<HUGE-BUGFIX>.<SMALL-BUGFIX-OR-METADATA-CHANGES>` (&lt;CIRI-BAHARU&gt;.&lt;PEMBAIKIAN-PEPIJAT-BESAR&gt;.&lt;PEMBAIKIAN-PEPIJAT-KECIL-ATAU-PERUBAHAN-METADATA&gt;). Pemversian lain seperti `1.0.0.1`, `1.0`, `1`, `1.0.0-BETA` atau mengubah `1.0.0` ke `2.0.0` untuk pembaikian pepijat/perubahan kecil **tidak** dibenarkan.
- Versi **mestilah** bermula dengan `1.0.0` melainkan diberitahu sebaliknya, versi lain **tidak** akan dibenarkan.

### **`logo`**

- Logo **mestilah** imej segi empat sama dengan nisbah bidang `1:1`.
- Imej **mestilah** mempunyai resolusi sekurang-kurangnya `512x512` piksel. Anda boleh membesarkan saiznya menggunakan alatan seperti [waifu2x](http://waifu2x.udp.jp/).

### **`thumbnail`**

- Lakaran kecil **patut** menggunakan [kad promosi lebar](https://i.imgur.com/3QfIc5v.jpg) jika boleh atau [tangkapan layar](https://i.imgur.com/OAcBmwW.png) jika **tiada** kad tersebut.

### **`color`**

- Warna **mestilah** nilai perenambelasan di antara `#000000` dan `#FFFFFF`.
- Rentetan warna **mestilah** diawalkan dengan simbol tanda pagar.

### **`tags`**

- **Semua** Presence mesti mempunyai sekurang-kurangnya _sebuah_ tag.
- Tag **tidak** patut ada sebarang selang, tanda palang, tanda petik tunggal/ganda, aksara Unicode, dan mestilah berhuruf kecil.
- Tag **sepatutnya** menyertakan nama perkhidmatan alternatif untuk memudahkan carian (sbg. cth., jika Presence untuk Amazon menyertakan sokongan AWS, ia perlu ada tag seperti `amazon-web-services` dan `aws`)
- Anda **perlu** tambah tag `NSFW` sekiranya Presence tersebut adalah untuk laman sesawang dewasa (NSFW 18+).

### **`category`**

- Kategori **mestilah** di kalangan kategori yang disenaraikan dalam [pendokumenan](https://docs.premid.app/dev/presence/metadata#presence-categories).
- Presence mestilah menggunakan kategori yang serasi dengan kandungan laman sesawang. (sbg. cth., jangan gunakan `anime` apabila laman sesawang tiada kaitan dengan anime).

### **`*regExp`** <br /> **`*iFrameRegExp`**

- Ungkapan nalar **mestilah** sah. Sila uji ungkapan anda menggunakan alatan yang disenaraikan dalam [pendokumenan](https://docs.premid.app/dev/presence/metadata#testing).

### **`readLogs`**

- Mestilah dalam nilai `boolean` (spt. `true` atau `false`).
- Membolehkan log untuk Presence anda.

### **`warning`**

- Membolehkan ikon amaran untuk memberitahu pengguna bahawa Presence ini memerlukan langkah tambahan dan tidak cukup sekadar menambah Presence.
- Contoh Presence yang menggunakan pemboleh ubah metadata ini ialah `VLC`.

### **`settings`**

- Jika anda memutuskan untuk membuat rentetan format (sbg. cth., `%song% by %artist%`), anda mesti meletakkan pemboleh ubah yang diapit dengan tanda peratus di kedua-dua sisi. Pemboleh ubah seperti `%var`, `var%`, atau `%%var%%` dan lain-lain yang serupa **tidak** dibenarkan untuk tujuan pemiawaian.
- Nama tetapan **tidak** patut berhuruf besar semata-mata. Sebagai contoh, nama seperti `SHOW BROWSING STATUS` itu **tidak** akan dibenarkan; tetapi, nama seperti `Show Browsing Status` atau `Show browsing status` dibenarkan.
- Jika anda menggunakan pilihan `multiLanguage`, anda patut tahu:
  - Nilai jenis **Boolean** hanya membolehkan rentetan daripada [`general.json`](https://github.com/PreMiD/Localization/blob/master/src/Presence/general.json) di repositori Penyetempatan atau daripada fail Presence (cth. apabila nama Presence ialah YouTube, sambungan akan dapatkan rentetan daripada fail `youtube.json` juga.)
  - Nilai jenis rentetan **String** (cth. `youtube`) akan menyatakan nama fail yang mana anda ingin dapatkan rentetan tersebut.
  - Nilai jenis tatasusunan **Array<String>** (cth. `["youtube", "discord"]`) akan menyatakan nama bagi kesemua fail berkaitan yang anda ingin dapatkan rentetan tersebut.

## [**presence.ts**](https://docs.premid.app/dev/presence/class)

> Kod yang anda tulis **mesti** ditulis dengan _baik_ dan **mesti** boleh _dibaca_ dan kesemua rentetan mestilah betul tatabahasanya (kesalahan tatabahasa di laman sesawang boleh diabaikan).

> Setiap Presence perlu ikut set peraturan lin yang ketat yang akan diperiksa semasa proses semakan. Beberapa pengesyoran boleh dilihat di bawah. [TypeScript Plugin Recommendations for Strict Type Checking](https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/eslint-plugin/docs/rules) untuk pengesyoran pemalam TypeScript bagi pemeriksaan jenis ketat. [ESlint Recommendations](https://eslint.org/docs/rules) untuk pengesyoran ESlint. [Prettier](https://prettier.io/) untuk menyusun semula format agar mengikut piawaian.

Ini senarai peraturan yang perlu diikuti semasa menulis fail `presence.ts` anda:

- **Sentiasa** isytihar tika baharu kelas `Presence` sebelum isytihar pemboleh ubah lain untuk mengelakkan isu terpencil yang mampu berlaku; ini bukan keperluan mengikut reka cipta jadi ia mungkin dialihkan pada masa hadapan.
- **Jangan** guna fungsi sendiri apabila [varian natif telah wujud](https://docs.premid.app/dev/presence#files-explained); ini untuk memastikan pembaikian di peringkat sambungan akan turut dikenakan pada Presence anda. Anda bebas untuk gunakan apa sahaja yang diperlukan sekiranya anda tidak menjumpainya disenaraikan dalam pendokumenan.
- Anda **dilarang** mengekod Presence untuk sesuatu laman tanpa menambah sokongan bahasa utamanya (sbg. cth., Presence untuk YouTube dikodkan dengan sokongan untuk bahasa Portugis dan bahasa Jepun, tanpa bahasa Inggeris itu sendiri.)
- Medan `smallImageKey` dan `smallImageText` bertujuan untuk menyediakan konteks tambahan/sekunder (seperti `playing/paused` untuk laman video, `browsing` untuk laman biasa, dan kegunaan lain) bukan untuk mempromosikan profil Discord atau apa-apa yang tidak berkaitan dengan PreMiD.
- Anda **tidak** dibenarkan mencapai `localStorage`.
- Apabila mencapai kuki untuk data disimpan, sila namakan kekunci dengan awalan `PMD_`.
- Anda hanya boleh lakukan permintaan HTTP/HTTPS ke `premid.app` atau API laman sesawang Presence. Jika anda menggunakan domain luaran, anda akan diminta menjelaskan kenapa ia diperlukan. API yang dibenarkan untuk membuat permintaan hanyalah [`Fetch API`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).
- **Jangan** tetapkan medan dalam objek presenceData sebagai tak tertakrif setelah ia diisytiharkan, sebaliknya gunakanlah kata kunci `delete`. (sbg. cth., gunakan `delete data.startTimestamp` dan bukannya `data.startTimestamp = undefined`)
- Anda **tidak** dibenarkan untuk menulis Presence yang mengubah kefungsian laman sesawang yang berkaitan. Ini termasuk penambahan, pemadaman, atau perubahan unsur DOM.
- Presence yang menggunakan butang mesti mengikut keperluan tambahan:
  - Lencongan ke laman utama tidak dibenarkan.
  - Promosi laman sesawang menggunakannya tidak dibenarkan.
  - Ia tidak boleh memaparkan maklumat yang tidak muat di medan yang lain.
  - Melencongkan secara terus ke strim audio/video adalah tidak dibenarkan.


## [**tsconfig.json**](https://docs.premid.app/dev/presence/tsconfig)

> **Jangan** tulis fail `tsconfig.json` anda sendiri, gunakan apa yang telah disediakan dalam [pendokumenan](https://docs.premid.app/dev/presence/tsconfig).

## Pengubahsuaian

> Anda **mesti** ubah versi dalam **metadata** kepada nilai lebih tinggi daripada versi sebelumnya apabila membuat perubahan kepada fail **presence.ts**, **iframe.ts** atau **metadata.json**.

Dalam sesetengah keadaan, Presence mungkin berkelakuan luar jangkaan atau diubah secara kecil untuk meningkatkan kefungsian mereka. Ini senarai peraturan yang anda **mesti** ikuti ketika mengubahsuai Presence.

- Jika penulis bagi Presence tertentu tidak dapat dihubungi melebihi sebulan, anda boleh hubungi pengulas untuk tentukan sama ada anda boleh mengubah Presence tersebut.
- Jika anda mengubah suai sesebuah Presence dan mengubah sekurang-kurangnya **satu suku** daripada pangkalan kod Presence tersebut, anda dibenarkan menambah diri sendiri sebagai penyumbang. Hubungi pengulas untuk maklumat lanjut mengenai perkara ini.
- Sesiapapun boleh cipta PR untuk membaiki pepijat. **Jangan** tukar imej jika ia tidak ketinggalan zaman dan masih mengikut spesifikasi.

# Pengesahan

> **Semua** kod yang disumbangkan ke kedai akan dilesenkan di bawah `Mozilla Public License 2.0`.

> Jika anda perlu menghubungi seseorang, sila gunakan pelayan Discord rasmi kami. Kesemua pengulas akan mempunyai peranan `Reviewer` di profil mereka.

> Sila ingat bahawa pengulas membuat kerja secara sukarela dan menguruskan repositori lain di samping yang ini, permintaan tarikan anda mungkin tidak diulas sehingga berlalunya beberapa jam atau hari setelah ia dicipta.

> **Sentiasa** pastikan cabangan anda mutakhir sebelum mencipta permintaan tarikan anda. Ini akan bantu mengehadkan positif palsu daripada semakan.

Proses paling penting dalam pembangunan Presence adalah untuk memasukkan Presence anda ke dalam kedai. Ini dilakukan dengan membuat [permintaan tarikan](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request) di GitHub pada repositori `PreMiD/Presences`. Pengulas kami akan sahkan Presence anda mengikut piawaian dan akan memasukkannya ke dalam kedai.

<div>
  <h2 style="font-size: 2rem; margin-bottom: 0;">Pengulas Presence</h2>
  <a href="https://github.com/Bas950"><img src="https://github.com/Bas950.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a> <a href="https://github.com/Slowlife01"><img src="https://github.com/Slowlife01.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a> <a href="https://github.com/EncryptedDev"><img src="https://github.com/EncryptedDev.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
  <br />
</div>

## `Sekatan`

Kesalahan berulang seperti pelanggaran garis panduan, penspaman permintaan tarikan, ancaman, atau perlakuan tidak sesuai akan mengharamkan anda daripada mencipta Presence.

Dalam senario ini, perubahan berikut akan berlaku:

- Presence di bawah pengurusan anda akan dipindahkan ke bot PreMiD atau pengguna lain (ikut keputusan pengulas). ID aplikasi untuk setiap Presence akan dicipta semula di bawah nama pemilik baharu.
- Kesemua isu dan permintaan tarikan anda (penciptaan Presence, penyumbangan Presence, dll) yang dicipta setelah pengharaman akan ditutup dengan segera.
- Semua tiket yang dicipta di bawah nama anda berkaitan pembangunan Presence akan dipadam.

## `Pengulasan`

Beberapa perkara anda patut tahu sebelum membuka permintaan tarikan:

- Ia memerlukan 2 orang pengulas untuk mencantumkan permintaan tarikan.
- Jika permintaan tarikan tidak aktif untuk tempoh 7 hari, ia akan ditutup dengan segera.
- Kesemua pemeriksaan **mestilah** lulus untuk membolehkan ia dicantumkan.
- ⚠️ Anda **mesti** berikan tangkapan layar baharu, tidak tersunting (diambil oleh anda sendiri) yang menunjukkan perbandingan profil anda dan laman sesawang untuk membuktikan Presence anda berfungsi. _Anda dibenarkan untuk menggabungkan tangkapan layar untuk menyenangkan pandangan_ Ini digunapakai untuk kedua-dua penciptaan dan pengubahsuaian.
- ⚠️ Anda juga **perlu** sertakan tangkapan layar tetapan Presence di dalam sambungan sekiranya dibekalkan. Contoh boleh dilihat di [sini](https://imgur.com/a/OD3sj5R).

## `Semakan`

![Contoh semakan](https://i.imgur.com/vF7QpBH.png)

Ketika ini, sesebuah Presence melalui 3 peringkat semakan yang berlainan. Kesemua semakan ini membantu pengulas untuk menentukan sama ada Presence anda sesuai untuk dikerahkan.

- `DeepScan` ialah bot yang memeriksa kualiti kod. Jika anda menerima ralat untuk isu baharu, anda **diwajibkan** membaikinya. *Amaran: DeepScan tidak akan sentiasa tunjukkan ralat untuk anda. Sebaliknya, sila lihat amaran yang dikeluarkan oleh CodeFactor.*
- `CodeFactor` ialah bot yang memeriksa kualiti kod. Jika anda menerima ralat untuk isu baharu, anda **diwajibkan** membaikinya.
- `Schema Validation` akan mengimbas fail `metadata.json` untuk sebarang ralat (sbg. cth., medan yang tercicir, jenis nilai yang tidak sah, dll.). Jika anda nampak sebarang isu baharu, anda juga **diwajibkan** untuk membaikinya. Penambahan medan skema ke fail `metadata.json` anda akan membolehkan penyunting teks anda (jika disokong) untuk menunjukkan ralat-ralat ini kepada anda ketika pembangunan.

## `Peraturan Tambahan`

- **Sentiasa** pastikan anda mulakan Presence anda dalam folder yang sesuai, sekiranya namanya bermula dengan _sebarang_ huruf Rumi maka ia mestilah berada di bawah padanan abjadnya (sbg. cth., `D/dアニメストア` atau `G/Google`). Sebarang aksara Unicode/bukan-Rumi yang lain **mesti** berada di bawah folder `#` (sbg. cth., `#/巴哈姆特`) dan nombor berada di bawah folder `0-9` (sbg. cth., `0-9/4anime`).

Setelah mematuhi kesemua garis panduan dengan ulasan dan semakan yang wajar, Presence anda akan dicantumkan dengan kedai.

# Cadangan

Jika anda mempunyai cadangan berkaitan garis panduan kami, anda patut hubungi kami @ [pelayan Discord PreMiD](https://discord.premid.app) dan kami akan memeriksanya!

# Sumbangan

Semakan `Revision 3` garis panduan ditulis dan disumbangkan oleh individu berikut:

<div>
<a href="https://github.com/PreMiD"><img src="https://github.com/PreMiD.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
</div>

Semakan `Revision 2` garis panduan ditulis dan disumbangkan oleh individu berikut:

<div>
<a href="https://github.com/CobyPowers"><img src="https://github.com/CobyPowers.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
</div>

Semakan `Revision 1` telah diselenggara oleh individu berikut:

<div>
<a href="https://github.com/CobyPowers"><img src="https://github.com/CobyPowers.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
<a href="https://github.com/Bas950"><img src="https://github.com/Bas950.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
<a href="https://github.com/i1u5"><img src="https://github.com/i1u5.png?size=2048" width="48px" style="max-width:100%; border-radius: 50%;"/></a>
</div>
