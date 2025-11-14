# Stationnement PMR

Un objet STATIONNEMENT_PMR est construit pour chaque objet NeTEx ParkingBay (qu'on retrouve dans le fichier parking.xml) avec ParkingBay/PublicUse = disabledPublicOnly et ParkingBay/ParkingVehicleType=car.

## idsStationnement

STATIONNEMENT_PMR.idsStationnement peut être construit à partir de l'identifiant de l'objet NeTEx (ParkingBay/@id) en utilisant la codification des identifiants du standard CNIG.

## typeStationnement

STATIONNEMENT_PMR.typeStationnement est renseigné à partir de ParkingBay/BayGeometry avec les règles de gestion suivantes :

* bataille si BayGeometry=orthogonal
* longitudinal si BayGeometry=parallel
* épi si BayGeometry=angled

## etatRevetement

STATIONNEMENT_PMR.etatRevetement ne peut être renseigné.

## largeurStat

STATIONNEMENT_PMR.largeurStat est rempli avec la valeur de ParkingBay/Width.

## longueurStat

STATIONNEMENT_PMR.longueurStat est rempli avec la valeur de ParkingBay/Length.

## bandLatSecurite

STATIONNEMENT_PMR.bandLatSecurite ne peut être renseigné.

## surLongueur

STATIONNEMENT_PMR.surLongueur ne peut être renseigné.

## signalPMR

STATIONNEMENT_PMR.signalPMR est renseigné à partir de ParkingBay/ParkingVisibility avec les règles de gestion suivantes :

* vrai si ParkingVisibility=signageOnly
* faux si ParkingVisibility=unmarked/demarcated

À défaut, on utilisera VisualSignsAvailable (ParkingBay/AccessibilityAssessment) avec les règles de gestion suivantes :

* vrai si VisualSignsAvailable est vrai
* faux si VisualSignsAvailable est faux

## marquageSol

STATIONNEMENT_PMR.marquageSol est renseigné à partir de ParkingBay/ParkingVisibility avec les règles de gestion suivantes :

* vrai si ParkingVisibility=demarcated
* faux si ParkingVisibility=unmarked/signageOnly

À défaut, on utilisera VisualSignsAvailable (ParkingBay/AccessibilityAssessment) avec les règles de gestion suivantes :

* vrai si VisualSignsAvailable est vrai
* faux si VisualSignsAvailable est faux

## pente

STATIONNEMENT_PMR.pente ne peut être renseigné.

## devers

STATIONNEMENT_PMR.devers ne peut être renseigné.

## typeSol

STATIONNEMENT_PMR.typeSol ne peut être renseigné.
