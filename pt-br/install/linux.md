---
title: Linux
description: Primeiros passos com a instalação do PreMiD no Linux
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2020-06-11T18:04:14.124Z
---

A instalação do aplicativo é muito importante, uma vez que a extensão não pode fazer nada por si só.

> Aur users that use DoomLerd's package should be safe as he says. We are not recommending to use it, but if you want you can still use it. Thanks to DoomLerd for handling aur repo still. 
> 
> {.is-warning}

## Tabela de Conteúdos

- **[Sobre](#about)**
  - [Estatísticas](#stats)
  - [Requisitos](#requirements)
  - Exemplos (em breve)
  - Perguntas Frequentes (em breve)
  - Building (soon)
  - [Suporte](#support)
  - [Créditos](#credits)
  - [Licença](#license)
- **[Snapcraft](#snapcraft)** (TL;DR : _never_ ™️)
- **[Portable AppImage](#appimage)** (_RECOMENDADO_)
  - [Installation instructions](#appimageinstall)
  - [Additional notes](#appimagenotes)
- [**Red Hat Enterprise Linux (RHEL) based distributions**](#packagecloud)
- [**Debian and Ubuntu based distributions**](#packagecloud)
- [**Arch Linux baseadas em distribuições Linux**](#arch)

<a name="about"></a>

## Sobre

**PreMiD** is a simple, configurable utility that uses Discord's RP ( Rich Presence ) library which allows you to show what you're doing on the web ( and a few programs ) in your Discord profile as **playing status**.

<a name="stats"></a>

### Estatísticas

<table>
  <tr>
    <th>Deployment</th>
    <th>Total downloads</th>
    <th>Latest release</th>
  </tr>
  <tr>
    <td><a href="https://github.com/PreMiD/Linux/actions"><img src="https://github.com/PreMiD/Linux/workflows/CI/badge.svg?branch=master&event=push" alt="CI"></a></td>
    <td><a href="https://github.com/PreMiD/Linux/releases"><img src="https://img.shields.io/github/downloads/PreMiD/Linux/total.svg?maxAge=86400" alt="All releases"></a></td>
    <td><a href="https://github.com/PreMiD/Linux/releases/latest"><img src="https://img.shields.io/github/v/release/PreMiD/Linux.svg?maxAge=86400" alt="Latest release"><br><img src="https://img.shields.io/github/downloads/PreMiD/Linux/latest/total.svg?maxAge=86400" alt="Github releases"></a></td>
  </tr>
</table>

<a name="requirements"></a>

### Requisitos

Technically every distribution that can run Discord's [official](https://discordapp.com/download) **app** ( not the web or the snap version ) can run PreMiD too;</br> As you may have noticed in the recent years, some Linux distributions started dropping support for the 32-bit (ia32/i686/i386/x86) architectures, and as a result, we did too. You can, however, try to build the app yourself if you desperately need to use it on a 32-bit distribution.</br> Since we currently use Electron as an engine (Discord does too!), its requirements also apply to this app :

- Ubuntu ≥ 12.04
- Fedora ≥ 21
- Debian ≥ 8

It is unknown whether older versions of other distributions support it, so just keep your distribution updated and use **LTS (Long-Term Support)** releases if your distribution offers them, as they're more stable (avoid alpha releases).

<a name="support"></a>

### Suporte

<div>
  <a target="_blank" href="https://discord.premid.app/" title="Junte-se ao nosso Discord!">
    <img height="75px" draggable="false" src="https://discordapp.com/api/guilds/493130730549805057/widget.png?style=banner2" alt="Junte-se ao nosso Discord!">
  </a>
</div>

<a name="credits"></a>

### Créditos

Thanks to :

- @nattadasu, @Rubensei, @Cairo2k18, zany130, Immanuel D, Friskytrash, Alexandre (and few other guys whom I forgot their names) for providing feedback on nightly releases.
- @apriluwu for maintaining the Gentoo builds
- @SlimShadyIAm and naka for formerly maintaining the Arch User Repository packages
- The Electron community for various packages
- Anyone else who has ever contributed to the project in any way.

<a name="license"></a>

### Licença

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FPreMiD%2FLinux.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2FPreMiD%2FLinux?ref=badge_large)

<img src="https://i.imgur.com/ACAxtmA.png" width="100" height="100" align="right"></img>
<a name="snapcraft"></a>

## Portable AppImage

O pacote AppImage é recomendado se o Discord funciona para você, mas para outros pacotes PreMiD (.deb, rpm, etc) não.

<a name="appimageinstall"></a>

### Installation instructions

```bash
wget https://github.com/PreMiD/Linux/releases/latest/download/PreMiD-Portable.AppImage && chmod a+x PreMiD*.AppImage
```

```bash
# Just double-click it or run
./PreMiD*.AppImage
```

<a name="appimagenotes"></a>

### Additional notes

Se você quer experimentar o PreMiD ou simplesmente não quer instalá-lo, este é o melhor, está sempre atualizado mas _NÃO AUTO-INICIE COM O SISTEMA!_</br>Se você ficar cansado de ter que abrir cada vez, use os outros pacotes (de acordo com sua distribuição).

<img src="https://raw.githubusercontent.com/PreMiD/Linux/master/.github/packagecloud.png" width="100" height="100" align="right"></img>
<a name="packagecloud"></a>

# PackageCloud

We released deb/rpm packages at our packagecloud repo. Please visit it at https://packagecloud.io/PreMiD/Linux and download your deb/rpm package or use automatic script.

For **Ubuntu/Debian**:

```bash
curl -s https://packagecloud.io/install/repositories/PreMiD/Linux/script.deb.sh | sudo bash
```

For **Fedora/CentOS/RedHat**:

```bash
curl -s https://packagecloud.io/install/repositories/PreMiD/Linux/script.rpm.sh | sudo bash
```

If command doesn't work, download **deb/rpm** file from our packagecloud repo or override settings.

<a name="arch"></a>
<img src="https://raw.githubusercontent.com/PreMiD/Linux/86ae2fbd49499785281f388a5305b06e0d3ecfea/.github/iusearchbtw.svg" width="100" height="100" align="right"></img>

## Distribuições baseadas em Arch Linux

Usando o [repositório do usuário Arch](https://aur.archlinux.org/packages/premid);</br> Distribuições suportadas são _em si_, Manjaro, Anarchy, Artix, Arco, ArchLabs, Endeavour, Archman, BlackArch, Liri OS e [todos que suportam a instalação por AUR](https://wiki.archlinux.org/index.php/Arch-based_distributions#Active).

<a name="archinstall"></a>

### Installation instructions

```bash
# Usando yay (recomendado)
yay -S premid
```

```bash
# Usando o pagkku
pakku -S premid
```

```bash
# Usando trizen
trizen -S premid
```

```bash
# Usando pacaur
pacaur -S premid
```

```bash
# ... você entende o ponto
```

ou manualmente do [Repositório de Usuários Arch](https://aur.archlinux.org/packages/premid) se você for um usuário experiente.

<a name="archnotes"></a>

### Additional notes

Se sua distribuição usa pacman, você deve instalar um dos ajudantes primeiro. Se você não tiver nenhum, é recomendado o Yay, execute :

```bash
git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si
```

```bash
yay -S premid
```

Outros AUR/Pacman helpers também funcionam bem, embora a funcionalidade de cada um deles seja diferente para que você possa enfrentar problemas enquanto os utiliza.
