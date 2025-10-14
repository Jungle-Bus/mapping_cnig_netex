# Fichier stop.xml

Cette partie de la documentation explique comment générer le fichier `stop.xml` de l'export NeTEx, qui contient les informations sur les arrêts, les quais, etc.

## Quay

!!! info "Remarque"

    Il est théoriquement possible de créer un élément NeTEx Quay pour chaque quai (QUAI). Cependant, les attributs CNIG ne permettent pas d'exporter les attributs obligatoires dans la cadre du profil français, notamment Quay/TransportMode.

## StopPlace

!!! info "Remarque"

    Il est théoriquement possible de créer un élément NeTEx StopPlace pour chaque ERP avec ERP.erpType = GA. Cependant, les attributs CNIG ne permettent pas d'exporter les attributs obligatoires dans la cadre du profil français, notamment StopPlace/TransportMode.

## StopPlaceEntrance

Un élément NeTEx StopPlaceEntrance est créé pour chaque entrée d'ERP avec ERP.erpType = GA.

### StopPlaceEntrance/Centroid/Location

StopPlaceEntrance/Centroid/Location est construit à partir de la géométrie du nœud de cheminement correspondant à l'entrée. Une géométrie ponctuelle est attendue.

### StopPlaceEntrance/AccessibilityAssessment

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

### StopPlaceEntrance/SiteRef

StopPlaceEntrance/SiteRef référence l’objet NeTEx dont c'est une entrée. Il s'agit de l'objet StopPlace exporté à partir de l'ERP.

### StopPlaceEntrance/placeEquipments

StopPlaceEntrance/placeEquipments contient une référence vers l'EntranceEquipment créé en complément de l'objet StopPlaceEntrance.

### StopPlaceEntrance/EntranceType

StopPlaceEntrance/EntranceType est rempli à partir de la valeur de l'attribut ENTREE.typePorte ou ENTREE.typePorte avec les règles de gestion suivantes :

- gate si typePorte = portail
- automaticDoor si typeOuverture = automatique
- revolvingDoor si typePorte = porte tambour
- swingDoor si typePorte = porte battante
- non renseigné sinon

### StopPlaceEntrance/Width

StopPlaceEntrance/Width est rempli avec de la valeur de l'attribut ENTREE.largeurPassage.

!!! info "Cas particulier"

	Si l'attribut ENTREE.largeurPassage de l'objet CNIG vaut 9999, on utilisera la valeur 0.80 à la place pour renseigner StopPlaceEntrance/Width.