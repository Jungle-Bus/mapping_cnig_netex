# Ascenseur

Un objet ASCENSEUR est construit pour chaque objet NeTEx LiftEquipment référencé dans un SitePathLink.

## idAscenseur

ASCENSEUR.idAscenseur peut être construit à partir de l'identifiant de l'objet NeTEx (LiftEquipment/@id) en utilisant la codification des identifiants du standard CNIG.

## largeurUtile

ASCENSEUR.largeurUtile est rempli avec LiftEquipment/Width.

À défaut, ASCENSEUR.largeurUtile est rempli avec la plus petite valeur de SitePathLink/MinimumWidth des SitePathLink qui référencent l'ascenseur.

## diamManoeuvreFauteuil

ASCENSEUR.diamManoeuvreFauteuil est rempli avec la valeur de l'attribut LiftEquipment/WheelchairTurningCircle.

## largeurCabine

ASCENSEUR.largeurCabine est rempli avec la valeur de l'attribut LiftEquipment/InternalWidth.

## longueurCabine

ASCENSEUR.longueurCabine est rempli avec la valeur de l'attribut LiftEquipment/Depth.

## boutonsEnRelief

ASCENSEUR.boutonsEnRelief est rempli à partir de LiftEquipment/RaisedButtons et LiftEquipment/BrailleButtons avec les règles de gestion suivantes :

* aucune touche différenciée si BrailleButtons et RaisedButtons sont faux
* touche 0 différenciée par relief supérieur si RaisedButtons est vrai et BrailleButtons est faux
* touche 0 de relief supérieur et autres touches en braille si BrailleButtons et RaisedButtons sont vrais

## annonceSonore

ASCENSEUR.annonceSonore ne peut être renseigné.

## signalEtageAudioAnnouncements

ASCENSEUR.signalEtage est rempli à partir de LiftEquipment/ReachedFloorAnnouncement avec les règles de gestion suivantes :

* aucun si ReachedFloorAnnouncement = none
* visuel si ReachedFloorAnnouncement = visual
* sonore si ReachedFloorAnnouncement = audio
* tactile si ReachedFloorAnnouncement = tactile
* visuel et sonore si ReachedFloorAnnouncement = visualAndAudio
* visuel et tactile et sonore si ReachedFloorAnnouncement = visualAndAudioAndTactile

## boucleInducMagnet

ASCENSEUR.boucleInducMagnet est rempli avec la valeur de l'attribut LiftEquipment/MagneticInductionLoop.

## miroir

ASCENSEUR.miroir est rempli avec la valeur de l'attribut LiftEquipment/MirrorOnOppositeSide.

## eclairage

ASCENSEUR.eclairage ne peut être renseigné.

## voyantAlerte

ASCENSEUR.voyantAlerte est renseigné à partir de la valeur de LiftEquipment/AlarmButton avec les règles de gestion suivantes :

* les deux si AlarmButton = true
* aucun si AlarmButton = false

## typeOuverture

ASCENSEUR.typeOuverture est renseigné à partir de la valeur de LiftEquipment/Automatic avec les règles de gestion suivantes :

* automatique si Automatic = true
* manuelle si Automatic = false

## mainCourante

ASCENSEUR.mainCourante est renseigné à partir de la valeur de LiftEquipment/HandrailType avec les règles de gestion suivantes :

* aucun si HandrailType = none
* à droite si HandrailType = oneSide
* des deux côtés si HandrailType = bothSides

## hauteurMainCourante

ASCENSEUR.hauteurMainCourante est rempli avec la valeur de l'attribut LiftEquipment/HandrailHeight.

## etatRevetement

ASCENSEUR.etatRevetement ne peut être renseigné.

## supervision

ASCENSEUR.supervision ne peut être renseigné.

## autrePorteSortie

ASCENSEUR.autrePorteSortie ne peut être renseigné.
