---
title: Semaine 6 - Partage SMB
author: "Dany Gagnon"
numbersections: true
autoEqnLabels: true
---

# Semaine 6 - Partage SMB

**Auteur: Dany Gagnon**

## Partage sur windows (j'ai choisis l'option 1, 2 et 3) avec un extra (Macbook)

Le SMB est le nom du protocole de partage (de dossiers, notamment) sur un réseau
Windows. On l'appelle aussi parfois CIFS (common internet file system). CIFS fait généralement référence à la version 1 de SMB. [@pierre2021smb, p. SMB]

On va essayer le partage sécurisé avec l'option `turn on password-protected` activée

Dans le terminal `cmd`, on va entrer la commande-

```cmd
compmgmt.msc
```

![Image montrant que le compmgmt.msc à ouvert une fenêtre](../assets/ddany_kQ5x16DaXg.png)

### Créer un utilisateur local


Ensuite, la fenêtre ouverte, je me suis rendu compte que `Local Users and Groups` n'est
pas la. J'ai ensuite découvert qu'il faut écrire la commande-

```cmd
netplwiz
```

Cette command va ouvrir la page de `Local Users and Groups`-

![Résultat de la commande netplwiz](../assets/ddany_9QaYbjpt7k.png)

On clique sur Add et on ajoute un utilisateur avec une interface graphique.

L'option terminal est mieux à mon avis, car on n'a pas à
cliquer sur pleins de trucs pour refuser que microsoft créer un compte
en ligne pour se connecter. Je trouve que c'est beaucoup plus simple, facile
et ça prend moins de temps.

On entre dans `cmd` la commande-
```cmd
net user <USER_NAME> <PASSWORD> /add
```
ou le **<USER_NAME>** est le nom d'utilisateur souhaité et le **<PASSWORD>** est le
mot de passe.

![Image montrant qu'il faut avoir les privilège administrateur pour pouvoir créer un compte](../assets/ddany_QeT8IDAqXB.png)

*PS: Il n'y a pas de commande `sudo` dans `cmd`, donc on doit l'ouvrir en mode administrateur*

![Image montrant que l'utilisateur Gagn a bien été crée](../assets/ddany_ycit2b63LZ.png)

On peut voir que en haut du terminal, le mot __Administrator__ apparait pour s'assurer que le terminal
est belle est bien en mode administrateur.

Vu qu'on créer un compte limité, on ne fait plus rien. Si on aurait voulu
créer un compte et le rendre administrateur, on aurait à écrire la commande-
```
net localgroup administrators <USER_ACCOUNT> /add
```

Ou le **<USER_ACCOUNT>** est le nom d'utilisateur à mettre dans le groupe.
Dans mon cas, ça aurait été **Gagn**.

![Image montrant que Gagn est belle et bien créer dans le groupe des Users](../assets/ddany_Eb76lUNODp.png)

### Paramètres par défauts

Ensuite on s'assure que l'option `File and printer sharing` est activé

![Image montrant que le File and printer sharing est activé](../assets/rtrF5rSS0p.png)

Ensuite on veut aussi s'assurer que le `password-protected sharing` est activé

![Image montrant que le Password-protected sharing est activé](../assets/ddany_ztXfDCFprz.png)

### Création du partage

Pour partager un dossier, j'ai choisis mon dossier nommé **cegep** qui contient mes projets
de cégep dans les cours. Si on veux que tout le monde puisse y accéder, on peut mettre l'option
everyone à `Read/Write`.

![Image qui démontre que tout le monde a accès au dossier cegep](../assets/ddany_0EPK8fkZLt.png)

Pour avoir le nom de la machine, on entre la commande-
```cmd
hostname
```

Pour moi, le hostname est: **DESKTOP-RFOC115**

![Preuve de la command hostname qui retourne le hostname](../assets/ddany_ivv1SCLrrX.png)

Donc si on entre **\\\\DESKTOP-RFOC115**

![On peut avoir accès au dossier partagé](../assets/ddany_V9wJdz3xCK.png)

![Image montrant le \\DESKTOP-RF0C115](../assets/ddany_NiCnqd1x3p.png)

Maintenant, c'est assez inutile de créer un arborescence juste pour accéder
à un dossier. On peut aller dans le **Advanced Sharing** pour changer le *path* du réseaux.

![Image montrant le Advanced Sharing](../assets/ddany_Mu5rT3zmIZ.png)

Ensuite, on peut voir que dans **\\\\DESKTOP-RFOC115** on a un dossier *cegep* qui
contient le dossier partagé.

![Image montrant que le network contient un dossier cegep](../assets/ddany_egc9LaFujr.png)

### Connection sur Macbook

Sur mon Macbook, je suis allé dans Réseaux, et je me suis connecté avec le compte **Gagn** avec le mots de passe **abc**
![Image montrant le dossier desktop-rfoc115 sur mon macbook](../assets/242981790_212588330964899_2426574694047331329_n.png)

Ensuite je suis entré dans le dossier cegep pour vous montrer le contenu
et prouver que j'ai belle est bien accès aux dossiers.

![Preuve montrant que j'ai bien accès au dossier du dossier partagé cegep](../assets/243158197_581300226355300_6843329348035995356_n.png)

### Connection sur l'utilisateur local de Windows

Je vais aussi prouver que j'ai accès avec mon autre utilisateur en me connectant dessus.

![Image montrant que j'ai aussi accès sur mon utilisateur local](../assets/explorer_lvxzPky8jg.png)

### Connection sur iPad

Ensuite, j'ai téléchargé [Lan Drive](https://play.google.com/store/apps/details?id=fr.webrox.landrive&hl=fr_CA&gl=US) sur mon iPad et j'ai réussi
à me connecter

![Preuve que l'application a détecté mon desktop-rfoc115](../assets/244520306_432901081535103_533837551005286358_n.jpg)

Gagn avec le mots de passe abc sur le port TCP *445*

![Image montrant la connection](../assets/245199319_405869934518153_489237348799307642_n.jpg)

Ensuite j'ai accès au dossier cegep avec mes sous-dossiers

![Image montrant que j'ai réussi à accèder mon dossier partagé sur un ipad](../assets/245266057_948171632716714_5321425024500519828_n.jpg)

## Partage de Windows à Linux

Pour faire le partage de Windows et se connecter à partir un ordinateur
Linux est simple. Il y a deux façons distincte de se connecter (soit par un
interface graphique ou par la ligne de commande). Je préfère l'option du
terminal. Pour débuter, on va utiliser la commande `smbclient`. Pour l'installer,
on va utiliser la commande-

```bash
# apt install smbclient
```

![Image montrant que j'ai réussi à me connecter sur le compte Gagn et avoir accès au dossier cegep](../assets/ddany_scbs3N52ic.png)

Ensuite, j'ai essayé de monter le dossier sur mon dossier **Backup**. Mais j'ai reçu l'erreur
suivante-

![Image montrant l'erreur qui reconnait pas le smbfs](../assets/ddany_ayumDJr4ue.png)

Suite à l'erreur, j'ai exécuter la commande-
```bash
# apt install cifs-utils
```

Se qui ma permis de monter les dossier cegep sur le chemin
`~/Backup`.

![Image montrant la commande pour monter le dossier](../assets/ddany_lkFI4LhPnF.png)

Pour prouver que le dossier est
correctement monté, je vais exécuter la commande-

```bash
ls ~/Backup
```

![Image qui prouve que le dossier ~/Backup/ contient les dossiers de cegep](../assets/ddany_zb1fv0PdEy.png)

Malheureusement, si on repart la machine, il va falloir recommencer les étapes pour avoir accès au dossier
**cegep** sur le dossier **Backup**.

Pour contrer à ça, on va le monter au démarrage. Pour monter un disque au démarrage,
on modifie le fichier fstab. On peut le modifier avec `nano` en exécutant la commande-
```bash
# nano /etc/fstab
```

*Ps: il faut être sudo*

![Image de mon /etc/fstab](../assets/ddany_lEgGEivpEB.png)

Pour vérifier que tout fonctionne, on va lancer la commande-
```bash
# mount -a
```

Pour ma part, j'ai eu une erreur qui disait qu'il ne pouvait pas résoudre `desktop-rfco115` car
j'ai fait une erreur de typo. Je l'ai ensuite changer pour le bon `hostname`

![Image qui montre que j'ai corriger la faute dans le fichier /etc/fstab](../assets/ddany_77fT00BioM.png)

![Image qui montre que tout c'est bien passé](../assets/ddany_417h5NBRs1.png)

Maintenant que tous fonctionne, je vais vérifier si le cadenas dans l'interface utilisateur
est présent.

![Preuve que le cadenas est bien présent](../assets/ddany_GVokYdOx6z.png)

Bref, on a vu le parcours de la connection sur un dossier partagés Windows. On a vu comment s'y
connecter à partir de plusieurs appareils (Macbook, iPad, iPhone, Windows et Linux). J'ai trouvé
ça très intéressant et j'ai été surpris par comment facile c'était se connecter sur un dossier
partagé.

-Dany Gagnon