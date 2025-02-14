---
title: Dépannage
description: Tout pour résoudre votre problème
published: true
date: 2021-12-20T14:27:18.034Z
tags:
editor: markdown
dateCreated: 2021-09-07T01:17:32.312Z
---

> Assurez-vous d'avoir l'extension **et** l'application installée! 
> 
> {.is-warning}

Inclus sur cette page :
1. [Dépannage général](https://docs.premid.app/troubleshooting#general)
2. [Dépannage sur Linux](https://docs.premid.app/troubleshooting#linux)
3. [Dépannage sur MacOS](https://docs.premid.app/troubleshooting#macos)

<a name="general"></a>

# Dépannage général
> Vous pouvez utiliser [cet](https://qkeleq10.github.io/PreMiD-Troubleshooting/) outil pour vous aider à mieux cibler votre problème. 
> 
> {.is-info}
### Recharger la page
Vous pouvez aussi appuyer sur <kbd>CTRL+R</kbd>/<kbd>F5</kbd> (Windows) ou <kbd>CMD+R</kbd> (MacOS) sur votre clavier au lieu de rechercher le bouton de rafraîchissement.

### Utilisez-vous l'application Discord ?
PreMiD ne fonctionne **pas** avec la version navigateur de Discord, vous devez télécharger l'application [ici](https://discord.com/download).

### Assurez-vous d'avoir activé l'activité de jeu Discord dans les paramètres
**Paramètres utilisateur** > **Activité de jeu**
<img src="https://i.imgur.com/9SfrrWm.png" width="500px" style="max-width:100%;" />

### Assurez-vous que Discord n'ai PAS été lancé en tant qu'administrateur
Très important. La RichPresence Discord ne marchera pas si vous exécutez Discord en tant qu'administrateur.

### Utilisez-vous une presence avec des paramètres ?
De nombreuses présences (dont `Twitch` et `SoundCloud`) sont affectées par un problème dû à l'extension. Ce problème empêche l'extension de récupérer les valeurs par défaut des paramètres.

Pour résoudre ce problème, il vous suffit d'activer/désactiver le paramètre le plus haut :
<img src="https://i.imgur.com/JtXxTzg.gif" width="500px" style="max-width:100%;" />

### Redémarrez votre navigateur
<kbd>Alt</kbd>+<kbd>F4</kbd> (Windows) ou <kbd>CMD</kbd>+<kbd>Q</kbd> (MacOS) marche aussi. (Vous devez redémarrer votre navigateur, évidemment.)

### Redémarrer PreMiD (l'application)
<img src="https://i.imgur.com/wQA15xu.png" width="500px" style="max-width:100%;" />
Vous devez redémarrer PreMiD par la suite.

### Recharger/redémarrer Discord
Appuyez sur <kbd>CTRL+R</kbd> (Windows) ou <kbd>CMD+R</kbd> (MacOS) sur votre clavier ou redémarrez Discord manuellement.

### Vérifiez si vous avez un antivirus ou un pare-feu en cours d'exécution sur votre ordinateur
Quelquefois, les antivirus et les pare-feu bloquent les applications qui créent/hébergent des serveurs ou qui se connectent simplement à Internet. Nous utilisons un serveur local pour intercepter et transférer les données entre l'application et l'extension donc si vous empêchez l'application de transférer les données, il se pourrait que vous ne puissiez pas utiliser PreMiD.

### Désactivez vos extensions
Désactivez toutes vos extensions et voyez si ça marche. Si ça marche, essayez d'activer vos extensions une par une et dites-nous laquelle empêche PreMiD de fonctionner.

### Redémarrez votre ordinateur
J'espère que vous savez comment redémarrer un ordinateur.

### Réinstallation de PreMiD
Parfois, il y a un problème avec les fichiers... Des tutoriels pour l'installation peuvent être trouvés [ici](/install).

### Suppression manuelle
Windows : Écrivez `%appdata%` dans la barre d'adresse de l'explorateur de fichiers et supprimez le dossier `PreMiD`. MacOS : `~/users/USER/~Librairy/Application Support/` et supprimez le dossier `PreMiD`.

### McAfee a détecté PreMiD comme un virus (Windows)
C'est un faux positif de la part de McAfee et nous leur avons signalé le problème, pour l'instant, vous pouvez exclure PreMiD de l'analyse en effectuant les étapes suivantes :

> Si vous ne vous sentez pas confiant de prendre ces mesures, n'hésitez pas à faire un ticket dans [#support](https://discord.premid.app/) et l'un de nos agents de support pourra vous aider ! 
> 
> {.is-warning}

1. Ouvrez l'application McAfee et cliquez sur l'icône Paramètres en haut à droite. <img src="https://i.imgur.com/rPLZn6c.png" width="500px" style="max-width:100%;" />
2. Cliquez sur "Objets en quarantaine" (Le second à partir du haut).
3. Développez-le, et cliquez sur l'icône `>` avant un élément avec le nom "settings.dat".
4. Assurez-vous que le chemin inclut "AppData\Local\Temp\PreMiD", si c'est le cas, sélectionnez-le et appuyez sur restore. <img src="https://i.imgur.com/9nvHmiI.png" width="500px" style="max-width:100%;" />
5. Une fois restauré, vous pouvez fermer la fenêtre pop-up "Éléments en quarantaine", puis appuyer à nouveau sur l'icône de paramètres en haut à droite.
6. Cliquez sur "Analyse en temps réel" (Troisième à partir du haut).
7. Développez-le et cliquez sur "Ajouter un fichier".
8. Tapez "%appdata%" dans la barre d'adresse du gestionnaire de fichiers et appuyez sur Entrer. <img src="https://i.imgur.com/2bchwLe.png" width="500px" style="max-width:100%;" />
9. Ouvrez le dossier "PreMiD", sélectionnez le fichier "PreMiD.exe" et cliquez sur Ouvrir. <img src="https://i.imgur.com/aHOyv3V.png" width="500px" style="max-width:100%;" />
10. McAfee devrait maintenant ignorer notre dossier, lancez simplement l'application et cela devrait marcher.

### PreMiD status bugged on Discord
Ne vous inquiétez pas. Appuyez sur <kbd>CTRL+R</kbd> (Windows) ou <kbd>CMD+R</kbd> (MacOS) tout en restant sur Discord pour recharger l'application.

<a name="linux"></a>

# Dépannage sur Linux
### Distributions basées sur Ubuntu/Debian
Si vous avez téléchargé Linux à partir de Snapcraft, la RichPresence ne marchera pas. Vous devez désinstaller la version Snapcraft en exécutant la commande `sudo snap remove discord` dans un terminal, ensuite téléchargez **[Discord pour Linux](https://discordapp.com/api/download?platform=linux)** (**[ou Discord Canary](https://discordapp.com/api/canary/download?platform=linux)**) et naviguez à l'emplacement où vous avez téléchargé Discord (généralement, il se trouve dans le dossier `$HOME/Downloads/`) puis installez le package en utilisant `sudo dpkg -i discord-*.deb`. Si l'AppImage ne fonctionne pas, vous devriez jeter un œil à nos autres packages **[ici](https://packagecloud.io/premid/linux)**.

### Distributions basées sur Arch Linux
Les distributions basées sur Arch Linux devraient utiliser le package <code>premid</code> ou le package <code>premid-git</code> fournis dans l'AUR (Arch User Repository), (<em x-id="3">ATTENTION : ce packet compile PreMiD directement depuis son code source.</em>). Si vous ne voulez pas installer un AUR manager (yay, etc.), vous pouvez utiliser notre AppImage qui est téléchargeable depuis notre <strong x-id="1"><a href="https://github.com/premid/linux/releases">dépôt Linux</a></strong>.
<em x-id="3">Attention : le paquet dans l'<strong x-id="1">AUR</strong> n'est pas maintenu par nous (en tant que PreMiD), mais par d'autre personnes.</em>

### Liaison aux ports
Vous devez savoir que <strong x-id="1">PreMiD</strong> se lie au port <strong x-id="1">3020</strong>. Ceci est nécessaire pour que l'Extension et l'Application puissent communiquer. Si <strong x-id="1">PreMiD</strong> vous montre une erreur à propos de ce port, vous devez vérifier si un processus est lié au port 3020 en exécutant la commande <code>sudo lsof -i:3020</code> ou <code>sudo netstat -tnlp | grep :3020</code> dans votre terminal. Si une processus est lié à ce dernier, vous devrez faire en sorte de libérer le port et relancer <code>PreMiD</code>.

### L'AppImage de PreMiD ne se lance pas au démarrage
Comme précisé dans notre **dépôt Linux**, AppImage ne peut pas être démarré lors de l'ouverture de session. Vous pouvez faire en sorte que cette dernière se lance au démarrage manuellement en suivant ces étapes :
1. Créez un fichier nommé <strong x-id="1">rc.local</strong> dans le dossier <code>/etc/</code>.
2. Ouvrez ce fichier dans votre éditeur favori et collez-y le code suivant en modifiant le dossier dans lequel l'AppImage est située :
```bash
#!/bin/bash
# Nécessaire pour s'exécuter en tant /bin/bash (si vous utilisez zsh etc. vous pouvez le changer.)

# Exemple: /home/PreMiD/PreMiD*.AppImage
<directory to appimage>/PreMiD*.AppImage

exit 0
```
3. Sauvegardez le fichier et rendez le exécutable avec la commande `sudo chmod a+x /etc/rc.local`.
4. Redémarrez votre PC et l'AppImage de PreMiD devrait se lancer au démarrage.

<a name="macos"></a>

# Dépannage sur MacOS
### Erreur lors de la création du dossier
<img src="https://i.imgur.com/td92lf6.png" width="300px" style="max-width:100%;" />

Si vous obtenez cette erreur, cela veux dire que votre compte n'a pas les permissions administrateur, vous devez donc créer un dossier manuellement en suivant ces étapes :
1. Ouvrez Finder et ouvrez le dossier **Applications**.
2. Faites un clic droit dans un espace vide et cliquez sur **Créer un dossier**.
3. Assignez le nom `PreMiD` à ce dossier (la casse est importante, n'oubliez pas les majuscules).
4. Réouvrez l'installateur.

# Cela n'a pas résolu mon problème
Veuillez ouvrir un ticket dans [#support](https://discord.premid.app/).
