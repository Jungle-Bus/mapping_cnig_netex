# Tapis roulant

Un objet TAPIS_ROULANT est construit pour chaque objet NeTEx SitePathLink avec AccessFeatureType = travelator.

Remarque : pour certains attributs, on utilisera également l'objet TravelatorEquipment référencé dans SitePathLink/placeEquipments.

## idTapisRoulant

TAPIS_ROULANT.idTapisRoulant peut être construit à partir de l'identifiant de l'objet NeTEx (SitePathLink/@id) en utilisant la codification des identifiants du standard CNIG.

## sens

TAPIS_ROULANT.sens est renseigné à partir de la valeur de TravelatorEquipment/DirectionOfUse de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

* variable si DirectionOfUse = both
* direct si DirectionOfUse = up

À défaut, TAPIS_ROULANT.sens est renseigné à partir de la valeur de SitePathLink/AllowedUse avec les règles de gestion suivantes :

* variable si AllowedUse = twoWay
* direct si AllowedUse = oneWay

## dispositifVigilance

TAPIS_ROULANT.dispositifVigilance ne peut être renseigné.

## largeurUtile

TAPIS_ROULANT.largeurUtile est renseigné avec la valeur de TravelatorEquipment/Width de l'équipement référencé dans SitePathLink/placeEquipments.

À défaut, TAPIS_ROULANT.largeurUtile est renseigné avec la valeur de SitePathLink/MinimumWidth.

## detecteur

TAPIS_ROULANT.detecteur est renseigné à partir de TravelatorEquipment/TactileActuators de l'équipement référencé dans SitePathLink/placeEquipments.
