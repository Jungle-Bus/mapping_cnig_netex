# Fichier poi.xml

Cette partie de la documentation explique comment générer le fichier `poi.xml` de l'export NeTEx, qui contient les points d'intérêts et les informations associées.

En particulier, on y trouve :

- des éléments NeTEx PointOfInterest, générés à partir des ERP du standard CNIG
- des éléments NeTEx PointOfInterestEntrance, générés à partir des entrées d'ERP du standard CNIG

## PointOfInterest

Un élément NeTEx PointOfInterest est créé pour chaque établissement recevant du public ou installation ouverte au public (ERP).

### PointOfInterest/Centroid/Location

PointOfInterest/Centroid/Location est construit à partir des attributs ERP.latitude et ERP.longitude.

### PointOfInterest/gml:Polygon

PointOfInterest/gml:Polygon est construit à partir de la géométrie de l'ERP. Une géométrie polygonale est attendue.

### PointOfInterest/Url

PointOfInterest/Url est rempli avec la valeur de l'attribut ERP.siteWeb.

### PointOfInterest/PostalAddress/AddressLine1

PointOfInterest/PostalAddress/AddressLine1 est rempli avec la valeur de l'attribut ERP.adresse.

### PointOfInterest/PostalAddress/PostCode

PointOfInterest/PostalAddress/PostCode est rempli avec la valeur de l'attribut ERP.codePostal.

### PointOfInterest/AccessibilityAssessment

Les **AccessibilityLimitation** suivants sont présents :

- WheelchairAccess
- AudibleSignalsAvailable
- VisualSignsAvailable
- TactileGuidanceAvailable

WheelchairAccess est rempli avec la valeur fixe "unknown".

AudibleSignalsAvailable est rempli avec la valeur true s'il y a un CHEMINEMENT_ERP cheminant dans l'ERP avec CHEMINEMENT_ERP.sysGuidSonore vrai.
Sinon, AudibleSignalsAvailable est rempli avec la valeur "unknown".

VisualSignsAvailable est rempli avec la valeur true s'il y a un CHEMINEMENT_ERP cheminant dans l'ERP avec CHEMINEMENT_ERP.sysGuidVisuel vrai.
Sinon, VisualSignsAvailable est rempli avec la valeur "unknown".

TactileGuidanceAvailable est rempli avec la valeur true s'il y a un CHEMINEMENT_ERP cheminant dans l'ERP avec CHEMINEMENT_ERP.sysGuidTactile vrai.
Sinon, TactileGuidanceAvailable est rempli avec la valeur "unknown".

### PointOfInterest/facilities

PointOfInterest/facilities comprend un **SiteFacilitySet**.

Le SiteFacilitySet peut contenir les éléments suivants :

- AccessibilityInfoFacilityList
- AssistanceFacilityList
- SanitaryFacilityList
- AccessFacilityList
- ParkingFacilityList
- Staffing

L'élément AccessibilityInfoFacilityList contient la valeur audioForHearingImpaired si au moins un des attributs suivants est vrai : ERP.accueilBIM, ERP.accueilBIMPortative, ERP.accueilLSF, ERP.accueilST, ERP.accueilAideAudition. Sinon, l'élément n'est pas présent.

L'élément AssistanceFacilityList contient la valeur information.

L'élément SanitaryFacilityList contient la liste de valeurs suivantes :

- wheelchairAccessToilet si ERP.sanitairesAdaptes vaut au moins 1
- toilet si ERP.sanitairesERP est vrai
- none si ERP.sanitairesERP est faux

L'élément AccessFacilityList contient la liste de valeurs suivantes :

- lift s'il y a un CHEMINEMENT_ERP cheminant dans l'ERP avec CHEMINEMENT_ERP.ascenseur vrai
- ramp s'il y a un CHEMINEMENT_ERP cheminant dans l'ERP avec CHEMINEMENT_ERP.rampe =  fixe / amovible
- stairs s'il y a un CHEMINEMENT_ERP cheminant dans l'ERP avec CHEMINEMENT_ERP.escalierNbMarche > 0 ou CHEMINEMENT_ERP.escalierDescendant > 0

L'élément ParkingFacilityList contient la valeur carPark si ERP.stationnementERP est vrai. Sinon, l'élément n'est pas présent.

L'élément Staffing contient la valeur unmanned si ERP.accueilPersonnel = absence de personnel. Sinon, l'élément n'est pas présent.

### PointOfInterest/entrances

PointOfInterest/entrances contient une liste de références vers les éléments NeTEx Entrance entrées de l'ERP.

### PointOfInterest/equipmentPlaces

PointOfInterest/equipmentPlaces contient une liste de références vers les équipements de l'ERP. Il peut s'agir d'EntranceEquipment et de AssistanceService.

### PointOfInterest/classifications

PointOfInterest/classifications pourra être utilisé pour exporter ERP.erpActivite, et éventuellement ERP.erpCategorie et ERP.erpType.

## PointOfInterestEntrance

Un élément NeTEx PointOfInterestEntrance est créé pour chaque entrée d'ERP.

### PointOfInterestEntrance/Centroid/Location

PointOfInterestEntrance/Centroid/Location est construit à partir de la géométrie du nœud de cheminement correspondant à l'entrée. Une géométrie ponctuelle est attendue.

### PointOfInterestEntrance/AccessibilityAssessment

Les **AccessibilityLimitation** suivants sont présents :

- WheelchairAccess
- StepFreeAccess
- TactileGuidanceAvailable

WheelchairAccess est renseigné à l'aide des règles de gestion suivantes :

- false si ENTREE.largeurPassage < 0.8 m
- false si ENTREE.effortOuverture > 50 N
- false si NOEUD_CHEMINEMENT.hauteurRessaut du nœud de cheminement correspondant à l'entrée > à 0,04 m
- true si ENTREE.largeurPassage ≥ 0.8 m, NOEUD_CHEMINEMENT.hauteurRessaut < 0.02 m et ENTREE.effortOuverture ≤ 50 N
- true si ENTREE.largeurPassage ≥ 0.8 m, NOEUD_CHEMINEMENT.hauteurRessaut < 0.02 m et ENTREE.typeOuverture = automatique

Enfin, si aucune des conditions n'est remplie, WheelchairAccess vaudra "unknown".

StepFreeAccess est rempli à partir de l'attribut NOEUD_CHEMINEMENT.hauteurRessaut du nœud de cheminement correspondant à l'entrée avec les règles de gestion suivantes :

- false si NOEUD_CHEMINEMENT.hauteurRessaut est strictement supérieur à 0,04 m
- true si NOEUD_CHEMINEMENT.hauteurRessaut est inférieur ou égal à 0,02 m
- partial si NOEUD_CHEMINEMENT.hauteurRessaut est compris entre 0,02 m et 0,04m , en ajoutant "Présence d'une marche de moins de 4 cm" à la liste des phrases utilisées pour constituer AccessibilityAssessment/validityConditions/ValidityCondition/Description
- unknown sinon

TactileGuidanceAvailable est rempli à l'aide des règles de gestion suivantes :

- true si l'entrée correspond à un nœud de cheminement qui est l'extrémité d'un tronçon de cheminement qui est une circulation et CIRCULATION.repereLineaire != aucun
- true s'il y a un CHEMINEMENT_ERP qui part ou arrive à l'entrée avec CHEMINEMENT_ERP.sysGuidTactile vrai
- false si l'entrée correspond à un nœud de cheminement qui est l'extrémité d'un tronçon de cheminement qui est une circulation et CIRCULATION.repereLineaire = aucun et aucun CHEMINEMENT_ERP qui part ou arrive à l'entrée n'a CHEMINEMENT_ERP.sysGuidTactile vrai
- unknown sinon

### PointOfInterestEntrance/SiteRef

PointOfInterestEntrance/SiteRef référence l’objet NeTEx dont c'est une entrée. Il s'agit de l'objet PointOfInterest exporté à partir de l'ERP.

### PointOfInterestEntrance/placeEquipments

PointOfInterestEntrance/placeEquipments contient une référence vers l'EntranceEquipment créé en complément de l'objet PointOfInterestEntrance.

### PointOfInterestEntrance/EntranceType

PointOfInterestEntrance/EntranceType est rempli à partir de la valeur de l'attribut ENTREE.typePorte ou ENTREE.typePorte avec les règles de gestion suivantes :

- gate si typePorte = portail
- automaticDoor si typeOuverture = automatique
- revolvingDoor si typePorte = porte tambour
- swingDoor si typePorte = porte battante
- non renseigné sinon

### PointOfInterestEntrance/Width

PointOfInterestEntrance/Width est rempli avec de la valeur de l'attribut ENTREE.largeurPassage.
