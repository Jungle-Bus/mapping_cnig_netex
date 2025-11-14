# Escalator

Un objet ESCALATOR est construit pour chaque objet NeTEx SitePathLink avec AccessFeatureType = escalator.

Remarque : pour certains attributs, on utilisera également l'objet EscalatorEquipment référencé dans SitePathLink/placeEquipments.

## idEscalator

ESCALATOR.idEscalator peut être construit à partir de l'identifiant de l'objet NeTEx (SitePathLink/@id) en utilisant la codification des identifiants du standard CNIG.

## transition

ESCALATOR.transition est rempli à partir de EscalatorEquipment/DirectionOfUse de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

* variable si DirectionOfUse = both
* montée si DirectionOfUse = up
* descente si DirectionOfUse = down

## dispositifVigilance

ESCALATOR.dispositifVigilance ne peut être renseigné.

## largeurUtile

ESCALATOR.largeurUtile est renseigné avec la valeur de EscalatorEquipment/Width de l'équipement référencé dans SitePathLink/placeEquipments.

À défaut, ESCALATOR.largeurUtile est renseigné avec la valeur de SitePathLink/MinimumWidth.

## detecteur

ESCALATOR.detecteur est renseigné à partir de EscalatorEquipment/TactileActuators de l'équipement référencé dans SitePathLink/placeEquipments.

## supervision

ESCALATOR.supervision est renseigné à partir de EscalatorEquipment/MonitoringRemoteControl de l'équipement référencé dans SitePathLink/placeEquipments.
