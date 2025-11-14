# Entrée

Un objet ENTREE est construit pour chaque objet NeTEx

* ParkingPassengerEntrance, qu'on retrouve dans le fichier parking.xml
* PointOfInterestEntrance, qu'on retrouve dans le fichier poi.xml
* StopPlaceEntrance ou Entrance, qu'on retrouve dans le fichier stop.xml

Afin de simplifier la lecture, on utilisera le terme générique Entrance pour désigner ces types trois objets NeTEx.

Remarque : pour certains attributs, on utilisera également l'objet EntranceEquipment référencé dans Entrance/placeEquipments.

## idEntree

ENTREE.idEntree peut être construit à partir de l'identifiant de l'objet NeTEx (Entrance/@id) en utilisant la codification des identifiants du standard CNIG.

## adresse

ENTREE.adresse est rempli avec la valeur de Entrance/PostalAddress/AddressLine1.

À défaut, on concaténera les valeurs des attributs suivants pour construire ENTREE.adresse :

* Entrance/PostalAddress/BuildingName
* Entrance/PostalAddress/HouseNumber
* Entrance/PostalAddress/Street

## typeEntree

ENTREE.typeEntree ne peut être renseigné.

## rampe

ENTREE.rampe ne peut être renseigné.

## rampeSonnette

ENTREE.rampeSonnette est renseigné à partir de EntranceEquipment/RampDoorbell de l'équipement référencé dans Entrance/placeEquipments.

## ascenseur

ENTREE.ascenseur ne peut être renseigné.

## escalierNbMarche

ENTREE.escalierNbMarche ne peut être renseigné.

## escalierMainCourante

ENTREE.escalierMainCourante ne peut être renseigné.

## reperabilite

ENTREE.reperabilite est renseigné à partir de EntranceEquipment/Recognizable de l'équipement référencé dans Entrance/placeEquipments.

## reperageEltsVitres

ENTREE.reperageEltsVitres ne peut être renseigné.

## signaletique

ENTREE.signaletique ne peut être renseigné.

## largeurPassage

ENTREE.largeurPassage est rempli avec la valeur de EntranceEquipment/Width de l'équipement référencé dans Entrance/placeEquipments.

À défaut, on utilisera Entrance/Width.

## controleAcces

ENTREE.controleAcces est renseigné à partir de EntranceEquipment/EntranceAttention de l'équipement référencé dans Entrance/placeEquipments à partir des règles de gestion suivantes :

* absence si EntranceAttention = none
* bouton d’appel si EntranceAttention = doorbell
* interphone si EntranceAttention = intercom

À défaut, on utilisera EntranceEquipment/AudioOrVideoIntercom de l'équipement référencé dans Entrance/placeEquipments avec les règles de gestion suivantes :

* absence si AudioOrVideoIntercom = false
* interphone si AudioOrVideoIntercom = true

## entreeAccueilVisible

ENTREE.entreeAccueilVisible ne peut être renseigné.

## eclairage

ENTREE.eclairage peut être approximé à partir de l'attribut Entrance/Lighting avec les règles de gestion suivantes :

* 150 si Lighting = wellLit
* 100 si Lighting = poorlyLit
* 0 si Lighting = unlit

## typePorte

ENTREE.typePorte est renseigné à partir de Entrance/EntranceType avec les règles de gestion suivantes :

* portail si EntranceType = gate
* porte tambour si EntranceType = revolvingDoor
* porte battante si EntranceType = swingDoor

À défaut, on utilisera EntranceEquipment/RevolvingDoor de l'équipement référencé dans Entrance/placeEquipments avec les règles de gestion suivantes :

* porte tambour si RevolvingDoor = true

## typeOuverture

ENTREE.typeOuverture est renseigné à partir de EntranceEquipment/AutomaticDoor de l'équipement référencé dans Entrance/placeEquipments avec les règles de gestion suivantes :

* automatique si AutomaticDoor = true
* manuelle si AutomaticDoor = false

## espaceManœuvre

ENTREE.espaceManœuvre est renseigné à partir de EntranceEquipment/TurningSpacePosition de l'équipement référencé dans Entrance/placeEquipments avec les règles de gestion suivantes :

* absence si TurningSpacePosition = none
* intérieur si TurningSpacePosition = inside
* extérieur si TurningSpacePosition = outside
* intérieur et extérieur si TurningSpacePosition = insideAndOutside

## largManœuvreExt

ENTREE.largManœuvreExt ne peut être renseigné.

## longManœuvreExt

ENTREE.longManœuvreExt ne peut être renseigné.

## largManœuvreInt

ENTREE.largManœuvreInt ne peut être renseigné.

## longManœuvreInt

ENTREE.longManœuvreInt ne peut être renseigné.

## typePoignée

ENTREE.typePoignée est renseigné à partir de EntranceEquipment/DoorHandleOutside et EntranceEquipment/DoorHandleInside de l'équipement référencé dans Entrance/placeEquipments avec les règles de gestion suivantes :

* béquille si DoorHandleOutside = lever et DoorHandleInside = lever
* bouton si DoorHandleOutside = button et DoorHandleInside = button
* poignée de tirage si DoorHandleOutside = grabRail et DoorHandleInside = grabRail
* levier de fenêtre si DoorHandleOutside = windowLever et DoorHandleInside = windowLever
* bâton maréchal si DoorHandleOutside = vertical et DoorHandleInside = vertical

## effortOuverture

ENTREE.effortOuverture est approximé à partir de EntranceEquipment/NecessaryForceToOpen de l'équipement référencé dans Entrance/placeEquipments avec les règles de gestion suivantes :

* 50 si NecessaryForceToOpen = heavyForce
* 40 si NecessaryForceToOpen = mediumForce
* 15 si NecessaryForceToOpen = lightForce
* 0 si NecessaryForceToOpen = noForce

À défaut, si EntranceEquipment/AutomaticDoor est vrai, ENTREE.effortOuverture = 0.
