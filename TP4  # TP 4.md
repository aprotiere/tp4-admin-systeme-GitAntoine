 # TP 4 Utilisateurs, groupes et permissions antoine chavée

<h1>Exercice 1. Gestion des utilisateurs et des groupes</h1>

<ol>
<li><h2>Commencez par créer deux groupes groupe1 et groupe2<h2></li>

*création d'utilisateur*

 >`sudo adduser antoine`

*ajout groupe*

 >`sudo addgroup ics`
 >`sudo groupadd ics`

<li><h2>Créez ensuite 4 utilisateurs u1, u2, u3, u4 avec la commande useradd, en demandant la création de
leur dossier personnel et avec bash pour shell
</h2></li>

*création d'un utilisateur u1 avec son dossier personnel et Sélectionne le shell à utiliser pour exécuter les commandes du terminal*

 >`-m => création du dossier personnel`

  >`--shell => indique l 'éxécution avec le bash`

 >`sudo useradd u1 -m --shell /bin/bash`

<li><h2>Placez les utilisateurs dans les groupes :
- u1, u2, u4 dans groupe1
- u2, u3, u4 dans groupe2
</h2></li>

*- Ajouter un utilisateur existant à un groupe (secondaire) existant*

>`usermod -a -G groupe1 u1`

<li><h2>Donnez deux moyens d’afficher les membres de groupe2</h2></li>

*affiche grace au chemin et a la commande grep qui récupère la valeur "groupe"*

>`cat etc/group | grep "groupe2"`

*installation du packet members pour afficher les nembres du groupes*

>`members "groupe2"`

<li><h2>Faites de groupe1 le groupe propriétaire de /home/u1 et /home/u2 et de groupe2 le groupe propriétaire
de /home/u3 et /home/u4</h2></li>

*chown est la commande qui modifier  le propriétaire du fichier ici groupe1 deviens prop du fichier u2  *

>`chown  :groupe1 /home/u2`

<li><h2>Remplacez le groupe primaire des utilisateurs :
- groupe1 pour u1 et u2
- groupe2 pour u3 et u4</h2></li>

*usermod permet modifier le groupe primaire d’un utilisateur*

>`sudo usermod -g groupe1 u1,u2`

<li><h2>Créez deux répertoires /home/groupe1 et /home/groupe2 pour le contenu commun aux groupes, et
mettez en place les permissions permettant aux membres de chaque groupe d’écrire dans le dossier
associé</h2></li>

*création d'un fichier groupe1*

>`sudo mkdir group1`

*chmod permet de modifier les droits existant sur
les fichiers 1 grace au valeur numérique 770 on donneras les droits sur se dossiers*

>`chmod 770 groupe1`

<li><h2>Comment faire pour que, dans ces dossiers, seul le propriétaire d’un fichier ait le droit de renommer
ou supprimer ce fichier ?
</h2></li>

*grace a sticky bit  que seul les propriétaire de se fichiers peuvent le modifier ect ici le propriétaire de se fichier est groupe1 donc tout les nembres du groupe 1 peuvent le modifier*

>`chmod +t groupe1`


<li><h2>Pouvez-vous vous connecter en tant que u1 ? Pourquoi ?</h2></li>

*avec su on prend l’identité de quelqu’un d’autre, pas avec sudo*

>`su u1`

*non car nous n'avons pas configurer de mot de passe*

<li><h2>Activez le compte de l’utilisateur u1 et vérifiez que vous pouvez désormais vous connecter avec son
compte</h2></li>

*Nous allons configurer un mpd au compte*

>`sudo passwd u1`

*on vérifie en se connectant*

>`su u1`

<li><h2>Quels sont l’uid et le gid de u1 ?
</h2></li>

*grace id nomUtilisateurs nous allons récupérer sont id*

>`id u2`

<li><h2>Quel utilisateur a pour uid 1003 ?</h2></li>

*on utilise la commande getent pour rechercher dans un groupe la personne qui a pour uid=1003*

>`getent group groupe1 1004`

<li><h2>Quel est l’id du groupe groupe1 ?</h2></li>

*soit on utilise getent pour récupérer l'id du groupe soit on se déplace dans le dossier groupe pour regarder sont id*

>`getent group groupe1`

<li><h2>Quel groupe a pour guid 1002 ?</h2></li>

*grace a getent il suffit de renseigner l id du group pour qu'il nous le trouve*

>`getent group 1003`

<li><h2>Retirez l’utilisateur u3 du groupe groupe2. Que se passe-t-il ? Expliquez.</h2></li>

*la commande gpasswd est utilisée pour  administrer les groups donc remove ect -d = delete*

>`sudo gpasswd -d u3 groupe1 `

*on ne peut pas enlever sont utilisateur car c'est sont unique groupe*

<li><h2>Modifiez le compte de u4 de sorte que :
— il expire au 1
er juin 2020
— il faut changer de mot de passe avant 90 jours
— il faut attendre 5 jours pour modifier un mot de passe
— l’utilisateur est averti 14 jours avant l’expiration de son mot de passe
— le compte sera bloqué 30 jours après expiration du mot de pass</h2></li>

*--expiredate = set date*

*chage -m = set j update mdp*

*chage -w = set j expire mdp*

*chage -I = set j compte bloqué*

<code>
sudo usermod --expiredate 2020-06-01 u4
sudo chage -m 90 u4
sudo chage -W 14 u4
sudo chage -I 30 u4
</code>

<li><h2>Quel est l’interpréteur de commandes (Shell) de l’utilisateur root ?</h2></li>

</ol>
