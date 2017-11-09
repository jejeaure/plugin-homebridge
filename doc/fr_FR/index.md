= Plugin HomeBridge

== Présentation HomeBridge

*Le plugin Homebridge* est un demon qui permet d’interagir avec un système domotique via l’assistant vocal Siri sous iOS. Le HomeKit a été introduit depuis iOS 8, mais est véritablement opérationnel depuis iOS 10 via l’application Maison. 

image::../images/homekit-logo.jpg[]

Le plugin Homebridge de Jeedom permet donc d’exposer des équipements Jeedom qui seront vus comme des accessoires compatibles au protocole *HomeKit*.

[IMPORTANT]
*Homebridge n'est pas officiellement supporté par Apple. A tout moment Apple peut bloquer ce protocole.*

===  Que peut-on faire avec HomeBridge ?

Homebridge peut s'utiliser avec une application compatible HomeKit ou avec l'assistant vocal Siri.

Depuis iOS 10, l'application Maison (inclue par défaut avec iOS) permet le pilotage d'équipements compatibles HomeKit. 

image::../images/cuisine-homekit.jpg[]

Les équipements peuvent être classés par pièce.

image::../images/piece-homekit.jpg[]

Beaucoup d'accessoires sont pris en charge.

image::../images/garage-homekit.png[]

Siri peut aussi interagir. Il répond aux questions : 


image::../images/siri-01.jpg[]

Siri peut également faire des actions : 

image::../images/siri-02.jpg[]

HomeKit à l'avantage d'être utilisable à l'extérieur du domicile. Seule condition: il faut disposer d'un concentrateur. 
L'iPad et l'AppleTV (et bientôt le HomePod) peuvent servir de concentrateur. Pour cela, ils doivent être connectés au même compte iCloud.


[TIP]
*HomeKit est le nom officiel du protocole développé par Apple. Homebridge est son équivalent Open Source développé par nfarina. Ce dernier a étendu le projet HAP-NodeJS qui est le moteur d'Homebridge.*

===  Type d'accessoire compatible avec HomeKit (on les ajoutera peu à peu à HomeBridge)

image::../images/acchb.jpg[]

== Installation et activation du plugin Homebridge

Le plugin Homebridge doit être installé via le market Jeedom. *Le plugin App Mobile officiel n'est plus indispensable.*

*Pour les migrations depuis le plugin App Mobile officiel, il est important de ne pas désactiver le plugin App Mobile. Une rubrique "Migration depuis le plugin App Mobile" est disponible dans la documentation.* 

image::../images/pluginHB.png[]

Un fois le plugin installé, il suffit de l'activer en cliquant sur "Activer".

image::../images/activationHB.png[]

===  Installation des dépendances

Les dépendances sont installées automatiquement par Jeedom dans les 5 min. Elles seront également réinstallées lors d'une mise à jour du plugin si besoin.

image::../images/installationDep.png[]

*Le temps d'installation des dépendances peut varier en fonction du matériel utilisé.*

*Systèmes compatibles avec Homebridge :*

* Raspberry Pi 2 et 3 (Le Pi 3 est conseillé)

* Box Jeedom Mini +

* Box Jeedom pro

* Box Jeedom smart

* Box Jeedom pro V2

* Tout système basé sur Debian 8 ou 9

[IMPORTANT]
*Les installations sous Docker et Raspberry Pi 1 ne sont pas compatibles avec cette version de Homebridge.*

Une fois les dépendances installées, le démon se lance (dans les 5 min). Si le statut n'est pas sur "OK", il faut cliquer sur "(Re)Démarrer".

image::../images/demon-homebridge.png[]


=== Mise à jour manuelle des dépendances

Pour mettre à jour manuellement les dépendances, il faut cliquer sur "Relancer".

image::../images/dependances-homebridge.png[]

=== Fichiers LOG

Les fichiers log permettent d'analyser pas à pas l'activité interne du processus et ses interactions avec son environnement.

Ces fichiers peuvent être nécessaires en cas de disfonctionnement du plugin.

image::../images/log.png[]

* Homebridge : Historise toutes les communications avec le démon homebridge.

* Homebridge_daemon : Historise les actions effectuées par Homebridge (par exemple si un accessoire est envoyé à Homebridge mais n'apparait pas dans l'application Maison, c'est ici qu'il faut aller voir).

* Homebridge_dep : Historise toutes les étapes de l'installation des dépendances. Si le démon refuse de démarrer par exemple, un coup d'oeil peut aider).

== Configuration du plugin Homebridge

=== Création du pont Homebridge

Pour créer le pont Homebridge, il faut aller dans la rubrique "Gestion", et cliquer sur "Configuration".

image::../images/gestion.png[]

Pour créer le pont, il suffit de lui donner un nom et un code "PIN".

image::../images/config-pluginhb.png[]

* *Utilisateur* : Permet à Homebridge d'utiliser l'ApiKey d'un utilisateur d'une box Jeedom.

* *Nom Homebridge* : Permet de nommer le pont Homebridge. 

[IMPORTANT]
Le changement de nom Homebridge obligera à reconfigurer les applications HomeKit.

* *PIN Homebridge* : Permet de personnaliser le code PIN Homebridge.

[IMPORTANT]
Les PIN suivants ne sont pas acceptés par Apple : 000-00-000, 111-11-111, 222-22-222 -> 999-99-999, 123-45-678, 876-54-321. Son changement obligera la reconfiguration des applications HomeKit.

* *Réparer* :  Permet une réparation de Homebridge en modifiant les identifiants. 

[IMPORTANT]
Il faut retirer le bridge de l'application "Maison".

* *Réparer & réinstaller* : Supprime et réinstalle complètement Homebridge. 

[IMPORTANT]
A n'effectuer que sur conseil d'un membre du forum et il faut retirer le pont de l'application "Maison".

* *Plateforme Homebridge supplémentaire* : Permet de rajouter manuellement un équipement.

[IMPORTANT]
Réservé à un public averti. Il n'y aura aucun support pour cette partie (permet par exemple d'ajouter des cameras à Homebridge).

Une fois les cases *Utilisateur, nom Homebridge et PIN Homebridge* correctement renseignées, la configuration se finalise en cliquant sur **Sauvegarder**. Le démon redémarre.

=== Ajout des accessoires dans Homebridge

Les équipements seront à ajouter manuellement. 

image::../images/config-piece.png[]

Afin d'intégrer un accessoire dans Homebridge, il faut sélectionner la pièce où il se trouve.

image::../images/choix-acc.png[]

Afin d'ajouter un accessoire à Homebridge, il suffit de cocher la case "Envoyer à Homebridge". Pour sauvegarder, il suffit de cliquer sur la petite disquette verte.

==== Configuration des types génériques

===== Généralités

En cliquant sur l'équipement, les types génériques utilisés pour la communication entre votre Jeedom et Homebridge apparaissent.

image::../images/typegen-1.png[]

La majorité des types génériques est déjà renseignée. Dans certains cas, une configuration manuelle sera nécessaire (pour le plugin Virtuel par exemple).

Voici les types génériques disponibles : 

Pour les informations : 

image::../images/typeginfo.png[]

Pour les actions : 

image::../images/ypegeaction.png[]

===== Lumières
[options="header",cols=",^m,"]
|===
| Type générique | Obligatoire | Valeurs possibles 
| Info/Lumière Etat (Binaire)| NON | Ajout pour les lumières

dont la luminosité ne change pas

lorsqu'elle est éteinte (Yeelight, Ikea, ...)

0 = Eteint 

autre que 0 = Allumé
| Info/Lumière Etat | OUI | Luminosité

0-100 ou 0-99 ou 0-255

(en fonction du max de Action/Lumière Slider)

ou Binaire

0 = Eteint

autre que 0 = Allumé 
| Action/Lumière Slider

(Luminosité)
| OUI | Réf. vers Lumière Etat
| Action/Lumière Bouton On | OUI | Réf. vers Lumière Etat :

- Binaire s'il est présent

- Etat sinon
| Action/Lumière Bouton Off | OUI | Réf. vers Lumière Etat :

- Binaire s'il est présent

- Etat sinon
| Info/Lumière Couleur| NON | Format #RRGGBB
| Action/Lumière Couleur| Si Info/Lumière Couleur | Réf. vers Info/Lumière Couleur
| Info/Lumière Température Couleur| NON | Numérique (Kelvin)

(en fonction du min-max de Action/Lumière Température Couleur)

(Eve Seulement)
| Action/Lumière Température Couleur| Si Info/Lumière Température Couleur | Réf. vers Info/Lumière Température Couleur

(Eve Seulement)
| Action/Lumière Toggle | NON Utilisé | N/A
| Action/Lumière Mode | NON Utilisé | N/A
|===

===== Prises
[options="header",cols=",^m,"]
|===
| Type générique | Obligatoire | Valeurs possibles 
| Info/Prise Etat | OUI | 0 = Eteint 

1 = Allumé
| Action/Prise Bouton On | OUI | Réf. vers Info/Prise Etat
| Action/Prise Bouton Off | OUI | Réf. vers Info/Prise Etat
| Action/Prise Slider | NON Utilisé | N/A
|===

===== Volets
[options="header",cols=",^m,"]
|===
| Type générique | Obligatoire | Valeurs possibles 
| Info/Volet Etat | OUI | 0 = Fermé 

>95 = Ouvert
| Action/Volet Bouton Monter | Si Descendre | Réf. vers Info/Volet Etat
| Action/Volet Bouton Descendre | Si Monter | Réf. vers Info/Volet Etat
| Action/Volet Bouton Stop | NON Utilisé | N/A
| Action/Volet Bouton Slider | Si Seul | Réf. vers Info/Volet Etat
|===

===== Volets BSO
Pas encore supportés

===== Chauffage fil pilote
N'existe pas en HomeKit

===== Serrures
[options="header",cols=",^m,"]
|===
| Type générique | Obligatoire | Valeurs possibles 
| Info/Serrure Etat | OUI | pas 1 = Non Sécurisée 

1 = Sécurisée
| Action/Serrure Bouton Ouvrir | OUI | Réf. vers Info/Serrure Etat
| Action/Serrure Bouton Fermer | OUI | Réf. vers Info/Serrure Etat
|===

===== Sirènes
N'existe pas en HomeKit

===== Thermostats
[options="header",cols=",^m,"]
|===
| Type générique | Obligatoire | Valeurs possibles 
| Info/Thermostat Etat (BINAIRE) | NON | 0 = Eteint 

1 = Allumé
| Info/Thermostat Etat (HUMAIN) | NON | Générique (Eve Seulement)
| Info/Thermostat Mode | OUI si associé mode homekit | Générique (Eve Seulement)
| Action/Thermostat Mode | NON | Peut être associé mode homekit
| Info/Thermostat Température Extérieur| NON utilisé | N/A
| Info/Thermostat Température ambiante| NON | -50 -> 100
| Info/Thermostat Consigne| OUI | 10 -> 38
| Action/Thermostat Consigne| OUI | 10 -> 38
| Info/Thermostat Verrouillage| NON | 0 = Non Verrouillé 

1 = Verrouillé
| Action/Thermostat Verrouillage| OUI si Info/Verrouillage | N/A
| Action/Thermostat Déverrouillage| OUI si Info/Verrouillage | N/A
|===

===== Portails ou Garages
[options="header",cols=",^m,"]
|===
| Type générique | Obligatoire | Valeurs possibles 
| Info/Portail état ouvrant

Info/Garage état ouvrant

(même traitement)| OUI | 0 = Fermé 

252 = Fermeture en cours

253 = Stoppé

254 = Ouverture en cours

255 = Ouvert

(Configurable)
| Action/Portail ou garage bouton toggle | OUI | Réf. vers Info/Portail état ouvrant

ou

Réf. vers Info/Garage état ouvrant
| Action/Portail ou garage bouton d'ouverture | NON Utilisé | N/A
| Action/Portail ou garage bouton de fermeture | NON Utilisé | N/A
|===

===== Haut-Parleurs (Eve Seulement)
[options="header",cols=",^m,"]
|===
| Type générique | Obligatoire | Valeurs possibles 
| Info/Haut-Parleur Mute | OUI | 1 = Pas de son 

0 = Son
| Action/Haut-Parleur Mute | OUI | Réf. vers Info/Haut-Parleur Mute
| Action/Haut-Parleur UnMute | OUI | Réf. vers Info/Haut-Parleur Mute
| Action/Haut-Parleur Toggle Mute | Si seul | Réf. vers Info/Haut-Parleur Mute
| Info/Haut-Parleur Volume | NON | %
| Action/Haut-Parleur Volume | OUI si Info/HP Volume | Réf. vers Info/Haut-Parleur Volume
|===

===== Generic
[options="header",cols=",^m,"]
|===
| Type générique | Obligatoire | Valeurs possibles 
| Info/Puissance Electrique | NON | Watts
| Info/Consommation Electrique

(cachée)| NON | KWh
| Info/Température | NON | -50->100 °C 
| Info/Luminosité | NON | 0.0001-> 100000 lux
| Info/Présence | NON | 0 = Pas de mouvement

1 = Mouvement
| Info/Batterie| NON | %
| Info/Batterie en charge| NON | 0 = NON

pas 0 = OUI
| Info/Détection de fumée | NON | pas 1 = Pas de fumée détectée

1 = fumée détectée
| Info/Inondation | NON | pas 1 = Pas de fuite détectée

1 = fuite détectée
| Info/Humidité | NON | %
| Info/Porte

Info/Fenêtre

(même traitement)| NON | pas 1 = Contact

1 = Pas de contact
| Info/Sabotage | NON | 1 = Pas de sabotage

0 = Sabotage
| Info/Choc | NON | Générique (Eve Seulement)
| Info/Pression | NON | Générique (Eve Seulement)
| Info/Son (dB) | NON | Générique (Eve Seulement)
| Info/UV | NON | Générique (Eve Seulement)
| Info/Générique | NON | Valeur <64 charactères 

avec Unité indiquée ou pas

(Eve Seulement)
| Action/Générique 

(N'existe pas en HomeKit)| NON | N/A
| Info/Pluie (accumulation) | NON | Générique (Eve Seulement)
| Info/Pluie (mm/h) | NON | Générique (Eve Seulement)
| Info/Vent (direction) | NON | Générique (Eve Seulement)
| Info/Vent (vitesse) | NON | Générique (Eve Seulement)
| Info/Actif | NON | 0 = inactif

1 = actif
| Info/Defectueux | NON | 0 = non

1 = oui
|===


*Des exemples de configurations sont disponibles à la fin de la documentation*

Pour valider, il faut aller dans la configuration du plugin et relancer le démon Homebridge en cliquant sur "(Re)Démarrer".

image::../images/demon-homebridge.png[]

==== Ajout de Jeedom dans HomeKit

Il existe plusieurs applications sur l'appstore compatibles HomeKit. L'application "Maison" d'Apple sera utilisée pour la rédaction de la documentation.


image::../images/app-domicile.jpg[]

L'inclusion de Jeedom dans HomeKit, se fait en ouvrant l'application "Maison" et en cliquant sur "Ajouter un accessoire".

image::../images/home-1.jpg[]

[TIP]
Dans l'exemple, le domicile s'appelle "Test". Son nom peut être modifié en allant dans les réglages de l'application.

Il faut scanner le code PIN 

image::../images/home-2.jpg[]

[TIP]
*Le code PIN peut être également rentré manuellement en cliquant sur "Code absent ou impossible à scanner ?".*

Il faut sélectionner le pont à inclure.

image::../images/home-3.jpg[]


[IMPORTANT]
Comme expliqué plus haut dans la doc, Homebridge n'est pas reconnu officiellement par Apple. Un message indique que l'accessoire n'est pas certifié, il faut valider l'inclusion en cliquant sur "Poursuivre l'ajout".

image::../images/home-4.png[]

*Le pont Jeedom est maintenant intégré à HomeKit.*

==== Rangement des accessoires dans HomeKit

Les accessoires doivent être rangés correctement dans HomeKit. Il faudra créer des pièces pour y intégrer les accessoires.

[IMPORTANT]
*Les pièces dans Jeedom ne sont pas importées dans Homebridge. Ceci n'est pas dû à Jeedom mais à la gestion des pièces par Apple.*

Le premier accessoire à "ranger" est le pont Jeedom. 

image::../images/home-5.jpg[]

Il faut sélectionner la pièce où sera installé le pont. Si elle n'existe pas, il faudra la créer en cliquant sur "Créer".

image::../images/home-05.jpg[]

Définir le nom de la nouvelle pièce. Il est également possible de lui attribuer un fond d'écran dédié. Pour finaliser la création de la pièce, il faut cliquer sur "Enregistrer".

image::../images/home-051.jpg[]

Maintenant, il ne reste plus qu'à ranger tous les accessoires dans les différentes pièces.

image::../images/home-052.jpg[]

[TIP]
*La fonction "Inclure dans les favoris" permet d'afficher l'accessoire dans la page principale de l'application*

image::../images/home-053.jpg[]

*Les accessoires doivent être "rangés" un par un. Si il y en a beaucoup, cette partie prendra du temps*.

La documentation complète de l'application "Maison" d'Apple est disponible https://support.apple.com/fr-fr/HT204893[ici].

== Migration depuis le plugin App Mobile

Le nouveau plugin Homebridge importe automatiquement la configuration Homebridge du plugin App Mobile. Il n'y a aucune opération à faire. 

Lorsque l'importation est terminée, la rubrique Homebridge disparait des paramètres du plugin App Mobile. 


image::../images/plugnmobilesanshb.png[]

Homebridge est complètement dessolidarisé du plugin App Mobile. Il fonctionne maintenant de manière autonome.

Lors de l'installation du plugin Homebridge, tous les accessoires vont être indisponibles. C'est normal.

image::../images/migration1.png[]

Dès que l'installation des dépendances est terminée, tous les accessoires seront de nouveaux disponibles.


== Troubleshooting

=== Aide Homebridge

==== Support

*Merci de passer par le forum, de créer *un* sujet par demande et de lire les autres sujets s'ils ressemblent au votre (ceux créés après la sortie de ce plugin, c'est logique :-))*

==== Point important

[IMPORTANT]
Les références vers l'état dans les actions sont primordiales !! Sinon pas de lien entre l'état et ses actions possibles.

Pour un "virtuel" : 

image::../images/reference-etat.png[]

Pour un accessoire physique (Dimmer 2 de Fibaro par exemple) : 

image::../images/ref2.png[]

==== FAQ

*-> Le pont Homebridge n'apparait pas dans l'application Maison !*

TIP: Vérifiez que vous êtes connectés au même réseau que le pont Homebridge et que les fonctions Igmp snooping ou dns multicast sont activées sur votre box, routeur ou switch. Le protocole HomeKit n'est pas routable.

*-> Je n'arrive pas à inclure Jeedom dans HomeKit !*

TIP: Vérifiez que le statut du démon Homebridge est sur OK.

image::../images/demonHB.png[]

TIP: Pour inclure votre Jeedom dans HomeKit, via une application compatible (par exemple Maison ou Eve), vérifiez que votre appareil iOS est connecté au même réseau que votre Jeedom.

image::../images/config-pluginhb.png[]

*-> Le démon Homebridge ne veut pas démarrer !*

TIP: Vérifiez que vous disposez de la dernière version des dépendances. En cas de doute, il est possible de les réinstaller en cliquant sur "Relancer". Si la réinstallation des dépendances ne fonctionne pas ou indique une erreur dans le log des dépendances, cliquez sur "Réparer et Réinstaller".

image::../images/dependances-homebridge.png[]

*-> Mon équipement n'apparait pas dans Homebridge !*

TIP: Vérifiez que la case "Envoyer à Homebridge" est cochée dans la configuration du plugin Homebridge.

*-> La case "Envoyer à Homebridge" est bien cochée mais mon équipement n'apparait toujours pas !*

TIP: Vérifiez dans la configuration de votre équipement que celui-ci est activé, et dans une pièce.

TIP: Vérifiez que les types génériques sont bien configurés. Chaque équipement envoyé à Homebridge doit avoir au moins un type générique "Etat".

image::../images/ypegelumi.png[]

*-> J'ai mon Homebridge qui n'exécute pas les commandes !*

TIP: Il faut bien mettre à jour le plugin App Mobile, puis dans la configuration des dépendances, il suffit de renseigner un utilisateur avec des droits d'exécution sur les commandes.

*-> J'ai bien le retour d'état d'un équipement mais impossible de le piloter !*

TIP: Vérifiez que les types génériques sont bien configurés. Il doit y avoir une cohérence entre les types. Si vous avez le type "Info Lumière Etat", vérifiez que les actions sont de types "Action / Lumière Bouton On" etc... Voir aussi la référence à l'état (le point important ci-dessus)

*-> Le message "sans réponse" apparait dans l'application Maison ou Eve*

image::../images/sans-reponse.jpg[]

1. Si vous n'avez pas de concentrateur HomeKit (iPad ou Apple TV), vérifiez que vous êtes connectés au même réseau que votre Jeedom. 
2. Vérifiez que le démon est activé. Si ce n'est pas le cas, redémarrez le.
3. Relancez votre box.
4. Si malgré tout vous avez toujours ces états, lancez une réparation.

TIP: Beaucoup d'informations se trouvent dans les logs, le prochain chapitre vous expliquera comment les analyser.

=== Interprétation des LOGS Homebridge

[source,]
----
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] ┌──── Maison > Accessoire 1 (111)
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] │ Accessoire visible, pas coché pour Homebridge
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] │ Vérification d'existance de l'accessoire dans Homebridge...
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] │ Accessoire non existant dans Homebridge
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] │ Accessoire Ignoré
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] └─────────
----
[TIP]
L'Accessoire 1 est visible mais la case "Envoyer vers Homebridge" n'est pas cochée. L'accessoire ne sera donc pas ajouté dans Homebridge.


[source,]
----
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] ┌──── Maison > Accessoire 2 (222)
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] │ Vérification d'existance de l'accessoire dans Homebridge...
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] │ Accessoire non existant dans Homebridge
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] │ Nouvel accessoire (Accessoire 2)
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] [INFO]  Ajout service :Accessoire 2 subtype:222-918|0|920- cmd_id:918 UUID:00000049-0000-1000-8000-0026BB765291
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] [INFO]     Caractéristique :On valeur initiale:false
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] │ Ajout de l'accessoire (Accessoire 2)
[Mon Jul 17 2017 19:35:08 GMT+0000 (UTC)] [Jeedom] └─────────
----
[TIP]
L'Accessoire 2 est visible et la case "Envoyer vers Homebridge" est cochée. L'accessoire sera donc ajouté dans Homebridge.


[source,]
----
[Mon Jul 17 2017 19:45:27 GMT+0000 (UTC)] [Jeedom] ┌──── Maison > Accessoire 3 (333)
[Mon Jul 17 2017 19:45:27 GMT+0000 (UTC)] [Jeedom] [WARN] Pas de type générique "Info/Prise Etat"
[Mon Jul 17 2017 19:45:27 GMT+0000 (UTC)] [Jeedom] │ Accessoire sans Type Générique
[Mon Jul 17 2017 19:45:27 GMT+0000 (UTC)] [Jeedom] │ Vérification d'existance de l'accessoire dans Homebridge...
[Mon Jul 17 2017 19:45:27 GMT+0000 (UTC)] [Jeedom] │ Accessoire non existant dans Homebridge
[Mon Jul 17 2017 19:45:27 GMT+0000 (UTC)] [Jeedom] │ Accessoire Ignoré
[Mon Jul 17 2017 19:45:27 GMT+0000 (UTC)] [Jeedom] └─────────
----
[TIP]
L'Accessoire 3 est visible et la case "Envoyer vers Homebridge" est cochée. Mais il n'y a pas de type générique "Etat" (ou celui-ci n'est pas visible). L'accessoire ne sera donc pas intégré dans Homebridge. Pour corriger ce problème, ajoutez le type générique "Info / Prise Etat" à l'accessoire (ou cochez la case "visible").


[source,]
----
[Mon Jul 17 2017 19:49:49 GMT+0000 (UTC)] [Jeedom] ┌──── Maison > Accessoire 4 (444)
[Mon Jul 17 2017 19:49:49 GMT+0000 (UTC)] [Jeedom] [WARN] Pas de type générique "Info/Lumière Etat" ou "Info/Lumière Couleur"
[Mon Jul 17 2017 19:49:49 GMT+0000 (UTC)] [Jeedom] [WARN] Pas de type générique "Action/Prise Bouton On" ou reférence à l'état non définie sur la commande On
[Mon Jul 17 2017 19:49:49 GMT+0000 (UTC)] [Jeedom] │ Vérification d'existance de l'accessoire dans Homebridge...
[Mon Jul 17 2017 19:49:49 GMT+0000 (UTC)] [Jeedom] │ Accessoire non existant dans Homebridge
[Mon Jul 17 2017 19:49:49 GMT+0000 (UTC)] [Jeedom] │ Nouvel accessoire (Accessoire 4)
[Mon Jul 17 2017 19:49:49 GMT+0000 (UTC)] [Jeedom] [INFO]  Ajout service :Accessoire 4 subtype:444-919|0|921- cmd_id:919 UUID:00000049-0000-1000-8000-0026BB765291
[Mon Jul 17 2017 19:49:49 GMT+0000 (UTC)] [Jeedom] [INFO]     Caractéristique :On valeur initiale:false
[Mon Jul 17 2017 19:49:49 GMT+0000 (UTC)] [Jeedom] │ Ajout de l'accessoire (Accessoire 4)
[Mon Jul 17 2017 19:49:49 GMT+0000 (UTC)] [Jeedom] └─────────
----
[TIP]
Il y a une incohérence entre les types génériques. Les types "actions" ne correpondent pas au type "info". Pour corriger le problème, modifiez les types génériques de l'accessoire en gardant une cohérence entres les types actions et info.


[source,]
----
sh: 1: homebridge: not found
----
[TIP]
Les dépendances Homebridge ne sont pas installées ou certains fichiers sont manquants. Cliquez sur "Relancer".

image::../images/dependances-homebridge.png[]


== Exemple de configuration

=== Lumière

Type d'accessoire : Dimmer 2 de Fibaro (Z-Wave)

image::../images/lumiere.png[]

Type d'accessoire : Double contact de Nodon (EnOcean)

image::../images/lumiere-2.png[]

Si les deux contacts sont utilisés, copier-coller les types génériques On-1 sur On-2, Off-1 sur Off-2 et Etat-1 sur Etat-2.

=== Température et hydrométrie

Type d'accessoire : Sonde Oregon (RfxCom)

image::../images/temperature.png[]


=== Détecteur d'ouverture

Type d'accessoire : Détecteur Fibaro (Z-Wave)

Fenêtre : 

image::../images/fenetre.png[]

Si un capteur de température est utilisé, mettre "Info / Température" sur le nom de la commande Température.

Porte : 

image::../images/porte.png[]

Si un capteur de température est utilisé, mettre "Info / Température" sur le nom de la commande Température.

=== Détecteur de fuite

Type d'accessoire : Détecteur Fibaro (Z-Wave)

image::../images/fuite.png[]

=== Détecteur de fumées

Type d'accessoire : Détecteur Fibaro (Z-Wave)

image::../images/fumee.png[]

=== Volets roulants 

Type d'accessoire : Détecteur Fibaro FGR-222 (Z-Wave)

image::../images/volet.png[]

=== Porte de garage

Type d'accessoire : Aeotec - Contrôleur de porte de garage (GEN5) (Z-Wave)

image::../images/garage.png[]

=== Virtuel

Type d'accessoire : Interrupteur bistable avec le plugin virtuel

image::../images/virtuel.png[]

image::../images/virtuel-tg.png[]

=== Caméra

Homebrige prend en charge les caméras.

image::../images/camera2.png[]

En touchant la capture de la caméra souhaitée, elle s'affiche en plein écran et en live !

image::../images/camera3.png[]

Suivant les configurations matérielles, la qualité de la transmition peut varier. Par exemple, sur un NUC gen7 core i7, c'est quasiment du live ! La latence est très faible.

Celles-ci peuvent afficher une notification lorsqu'un mouvement est détecté par un capteur de présence. Il faut que la caméra et le capteur soient configurés dans la même pièce et que les notifications du capteur soient activées.

image::../images/notif.jpg[]

Les caméras décrites ci-dessous ont été testées. Elles sont donc fonctionnelles dans Homebridge.



L'intégration des caméras se fait via la bouton rouge "Plateforme Homebridge suplémentaire".

image::../images/plateforme-hb.png[]

==== Foscam C1

[source,]
----
{
   "platform":"Camera-ffmpeg",
   "cameras":[
      {
         "name":"Camera-Salon",
         "videoConfig":{
            "source":"-re -i rtsp://login:password@xxx.xxx.xxx.xxx:554/videoMain",
            "stillImageSource":"-i http://192.168.1.121:88/cgi-bin/CGIProxy.fcgi?cmd=snapPicture2&usr=login&pwd=password",
            "maxStreams":2,
            "maxWidth":1280,
            "maxHeight":720,
            "maxFPS":30,
            "vcodec": "h264"
         }
      }
   ]
}
----

Remplacer les valeurs xxx.xxx.xxx.xxx par l'adresse IP de la caméra, login par le login de connexion à la caméra et password par le mot de passe de connexion à la caméra.

==== Foscam C1 V2

[source,]
----
{
   "platform":"Camera-ffmpeg",
   "cameras":[
      {
         "name":"Son nom",
         "videoConfig":{
            "source":"-re -i rtsp://login:password@xxx.xxx.xxx.xxx:Portrtsp/videoMain",
            "stillImageSource":"-i http://login:password@xxx.xxx.xxx.xxx:Port/cgi-bin/CGIProxy.fcgi?cmd=snapPicture2&usr=login&pwd=password",
            "maxStreams":2,
            "maxWidth":1280,
            "maxHeight":720,
            "maxFPS":30
         }
      }
   ]
}
----

Remplacer les valeurs xxx.xxx.xxx.xxx par l'adresse IP de la caméra, login par le login de connexion à la caméra et password par le mot de passe de connexion à la caméra.


==== Foscam FI9821P 

[source,]
----
      {
         "name":"son nom",
         "videoConfig":{
            "source":"-re -i rtsp://login:password@xxx.xxx.xxx.xxx:Port/videoMain",
            "stillImageSource":"-i http://login:password@xxx.xxx.xxx.xxx:Port/cgi-bin/CGIProxy.fcgi?cmd=snapPicture2&usr=login&pwd=password",
            "maxStreams":2,
            "maxWidth":1280,
            "maxHeight":720,
            "maxFPS":30
         }
      }
   ]
}
----


Remplacer les valeurs xxx.xxx.xxx.xxx par l'adresse IP de la caméra, login par le login de connexion à la caméra et password par le mot de passe de connexion à la caméra.

==== Foscam FI9803 V3

[source,]
----
{
   "platform":"Camera-ffmpeg",
   "cameras":[
      {
         "name":"Son nom",
         "videoConfig":{
            "source":"-re -i rtsp://login:password@xxx.xxx.xxx.xxx:Portrtsp/videoMain",
            "stillImageSource":"-i http://login:password@xxx.xxx.xxx.xxx:Port/cgi-bin/CGIProxy.fcgi?cmd=snapPicture2&usr=login&pwd=password",
            "maxStreams":2,
            "maxWidth":1280,
            "maxHeight":720,
            "maxFPS":30
         }
      }
   ]
}
----

==== wanscam rtsp HWXXX

[source,]
----
{
 "platform":"Camera-ffmpeg",
   "cameras":[
      {
         "name":"Camera-Arrière",
         "videoConfig":{
            "source":"-re -i rtsp://login:password@xxx.xxx.xxx.xxx:554/1",
            "stillImageSource":"-i http://login:password@xxx.xxx.xxx.xxx/web/tmpfs/snap.jpg",
            "maxStreams":2,
            "maxWidth":1280,
            "maxHeight":720,
            "maxFPS":30,
            "vcodec": "h264"
         }
      }
   ]
}
----

Remplacer les valeurs xxx.xxx.xxx.xxx par l'adresse IP de la caméra, login par le login de connexion à la caméra et password par le mot de passe de connexion à la caméra.

==== Dlink DCS-5020L

[source,]
----
{
  "platform": "Camera-ffmpeg",
  "cameras": [
	{
	  "name": "Camera Cellier",
	  "videoConfig": {
		"source": "-re -f mjpeg -i http://login:password@xxx.xxx.xxx.xxx/mjpeg.cgi",
		"stillImageSource": "-f mjpeg -i http://login:password@xxx.xxx.xxx.xxx/image/jpeg.cgi",
		"maxStreams": 2,
		"maxWidth": 640,
		"maxHeight": 480,
		"maxFPS": 30,
		"vcodec": "h264"
	  }
	}
  ]
}
----

Remplacer les valeurs xxx.xxx.xxx.xxx par l'adresse IP de la caméra, login par le login de connexion à la caméra et password par le mot de passe de connexion à la caméra.

==== Netatmo Welcome

Cette caméra deviendra officielement compatible HomeKit en fin d'année 2017. 
Son intégration dans Homebridge est néanmoins possible.

[source,]
----
{
"platform": "Camera-ffmpeg",
"cameras": [
{
"name": "Camera Name",
"videoConfig": {
"source": "-re -i http://xxx.xxx.xxx.xxx/<Local_Access_Key>/live/files/high/index.m3u8",
"stillImageSource": "-i http://xxx.xxx.xxx.xxx/<Local_Access_Key>/live/snapshot_720.jpg",
"maxStreams": 2,
"maxWidth": 1280,
"maxHeight": 720,
"maxFPS": 30
}
}
]
}
----

Remplacer les valeurs xxx.xxx.xxx.xxx par l'adresse IP la caméra et  <Local_Access_Key> -> voir dans le plugin Caméra l'URL de capture /<Local_Access_Key>/live/snapshot_720.jpg.

image::../images/camera.png[]

=== Type Générenic Custom

Le type générique "Custom" permet de faire remonter n'importe quelles valeurs "info" de tous types dans Hombridge. *Quelques exemples sont décris dans ce chapritre.*

*L'information à remonter dans Homebridge ne doit pas dépasser 64 carractères.*  

[IMPORTANT]
*Seule l'application d'Elgato Eve est compatible avec ce type générique. Les équipements utilisant ce type générique n'apparaiteront pas dans l'application Maison d'Apple.*

[IMPORTANT]
*Les interractions avec Siri ainsi que les automations ne sont pas possible avec ce type générique*

[IMPORTANT]
*Il est n'est pas possible de renommer l'accessoire*

==== Utilisation avec le plugin Mode

Cela permet d'afficher l'intitulé du mode jeedom en cours.

image::../images/custom-1.png[]

Dans ce cas, il faut attribuer le type générique "Info/Générique" au nom de commande "Mode".


image::../images/custom-2.png[]

==== Utilisation avec le plugin Netatmo (station météo)

Cela permet d'afficher les informations de type pression, CO2, noise.

image::../images/custom-3.png[]

image::../images/custom-4.png[]

[TIP]
*Si le champ unité a été indiqué dans jeedom, il remontra dans le type custom.*

image::../images/custom-9.png[]

==== Utilisation avec le plugin vigilance méteo

image::../images/custom-7.png[]

image::../images/custom-6.png[]

=== Plugins spécifiques

==== Plugin "Thermostat"

[IMPORTANT]
La fonctionnalité du thermostat dans Homebridge est compatible uniquement (pour l'intant) avec le plugin Jeedom "Thermostat". Pour configurer le plugin "Thermostat", il faut se référer à la http://https://jeedom.github.io/documentation/plugins/thermostat/fr_FR/index.html[documentation du plugin].


===== Configuration

Dans HomeKit, le thermostat est géré suivant 4 modes : "Éteint", "Chauffer" "Climatiser" et "Automatique". 

Pour utiliser le thermostat dans HomeKit, l'application Eve est beaucoup plus fonctionnelle que l'application Maison. Il est d'ailleur conseillé de l'utiliser.

image::../images/thermostat1.png[]

* *Température cible* : Température de consigne;

* *Mode* : Sélection du mode du thermostat;

* *Protection enfants* : Permet de verrouiller les réglages du thermostat;

* *Statut* : Indique si le chauffage ou la climatisation émet ou pas de la chaleur ou du froid.

Seuls les modes "Chauffer" et "Refroidir" sont à configurer. Il faut attribuer un mode du plugin "Thermostat" à un mode de HomeKit.

image::../images/thermostat.png[]

===== Utilisation

Seuls les modes "CHAUF", "CLIM" et "ÉTEINT" fonctionneront. Le Mode "AUTO" est non fonctionnel. Pour mettre à l'arrêt le système de chauffage ou climatisation, il faut sélectionner le mode "ÉTEINT".

[underline]#Mise en route du chauffage#

* *CHAUF* : Active le mode du plugin "Thermostat" pour la partie chauffage.

image::../images/chauffe.png[]

La température cible passe automatique à la température de consigne réglée dans le plugin "Thermostat".

Le mode passe en "Chauffage". Cela ne veut pas dire que le radiateur émet de la chaleur. C'est juste que le système de chauffage est en route. Le statut indique si le radiateur émet de la chaleur.

image::../images/statut.png[]

*Statut arrêté" : Le radiateur n'émet pas de chaleur.

*Statut chauffage" : Le radiateur émet de la chaleur.

Il est également possible de régler une température de consigne directement depuis l'application Eve ou via Siri.

image::../images/sirichauff.png[]

Le chauffage passe en mode manuel.

image::../images/forcechauff.png[]

Le mode passe en "Désactivé", c'est normal. Dans certain cas, il peut rester dans la position où il était avant la demande de changement de la température de consigne.

La température de consigne passe bien à la valeur demandée. Si la température ambiante est infèrieure à la température de consigne, le chauffage se mettra en route. Le statut passera donc en "Chauffage".

[underline]#Mise en route de la climatisation#

Le fonctionnement de la climatisation est indentique au fonctionnement du chauffage.

En cliquant sur "CLIM", on active le mode de climatisation réglé dans le plugin "Thermostat".

image::../images/clim.png[]

On peut modifier la température de consigne.

image::../images/siriclim.png[]

Le fonctionnement de la climatisation passe en mode manuel.

image::../images/climforce.png[]

==== Plugin "Alarme"

[IMPORTANT]
La fonctionnalité de l'alarme dans Homebridge est compatible uniquement (pour l'intant) avec le plugin Jeedom "Alarme". Pour configurer le plugin "Alarme", il faut se référer à la http://https://jeedom.github.io/documentation/plugins/alarm/fr_FR/index.html[documentation du plugin].

*Ce mode fonctionne avec l'application d'Apple Maison et celle d'Elgato Eve.*

===== Configuration

Dans HomeKit, la fonction alarme est gérée suivant 4 modes : "Désactivée", "Nuit", "A distance" et "Domicile".

Depuis l'application Maison : 

image::../images/alarme.png[]

Depuis l'application Eve : 

image::../images/alarmeeve.png[]

Le mode "Désactivé", inhibe l'ensemble des modes d'alarme du plugin "Alarme". Les actions de l'onglet "Désactivation OK" sont lancées (en fonction du mode de sortie).

image::../images/inhibe.png[]

Les 3 autres modes, sont à définir dans la configuration du plugin Homebridge.

image::../images/configalarme.png[]

[IMPORTANT]

Le "mode Jeedom" correspond aux modes du plugin "Alarme".

image::../images/modealarme.png[]

Il suffit d'affecter le "mode Jeedom" au mode Homebridge choisi.

===== Utilisation

Il suffit de cliquer sur l'icone "Alarme" dans l'application Maison.

image::../images/iconealarme.png[]

Et de sélectionner le mode.

image::../images/selmodealarme.png[]

L'alarme est activée.

Sur le dashboard : 

image::../images/alarmeactive.png[]

Sur l'application Maison : 

image::../images/alarmeactive2.png[]

Pour la désactiver, il suffit de sélectionner "Désactivée". Les actions définies dans la partie "Désactivation OK" du plugin "Alarme" vont s'exécuter.

image::../images/desactivationok.png[]

En cas de déclenchement de l'alarme, une notification apparait sur le téléphone.

image::../images/alarmedeclanchee.png[]

Pour la désarmer, il faut cliquer sur l'icone "Alarme" et sélectionner "Désactivée".

image::../images/reinitialiseralarme.png[]

Les actions définies dans la partie "Réinitialisation" du plugin "Alarme" vont s'exécuter.

image::../images/reinitialisation.png[]

== Changelog

=== Plugin HomeBridge

==== v1.3.2 (09-11-2017)
    * Essai de génération de documentation par le market
    * Autre bug sur Inversion corrigé
    * Bug Siri "Ouvre tous les volets du salon" corrigé

==== v1.3.1 (31-10-2017)
    * Bug invertBinary sur présence sans inversion
    * Mise à jour documentation
    * Compatibilité Serrure Nuki

==== v1.3 (30-10-2017)
    * Plugin séparé du plugin App Mobile.
    * Récupération de la configuration du plugin App Mobile s'il est installé.
    * Meilleure réparation et installation plus poussée pour éviter des problèmes divers.
    * Documentation complètement réécrite et adaptée par @bphoque, près de 60 pages A4 !!!
    * Type "Info/Générique" supporté pour les infos Jeedom de type Numérique, Binaire, Autre dans l'application Eve uniquement (pas encore disponnible dans "Maison").
[IMPORTANT]
ne pas modifier ce type dans Jeedom pendant que Homebridge fonctionne
    * Les types génériques "Info/Choc", "Info/Vent (direction)", "Info/Vent (vitesse)", "Info/Pluie (mm/h)", "Info/Pluie (accumulation)", "Info/Pression", "Info/Son (dB)" sont gérés comme des "Info/Générique" et affichés dans Eve.
    * Lumières : Fonctionnement est corrigé pour certains plugins (voir annonce forum)
[TIP]
Si vous aviez un pont Philips Hue v1, vous avez maintenant accès à HomeKit :)
    * Alarme : les modes sont liables aux modes imposés d'HomeKit : Absent, Nuit, Présent, Désactivé. Fonctionne en consultation ET action.
    * Thermostat : (Fonctionne mieux dans Eve) : Température de consigne fonctionne, les modes peuvent être liés aux modes imposés d'HomeKit : Chauf., Clim.. L'asservissement se faisant dans Jeedom, le mode auto ne sert à rien dans HomeKit. Le statut est dans un champ générique (visible dans Eve) (cette façon de faire permet de lier les modes et d'avoir une fonctionnalité supplémentaire au lieu  de simplement vous montrer que votre chauffage chauffe). Le verrouillage apparait aussi dans Eve.
    * Nouveau design du plugin, simplification, plus besoin de choisir les plugins qui seront envoyés à Homebridge, le choix est maintenant par équipement.
    * Fenêtre "DebugInfo" (en niveau de log "info" ou "debug") pour donner des éléments importants de votre configuration en cas de demande d'aide sur le forum (à la demande).
    * Périphériques invisibles ajoutés à Homebridge, tant que "Envoyer dans Homebridge" est coché.
    * Temporisation des Slider des lumières et des volets et volumes, sinon toutes les valeurs sont envoyées à Jeedom, maintenant elles ne le sont que si le slider dans Maison ne bouge plus depuis 500ms.
    * Type Générique officiel Sabotage supporté (binaire).
    * Possibilité de personnaliser les états des Portes de Garage (Ouvert (255), En Ouverture (254), Stopé (253), En Fermeture (252), Fermé (0)) avec d'autres valeurs.
    * Les types spécifiques à Homebridge : j'ai maintenant la possibilité de créer des types spécifiques pour Homebridge, ceux-ci ne font pas partie du core (comme les types génériques) mais les complètent. Il faut néanmoins les définir manuellement dans le plugin (les types génériques restent utilisés principalement, ces types sont un ajout pour les types génériques qui n'existent pas).
    * Nouveaux types spécifiques à Homebridge : 
      ** Status Defectueux (binaire : 0:non/ 1:oui -> peut-être mappé à un binaire représentant par exemple un lien mort chez Z-Wave) .
      ** Status Actif (binaire : 0:non/ 1:oui -> peut-etre mappé au status "online" d'une Xiaomi Yeelight par exemple).
      ** Haut-parleurs, il devrait fonctionner automatiquement avec le plugin Sonos par exemple (à tester), les types sont : 
         *** Info/Haut-parleur Mute (binaire)
         *** Info/Haut-parleur Volume (pourcentage)
         *** Action/Haut-parleur Mute
         *** Action/Haut-parleur Unmute
         *** Action/Haut-parleur Toggle Mute (soit Toggle soit Mute/Unmute, les deux choix sont possibles séparément)
         *** Action/Haut-parleur Volume (typiquement un slider)
[IMPORTANT]
Info/Haut-parleur Mute est obligatoire, c'est étrange mais c'est une obligation coté HomeKit.

==== v1.2.1
    * Bugfix : capteurs Fenêtres
    * Bugfix : volets Somfy
    * Bugfix : Consommation Electrique qui bug sur composants Z-Wave
    * Bugfix : En chargement pour périf avec batterie

==== v1.2.0
    * Realease Stable

==== v1.1.4

    * Bugfix : unregister Accessories si on a une erreur
    * Update Homebridge & HAP-NodeJS
    * Bugfix : Temperature isNaN -> 0
    * pré-support Sabotage
    * Bugfix : Interdire une valeur Null ou Undefined d'être envoyée à HomeKit
    
==== v1.1.2

    * Support basique Alarme : besoin d'une config coté plugin pour mapper les modes NUIT, ABSENT, PRESENT avec des ALARM_SET_MODE Jeedom
    
==== v1.1.1 
    * Bugfix : Restauration des valeurs en cache au redémarrage
    * Bugfix : Bornage des valeurs du détecteur de lumière
    
==== v1.1.0 

    * Support des Plateformes Homebridge en mode expert (Cameras, autre...)
    * Documentation code
    * Freeze des fonctionnalités, debugging à faire en vue de version stable
    
==== v1.0.27

    * Simplifié l'ajout/suppression des services
    * Commencé à résoudre les problèmes LightBulbs mais pas terminé
    
==== v1.0.26

    * Gestion pourcentage batterie via le type générique "BATTERY"
    * Si < 20% on set un flag "LowBattery" dans Homekit pour afficher dans Maison/Eve/...
    * Gestion du "charge en cours" définit sur "non chargeable" pour l'instant car il faut voir comment on gère ca coté Jeedom

==== v1.0.25 

    * Nettoyage du code et simplification
    * Meilleure gestion des services en cas de modification de ceux-ci (modification des types génériques)

==== v1.0.24

    * Optimisation (on break les boucles si on a trouvé l'élément, plus rapide sur les grosses installations)

==== v1.0.23

    * si un volet est ouvert à 95% afficher 100% dans Maison (usure mécanique, recalibration)

==== v1.0.22

    * Préparation des Sonnettes en prévision du support dans HomeKit par Apple

==== v1.0.21

    * Corrigé la gestion des Serrures, elles fonctionnent
        *!!! si vous utilisez un iPad comme concentrateur HomeKit, pensez a désactiver Siri pour éviter à qqun de crier "siri ouvre la porte d'entrée" par la boite aux lettres (c'est arrivé !) !!!*

==== v1.0.20

    * Logs plus clairs et plus de verbosité sur la création des Characteristics

==== v1.0.19

    * Support pour les portes de garage/barrières, N'utiliser que BARRIER_STATE ou GARAGE_STATE (même traitement, états 255,254,253,252,0) et GB_TOGGLE

==== v1.0.18

    * Combiné les types OPENING et OPENING_WINDOW car c'est un même type dans Homebridge.
    * Ajout du Model (nom du type de l'eqLogic) et du Serial Number (id de l'objet + id logique) dans Homebridge.

==== v1.0.17

    * Prise en charge du niveau de debug du plugin App Mobile (il faut sauver le niveau et relancer le demon pour prise en charge)
    * Simplification du code (retiré des choses inutiles comme la création d'un serveur http)

==== v1.0.16

    * activation d'un mode debug dans la plateforme, il sera lié au status du plugin.
    * Francisation des messages du log, plus de verbosité, plus de clareté et de détails pour encore mieux vous aider en cas de problème.
    * Modification des paramètres de composition des UUID, uniquement l'id Jeedom et le nom du périphérique (la pièce Jeedom entrait en considération).
[IMPORTANT]
Cela signifie qu'à l'installation de cette version, vos périphériques dans Maison vont disparaitre pour réapparaitre dans la pièce par défaut (et casser vos scènes et automations).

        ** Point positif : vous pouvez maintenant changer de pièce dans Jeedom les périphériques sans les perdre dans Maison. Malheureusement, ils ne changeront pas dans Maison (non-implémenté dans Homebridge).
        ** j'ai gardé le nom du périphérique pour l'instant dans l'identifiant car le renommage d'un périphérique dans Jeedom casserait tout dans Maison (pour l'instant) de toute façon.
    * Modification du délais d'interrogation-longue pour optimiser les systèmes avec moins de changements d'états.
    * Modification du modèle de fonctionnement. Maintenant on prend un état des périphérique au démarrage du plugin et on le met à jour en temps réel à chaque changement dans Jeedom ou Maison. Moins de requêtes sur l'API Jeedom, plus petits temps de réponse dans Maison.
    * Ajout d'un ramasse miettes à la fin de l'ajout des périphériques présent dans Jeedom à Homebridge, tout ce qui n'a pas été ajouté/modifié est supprimé d'Homebridge (si vous avez rendu invisible un périf ou supprimé dans Jeedom par exemple).
    * Suppression du bouton Regénérer le fichier de configuration : plus besoin, lorsqu'on sauvegarde la configuration, on regénère le fichier automatiquement et on relance le daemon.
    * Suppression du bouton Effacer le cache : plus besoin, on gère la suppression individuelle des périphériques. 
[TIP]
Si vous avez un problème avec un périphérique malgré tout : décochez "Envoyer à Homebridge" | relancez le daemon | décochez "Envoyer à Homebridge" | relancez le daemon : il sera recréé tout proprement (et dans la pièce par défaut de Maison).

    * Ajout d'avertissements et de messages d'attention si on s'approche du nombre fatidique de 100 accessoires envoyés dans Homebridge (HomeKit ne supporte pas plus de 100 accessoires).
    * Au démarrage du daemon, vérification si avahi-daemon et dbus sont bien lancés, sinon, les démarrer.
    * A l'install des dépendances, passer avahi-daemon et dbus à enabled si pas le cas.
    * Corrections diverses, simplifications et optimisations.
    
    


