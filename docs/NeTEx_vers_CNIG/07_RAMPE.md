# Rampe d'accès

Un objet RAMPE est construit pour chaque objet NeTEx SitePathLink avec AccessFeatureType = ramp.

Remarque : pour la plupart des attributs, on utilisera également l'objet RampEquipment référencé dans SitePathLink/placeEquipments.

## idRampe

RAMPE.idRampe peut être construit à partir de l'identifiant de l'objet NeTEx (SitePathLink/@id) en utilisant la codification des identifiants du standard CNIG.

## etatRevetement

RAMPE.etatRevetement ne peut être renseigné.

## largeurUtile

RAMPE.largeurUtile est renseigné avec la valeur de RampEquipment/Width de l'équipement référencé dans SitePathLink/placeEquipments.

À défaut, RAMPE.largeurUtile est renseigné avec la valeur de SitePathLink/MinimumWidth.

## mainCourante

RAMPE.mainCourante est renseigné à partir de RampEquipment/HandrailType de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

* aucun si HandrailType = none
* à gauche si HandrailType = oneSide (Remarque : il s'agit d'une approximation)
* des deux côtés si HandrailType = bothSides

## distPalierRepos

RAMPE.distPalierRepos est rempli avec la valeur de RampEquipment/RestStopDistance de l'équipement référencé dans SitePathLink/placeEquipments.

## chasseRoue

RAMPE.chasseRoue est rempli à partir de RampEquipment/SafetyEdge de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

* aucun si SafetyEdge = none
* à gauche si SafetyEdge = oneSide (Remarque : il s'agit d'une approximation)
* des deux côtés si SafetyEdge = bothSides

## aireRotation

RAMPE.aireRotation est rempli à partir de RampEquipment/TurningSpace de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

* aucun si TurningSpace = none
* en bas si TurningSpace = bottom
* en haut si TurningSpace = top
* en haut et en bas si TurningSpace = topAndBottom

## poidsSupporte

RAMPE.poidsSupporte est renseigné avec la valeur de RampEquipment/MaximumLoad de l'équipement référencé dans SitePathLink/placeEquipments.
