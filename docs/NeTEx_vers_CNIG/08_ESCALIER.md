# Escalier

Un objet ESCALIER est construit pour chaque objet NeTEx SitePathLink avec AccessFeatureType = stairs/seriesOfStairs.

Remarque : pour certains attributs, on utilisera également l'objet StaircaseEquipment référencé dans SitePathLink/placeEquipments.

## idEscalier

ESCALIER.idEscalier peut être construit à partir de l'identifiant de l'objet NeTEx (SitePathLink/@id) en utilisant la codification des identifiants du standard CNIG.

## etatRevetement

ESCALIER.etatRevetement ne peut être renseigné.

## mainCourante

ESCALIER.mainCourante est renseigné à partir de StaircaseEquipment/HandrailType de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

* aucun si HandrailType = none
* à droite si HandrailType = oneSide
* des deux côtés si HandrailType = bothSides

## dispositifVigilance

ESCALIER.dispositifVigilance est renseigné à partir de StaircaseEquipment/TopEnd/TexturedSurface de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

* absence si TexturedSurface = false
* bon état si TexturedSurface = true

## contrasteVisuel

ESCALIER.contrasteVisuel est renseigné à partir de StaircaseEquipment/StepColourContrast de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

* absence si StepColourContrast = false
* bon état si StepColourContrast = true

## largeurUtile

ESCALIER.largeurUtile est renseigné avec la valeur de StaircaseEquipment/Width de l'équipement référencé dans SitePathLink/placeEquipments.

À défaut, ESCALIER.largeurUtile est renseigné avec la valeur de SitePathLink/MinimumWidth.

## mainCouranteContinue

ESCALIER.mainCouranteContinue est renseigné à partir de StaircaseEquipment/ContinuousHandrail de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

* aucun si ContinuousHandrail = none
* à droite si ContinuousHandrail = oneSide
* des deux côtés si ContinuousHandrail = bothSides

## prolongMainCourante

ESCALIER.prolongMainCourante est renseigné à partir de StaircaseEquipment/TopEnd/ContinuingHandrail et de StaircaseEquipment/BottomEnd/ContinuingHandrail de l'équipement référencé dans SitePathLink/placeEquipments avec les règles de gestion suivantes :

* aucun si TopEnd/ContinuingHandrail = none et BottomEnd/ContinuingHandrail = none
* à droite si TopEnd/ContinuingHandrail = oneSide et BottomEnd/ContinuingHandrail = oneSide
* des deux côtés si TopEnd/ContinuingHandrail = bothSides et BottomEnd/ContinuingHandrail = bothSides

## nbMarches

ESCALIER.nbMarches est rempli avec la valeur de StaircaseEquipment/NumberofSteps de l'équipement référencé dans SitePathLink/placeEquipments.

À défaut, on utilisera SitePathLink/NumberOfSteps.

## nbVoleeMarches

ESCALIER.nbVoleeMarches est rempli avec la valeur de StaircaseEquipment/NumberOfFlights de l'équipement référencé dans SitePathLink/placeEquipments.

## hauteurMarche

ESCALIER.hauteurMarche est rempli avec la valeur de StaircaseEquipment/StepHeight de l'équipement référencé dans SitePathLink/placeEquipments.

## giron

ESCALIER.giron est rempli avec la valeur de StaircaseEquipment/StepLength de l'équipement référencé dans SitePathLink/placeEquipments.
