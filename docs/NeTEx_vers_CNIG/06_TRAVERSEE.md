# Traversée

Un objet TRAVERSEE est construit pour chaque objet NeTEx SitePathLink avec AccessFeatureType = crossing.

Remarque : pour certains attributs, on utilisera également l'objet CrossingEquipment référencé dans SitePathLink/placeEquipments.

## idTraversee

TRAVERSEE.idTraversee peut être construit à partir de l'identifiant de l'objet NeTEx (SitePathLink/@id) en utilisant la codification des identifiants du standard CNIG.

## etatRevetement

TRAVERSEE.etatRevetement ne peut être renseigné.

## typeMarquage

TRAVERSEE.typeMarquage est rempli à partir de l'attribut CrossingEquipment/ZebraCrossing de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

- aucun si ZebraCrossing = false
- bandes blanches si ZebraCrossing = true

À défaut, TRAVERSEE.typeMarquage est rempli à partir de VisualSignsAvailable (SitePathLink/AccessibilityAssessment) avec les règles de gestion suivantes :

- aucun si VisualSignsAvailable = false
- bandes blanches si VisualSignsAvailable = true

## etatMarquage

TRAVERSEE.etatMarquage est rempli à partir de l'attribut CrossingEquipment/MarkingStatus de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

- bon état si MarkingStatus = good
- dégradation entraînant une difficulté d'usage ou d'inconfort si MarkingStatus = worn
- dégradation entraînant un problème de sécurité immédiat si MarkingStatus = hazardous
- absence si MarkingStatus = none

## eclairage

TRAVERSEE.eclairage est rempli à partir de l'attribut SitePathLink/Lighting avec les règles de gestion suivantes :

- bon éclairage si Lighting = wellLit
- éclairage insuffisant  si Lighting = poorlyLit
- absence d’éclairage si Lighting = unlit

## feuPietons

TRAVERSEE.feuPietons est rempli à partir de l'attribut CrossingEquipment/PedestrianLights de l'équipement référencé dans SitePathLink/placeEquipments.

## aideSonore

TRAVERSEE.aideSonore est rempli à partir de AudibleSignalsAvailable (SitePathLink/AccessibilityAssessment) avec les règles de gestion suivantes :

- bon état si AudibleSignalsAvailable = true
- absence si AudibleSignalsAvailable = false
- dégradation entraînant une difficulté d'usage ou d'inconfort si AudibleSignalsAvailable = partial

Remarque : en cas de présence de AccessibilityAssessment/validityConditions/ValidityCondition/Description, on pourra affiner la valeur de cet attribut.

Si AudibleSignalsAvailable est absent ou qu'il vaut unkown, TRAVERSEE.aideSonore est rempli à partir de l'attribut CrossingEquipment/AcousticCrossingAids de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

- bon état si AcousticCrossingAids = true
- absence si AcousticCrossingAids = false

## repereLineaire

TRAVERSEE.repereLineaire est rempli à partir de TactileGuidanceAvailable (SitePathLink/AccessibilityAssessment) avec les règles de gestion suivantes :

- aucun si TactileGuidanceAvailable = false
- autre si TactileGuidanceAvailable = true

## chausseeBombee

TRAVERSEE.chausseeBombee est rempli à partir de l'attribut CrossingEquipment/BumpCrossing de l'équipement référencé dans SitePathLink/placeEquipments.

## voiesTraversees

TRAVERSEE.voiesTraversees ne peut être renseigné.
