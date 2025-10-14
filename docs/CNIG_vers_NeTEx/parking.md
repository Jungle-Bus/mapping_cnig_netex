# Fichier parking.xml

Cette partie de la documentation explique comment générer le fichier `parking.xml` de l'export NeTEx, qui contient les informations sur les parkings.

En particulier, on y trouve des éléments NeTEx ParkingBay, générés à partir des places de stationnement réservées aux personnes à mobilité réduite du standard CNIG.

## ParkingBay

Un élément NeTEx ParkingBay est créé pour chaque place de stationnement de véhicule réservée aux personnes à mobilité réduite (STATIONNEMENT_PMR).

### ParkingBay/Centroid/Location

ParkingBay/Centroid/Location est construit à partir de la géométrie du nœud de cheminement donnant accès au stationnement PMR. Une géométrie ponctuelle est attendue.

### ParkingBay/AccessibilityAssessment

Les **AccessibilityLimitation** suivants sont présents :

- WheelchairAccess
- StepFreeAccess
- VisualSignsAvailable
- TactileGuidanceAvailable

WheelchairAccess est renseigné à l'aide des règles de gestion suivantes :

- false si STATIONNEMENT_PMR.devers > 2%
- false si STATIONNEMENT_PMR.pente > 2%
- false si STATIONNEMENT_PMR.largeurStat < 3.3 m
- false si STATIONNEMENT_PMR.typeSol = gravel / stabilisé / uneven
- false si STATIONNEMENT_PMR.etatRevetement = dégradation entraînant un problème de sécurité immédiat
- false si le nœud de cheminement donnant accès au stationnement PMR a NOEUD_CHEMINEMENT.hauteurRessaut > 0,04 m 
- true si toutes les conditions suivantes sont remplies : STATIONNEMENT_PMR.devers ≤ 2%, STATIONNEMENT_PMR.pente ≤ 2%, STATIONNEMENT_PMR.largeurStat ≥ 3,3 m, STATIONNEMENT_PMR.typeSol != gravel / stabilisé / uneven, STATIONNEMENT_PMR.etatRevetement != dégradation entraînant un problème de sécurité immédiat / dégradation entraînant une difficulté d'usage ou d'inconfort, NOEUD_CHEMINEMENT.hauteurRessaut ≤ 0.02 m

StepFreeAccess est rempli à partir de l'attribut NOEUD_CHEMINEMENT.hauteurRessaut du nœud de cheminement donnant accès au stationnement PMR avec les règles de gestion suivantes :

- false si NOEUD_CHEMINEMENT.hauteurRessaut est strictement supérieur à 0,04 m
- true si NOEUD_CHEMINEMENT.hauteurRessaut est inférieur ou égal à 0,02 m
- partial si NOEUD_CHEMINEMENT.hauteurRessaut est compris entre 0,02 m et 0,04m , en ajoutant "Présence d'une marche de moins de 4 cm" à la liste des phrases utilisées pour constituer AccessibilityAssessment/validityConditions/ValidityCondition/Description
- unknown sinon

VisualSignsAvailable est renseigné à l'aide des règles de gestion suivantes :

- false si STATIONNEMENT_PMR.signalPMR et STATIONNEMENT_PMR.marquageSol sont faux
- true si STATIONNEMENT_PMR.signalPMR et STATIONNEMENT_PMR.marquageSol sont vrais
- partial si STATIONNEMENT_PMR.signalPMR est vrai et STATIONNEMENT_PMR.marquageSol est faux, en ajoutant "Signalétique présente mais marquage au sol non conforme" à la liste des phrases utilisées pour constituer AccessibilityAssessment/validityConditions/ValidityCondition/Description
- partial si STATIONNEMENT_PMR.signalPMR est faux et STATIONNEMENT_PMR.marquageSol est vrai, en ajoutant "Marquage au sol présent mais signalétique non conforme" à la liste des phrases utilisées pour constituer AccessibilityAssessment/validityConditions/ValidityCondition/Description
- unknown sinon

TactileGuidanceAvailable est rempli à l'aide des règles de gestion suivantes :

- true si le nœud de cheminement donnant accès au stationnement PMR est l'extrémité d'un tronçon de cheminement qui est une circulation et CIRCULATION.repereLineaire != aucun
- false si le nœud de cheminement donnant accès au stationnement PMR est l'extrémité d'un tronçon de cheminement qui est une circulation et CIRCULATION.repereLineaire = aucun
- unknown sinon

### ParkingBay/PublicUse

ParkingBay/PublicUse est rempli avec la valeur fixe "disabledPublicOnly".

### ParkingBay/ParkingVehicleType

ParkingBay/ParkingVehicleType est rempli avec la valeur fixe "car".

### ParkingBay/BayGeometry

ParkingBay/BayGeometry est rempli avec la valeur de l'attribut STATIONNEMENT_PMR.typeStationnement avec les règles de gestion suivantes :

- orthogonal si typeStationnement = bataille
- angled si typeStationnement = épi
- parallel si typeStationnement = longitudinal

### ParkingBay/ParkingVisibility

ParkingBay/ParkingVisibility est rempli avec les règles de gestion suivantes :

- unmarked si STATIONNEMENT_PMR.signalPMR et STATIONNEMENT_PMR.marquageSol sont faux
- signageOnly si STATIONNEMENT_PMR.signalPMR est vrai et STATIONNEMENT_PMR.marquageSol est faux
- demarcated si STATIONNEMENT_PMR.marquageSol est vrai
- non renseigné sinon

### ParkingBay/Length

ParkingBay/Length est rempli avec la valeur de l'attribut STATIONNEMENT_PMR.longueurStat.

Cas particulier : si STATIONNEMENT_PMR.longueurStat vaut 9999 ParkingBay/Length n'est pas renseigné.

### ParkingBay/Width

ParkingBay/Width est rempli avec la valeur de l'attribut STATIONNEMENT_PMR.largeurStat.

Cas particulier : si STATIONNEMENT_PMR.largeurStat vaut 9999 ParkingBay/Width n'est pas renseigné.
