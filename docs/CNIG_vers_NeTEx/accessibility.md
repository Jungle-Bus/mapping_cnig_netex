# Fichier accessibility.xml

Cette partie de la documentation explique comment générer le fichier `accessibility.xml` de l'export NeTEx, qui contient les équipements et les informations de cheminement.

## NavigationPath

Un objet NeTEx NavigationPath est construit pour chaque cheminement (CHEMINEMENT).

### NavigationPath/PathLinkInSequence

NavigationPath/PathLinkInSequence est rempli avec des références vers les objets NeTEx correspondants aux tronçons de cheminement qui composent le cheminement.

## SitePathLink

Un objet NeTEx SitePathLink est construit pour chaque tronçon de cheminement (TRONCON_CHEMINEMENT).

!!! info "Remarque"

    Il faudrait théoriquement également créer un ou plusieurs objets NeTEx SitePathLink pour représenter les déplacements verticaux qu'on peut effectuer en ascenseur (ASCENSEUR) ou avec un élévateur (ELEVATEUR), mais la modélisation et les attributs CNIG ne le permettent pas (il n'est notamment pas possible d'identifier les niveaux desservis et donc le nombre de SitePathLink à créer en conséquence).

### SitePathLink/Distance

SitePathLink/Distance est rempli à partir de l'attribut TRONCON_CHEMINEMENT.distance.

### SitePathLink/gml:LineString

SitePathLink/gml:LineString est construit à partir de la géométrie du TRONCON_CHEMINEMENT. Une géométrie linéaire est attendue.

### SitePathLink/From

SitePathLink/From est construit à partir de l'attribut TRONCON_CHEMINEMENT.from.

Il s'agit d'une référence vers l'objet NeTEx qui représente le nœud de départ du tronçon.

### SitePathLink/To

SitePathLink/To est construit à partir de l'attribut TRONCON_CHEMINEMENT.to.

Il s'agit d'une référence vers l'objet NeTEx qui représente le nœud de destination du tronçon.

### SitePathLink/AccessibilityAssessment

SitePathLink/AccessibilityAssessment est calculé à partir des attributs du TRONCON_CHEMINEMENT.

#### WheelchairAccess

Si le TRONCON_CHEMINEMENT est un ESCALIER, ESCALATOR ou un TAPIS_ROULANT, WheelchairAccess est rempli avec la valeur fixe false.

Si le TRONCON_CHEMINEMENT est une RAMPE, WheelchairAccess est rempli avec les règles de gestion suivantes :

- false si TRONCON_CHEMINEMENT.pente > 5%
- false si RAMPE.largeurUtile < 1,4m
- true si TRONCON_CHEMINEMENT.pente ≤ 5% et RAMPE.largeurUtile ≥ 1,4 m

Si le TRONCON_CHEMINEMENT est une CIRCULATION, WheelchairAccess est rempli avec les règles de gestion suivantes :

- false si TRONCON_CHEMINEMENT.devers > 5%
- false si TRONCON_CHEMINEMENT.pente > 8%
- false si CIRCULATION.largeurUtile < 0.9 m
- false si CIRCULATION.typesol = gravel / stabilisé / uneven
- false si CIRCULATION.etatRevetement = dégradation entraînant un problème de sécurité immédiat
- false si le tronçon de cheminement comporte un ou plusieurs OBSTACLEs
- true si toutes les conditions suivantes sont remplies :
	- TRONCON_CHEMINEMENT.devers ≤ 2%
	- TRONCON_CHEMINEMENT.pente ≤ 5%
	- CIRCULATION.largeurUtile ≥ 1,4 m
	- CIRCULATION.typesol != gravel / stabilisé / uneven
	- CIRCULATION.etatRevetement != dégradation entraînant un problème de sécurité immédiat
	- le tronçon de cheminement ne comporte aucun OBSTACLE
- sinon, partial si toutes les conditions suivantes sont remplies :
	- TRONCON_CHEMINEMENT.devers ≤ 5%
	- TRONCON_CHEMINEMENT.pente ≤ 8%
	- CIRCULATION.largeurUtile ≥ 0.9 m
	- CIRCULATION.typesol != gravel / stabilisé / uneven
	- CIRCULATION.etatRevetement != dégradation entraînant un problème de sécurité immédiat
	- le tronçon de cheminement ne comporte aucun OBSTACLE
- unknown sinon

Si le TRONCON_CHEMINEMENT est une TRAVERSEE, WheelchairAccess est rempli avec les règles de gestion suivantes :

- false si TRONCON_CHEMINEMENT.devers > 5%
- false si TRONCON_CHEMINEMENT.pente > 8%
- false si TRAVERSEE.etatRevetement = dégradation entraînant un problème de sécurité immédiat
- false si au moins une des deux extrémités du tronçon de cheminement correspondant à la traversée a NOEUD_CHEMINEMENT.hauteurRessaut > 0.04 m
- true si toutes les conditions suivantes sont remplies :
	- TRONCON_CHEMINEMENT.devers ≤ 2%
	- TRONCON_CHEMINEMENT.pente ≤ 5%
	- TRAVERSEE.etatRevetement != dégradation entraînant un problème de sécurité immédiat
	- les deux extrémités du tronçon de cheminement correspondant à la traversée ont NOEUD_CHEMINEMENT.hauteurRessaut ≥ 0.02 m
- sinon, partial si toutes les conditions suivantes sont remplies :
	- TRONCON_CHEMINEMENT.devers ≤ 5%
	- TRONCON_CHEMINEMENT.pente ≤ 8%
	- TRAVERSEE.etatRevetement != dégradation entraînant un problème de sécurité immédiat
	- les deux extrémités du tronçon de cheminement correspondant à la traversée ont NOEUD_CHEMINEMENT.hauteurRessaut ≤ 0.04 m
- unknown sinon

Si le TRONCON_CHEMINEMENT est un QUAI, WheelchairAccess est rempli avec les règles de gestion suivantes :

- false si TRONCON_CHEMINEMENT.devers > 5%
- false si TRONCON_CHEMINEMENT.pente > 8%
- false si QUAI.largeurPassage < 0.9 m
- false si QUAI.diamZoneManoeuvre < 1.5 m
- false si QUAI.etatRevetement = dégradation entraînant un problème de sécurité immédiat
- false si le tronçon de cheminement comporte un ou plusieurs OBSTACLEs
- true si toutes les conditions suivantes sont remplies :
	- TRONCON_CHEMINEMENT.devers ≤ 2%
	- TRONCON_CHEMINEMENT.pente ≤ 5%
	- QUAI.largeurPassage ≥ 1,4 m
	- QUAI.etatRevetement != dégradation entraînant un problème de sécurité immédiat
	- le tronçon de cheminement ne comporte aucun OBSTACLE
- sinon, partial si toutes les conditions suivantes sont remplies :
	- TRONCON_CHEMINEMENT.devers ≤ 5%
	- TRONCON_CHEMINEMENT.pente ≤ 8%
	- QUAI.largeurPassage ≥ 0.9 m
	- QUAI.etatRevetement != dégradation entraînant un problème de sécurité immédiat
	- le tronçon de cheminement ne comporte aucun OBSTACLE
- unknown sinon

Enfin, si aucune des conditions n'est remplie, WheelchairAccess vaudra "unknown".

#### StepFreeAccess

Si le TRONCON_CHEMINEMENT est un ESCALIER, StepFreeAccess est rempli avec la valeur fixe "false".

Si le TRONCON_CHEMINEMENT est un ESCALATOR, un TAPIS_ROULANT ou une RAMPE, StepFreeAccess est rempli avec la valeur fixe "true".

Si le TRONCON_CHEMINEMENT est une TRAVERSEE, StepFreeAccess est rempli avec les règles de gestion suivantes :

- false si au moins une des deux extrémités du tronçon de cheminement correspondant à la traversée a NOEUD_CHEMINEMENT.hauteurRessaut > 0.04 m
- true si les deux extrémités du tronçon de cheminement correspondant à la traversée ont NOEUD_CHEMINEMENT.hauteurRessaut ≥ 0.02 m
- sinon, partial si les deux extrémités du tronçon de cheminement correspondant à la traversée ont NOEUD_CHEMINEMENT.hauteurRessaut ≤ 0.04 m. Dans ce cas, on ajoute "Présence de marches de moins de 4 cm" à la liste des phrases utilisées pour constituer AccessibilityAssessment/validityConditions/ValidityCondition/Description
- unknown sinon

Sinon, StepFreeAccess est rempli avec les règles de gestion suivantes :

- false si le tronçon de cheminement comporte un ou plusieurs OBSTACLEs avec OBSTACLE.typeObstacle = ressaut
- true si le tronçon de cheminement ne comporte aucun OBSTACLE avec OBSTACLE.typeObstacle = ressaut
- unknown sinon

Enfin, si aucune des conditions n'est remplie, StepFreeAccess vaudra "unknown".

#### EscalatorFreeAccess

Si le TRONCON_CHEMINEMENT est un ESCALATOR, EscalatorFreeAccess est rempli avec la valeur fixe "false".

Sinon, EscalatorFreeAccess est rempli avec la valeur fixe "true".

#### LiftFreeAccess

Si une des extrémités du TRONCON_CHEMINEMENT correspond à un ASCENSEUR ou un ELEVATEUR, LiftFreeAccess est rempli avec la valeur fixe "false".

Sinon, LiftFreeAccess est rempli avec la valeur fixe "true".

#### VisualSignsAvailable

Si le TRONCON_CHEMINEMENT est une TRAVERSEE, VisualSignsAvailable est rempli avec les règles de gestion suivantes :

- false si TRAVERSEE.typeMarquage = aucun
- false si TRAVERSEE.etatMarquage = absence
- true si TRAVERSEE.etatMarquage = bon état / dégradation sans gravité
- partial si TRAVERSEE.etatMarquage = dégradation entraînant une difficulté d'usage ou d'inconfort. Dans ce cas, on ajoute à la liste des phrases utilisées pour constituer AccessibilityAssessment/validityConditions/ValidityCondition/Description la phrase suivante : "Marquage au sol avec dégradation entraînant une difficulté d’usage ou d’inconfort"
- partial si TRAVERSEE.etatMarquage = dégradation entraînant un problème de sécurité immédiat. Dans ce cas, on ajoute à la liste des phrases utilisées pour constituer AccessibilityAssessment/validityConditions/ValidityCondition/Description la phrase suivante : "Marquage au sol avec dégradation entraînant un problème de sécurité immédiat"
- unknown sinon

Sinon, VisualSignsAvailable n'est pas renseigné.

#### AudibleSignalsAvailable

Si le TRONCON_CHEMINEMENT est une TRAVERSEE, AudibleSignalsAvailable est rempli avec les règles de gestion suivantes :

- false si TRAVERSEE.aideSonore = absence
- true si TRAVERSEE.aideSonore = bon état / dégradation sans gravité
- partial si TRAVERSEE.aideSonore = dégradation entraînant une difficulté d'usage ou d'inconfort. Dans ce cas, on ajoute à la liste des phrases utilisées pour constituer AccessibilityAssessment/validityConditions/ValidityCondition/Description la phrase suivante : "Répétiteurs sonores avec dégradation entraînant une difficulté d’usage ou d’inconfort"
- partia si TRAVERSEE.aideSonore = dégradation entraînant un problème de sécurité immédiat. Dans ce cas, on ajoute à la liste des phrases utilisées pour constituer AccessibilityAssessment/validityConditions/ValidityCondition/Description la phrase suivante : "Répétiteurs sonores avec dégradation entraînant un problème de sécurité immédiat"
- unknown sinon

Sinon, AudibleSignalsAvailable n'est pas renseigné.

#### TactileGuidanceAvailable

Si le TRONCON_CHEMINEMENT est une CIRCULATION, TactileGuidanceAvailable est rempli avec les règles de gestion suivantes :

- false si CIRCULATION.repereLineaire = aucun
- true si CIRCULATION.repereLineaire != aucun
- unknown sinon

Si le TRONCON_CHEMINEMENT est une TRAVERSEE, TactileGuidanceAvailable est rempli avec les règles de gestion suivantes :

- false si TRAVERSEE.repereLineaire = aucun
- true si TRAVERSEE.repereLineaire != aucun
- unknown sinon

Si le TRONCON_CHEMINEMENT est un QUAI, TactileGuidanceAvailable est rempli avec les règles de gestion suivantes :

- false si QUAI.signalisationPorte != tactile / visuel et tactile / tactile et sonore / visuel et tactile et sonore
- true si QUAI.signalisationPorte = tactile / visuel et tactile / tactile et sonore / visuel et tactile et sonore
- unknown sinon

Sinon, TactileGuidanceAvailable est rempli avec la valeur fixe "unknown".

### SitePathLink/PublicUse

SitePathLink/PublicUse a la valeur fixe "all" car tous les cheminements décrits sont réputés accessibles à tous.

### SitePathLink/Covered

SitePathLink/Covered est rempli à partir de l'attribut CIRCULATION.couvert de l'objet CIRCULATION correspondant au TRONCON_CHEMINEMENT courant :

- indoors si couvert = intérieur
- outdoors si couvert = extérieur non couvert
- covered si couvert = extérieur couvert
- unknown si non renseigné

Si le TRONCON_CHEMINEMENT n'est pas une CIRCULATION, l'élément SitePathLink/Covered est absent.

### SitePathLink/Lighting

Si le TRONCON_CHEMINEMENT est une CIRCULATION, SitePathLink/Lighting est rempli à partir de l'attribut CIRCULATION.eclairage de l'objet CIRCULATION correspondant au TRONCON_CHEMINEMENT courant :

- wellLit si eclairage = bon éclairage
- poorlyLit si eclairage = éclairage insuffisant
- unlit si eclairage = absence d’éclairage
- unknown si non renseigné

Si le TRONCON_CHEMINEMENT est une TRAVERSEE, SitePathLink/Lighting est rempli à partir de l'attribut TRAVERSEE.eclairage de l'objet TRAVERSEE correspondant au TRONCON_CHEMINEMENT courant avec les mêmes règles de gestion.

Si le TRONCON_CHEMINEMENT est un ASCENSEUR, SitePathLink/Lighting est rempli à partir de l'attribut TRAVERSEE.eclairage de l'objet ASCENSEUR correspondant au TRONCON_CHEMINEMENT courant : TODO

Sinon, l'élément SitePathLink/Lighting est absent.

### SitePathLink/AllAreasWheelchairAccessible

SitePathLink/AllAreasWheelchairAccessible est rempli avec la valeur true si WheelchairAccess vaut true, et false si WheelchairAccess est false.

Sinon, SitePathLink/AllAreasWheelchairAccessible n'est pas renseigné.

### SitePathLink/NumberOfSteps

Si le TRONCON_CHEMINEMENT est un ESCALIER, SitePathLink/NumberOfSteps est rempli à partir de l'attribut ESCALIER.nbMarches de l'objet ESCALIER correspondant au TRONCON_CHEMINEMENT courant.

Si le TRONCON_CHEMINEMENT comporte un ou plusieurs OBSTACLEs avec OBSTACLE.typeObstacle = ressaut, SitePathLink/NumberOfSteps est rempli avec le nombre de ces OBSTACLEs.

Sinon, SitePathLink/NumberOfSteps est rempli avec la valeur fixe 0.

### SitePathLink/MinimumWidth

Si le TRONCON_CHEMINEMENT est une CIRCULATION ne comportant aucun OBSTACLE, SitePathLink/MinimumWidth est rempli à partir de l'attribut CIRCULATION.largeurUtile de l'objet CIRCULATION correspondant au TRONCON_CHEMINEMENT courant.

Si le TRONCON_CHEMINEMENT est une CIRCULATION et comporte un ou plusieurs OBSTACLEs ou PASSAGE_SELECTIFs, SitePathLink/MinimumWidth est rempli avec la plus petite valeur d'OBSTACLE.largeurUtile et PASSAGE_SELECTIF.largeurUtile.

Remarque : si tous les OBSTACLE.largeurUtile = 9999 et tous les PASSAGE_SELECTIF.largeurUtile = 9999, on peut ignorer les obstacles et utiliser CIRCULATION.largeurUtile.

Si le TRONCON_CHEMINEMENT est une RAMPE, SitePathLink/MinimumWidth est rempli à partir de l'attribut RAMPE.largeurUtile de l'objet RAMPE correspondant au TRONCON_CHEMINEMENT courant.

Si le TRONCON_CHEMINEMENT est un ESCALIER, SitePathLink/MinimumWidth est rempli à partir de l'attribut ESCALIER.largeurUtile de l'objet ESCALIER correspondant au TRONCON_CHEMINEMENT courant.

Si le TRONCON_CHEMINEMENT est un ESCALATOR, SitePathLink/MinimumWidth est rempli à partir de l'attribut ESCALATOR.largeurUtile de l'objet ESCALATOR correspondant au TRONCON_CHEMINEMENT courant.

Si le TRONCON_CHEMINEMENT est un TAPIS_ROULANT, SitePathLink/MinimumWidth est rempli à partir de l'attribut TAPIS_ROULANT.largeurUtile de l'objet TAPIS_ROULANT correspondant au TRONCON_CHEMINEMENT courant.

Si le TRONCON_CHEMINEMENT est un QUAI, SitePathLink/MinimumWidth est rempli à partir de l'attribut QUAI.largeurPassage de l'objet QUAI correspondant au TRONCON_CHEMINEMENT courant.

Sinon, ou si l'attribut en question est manquant, SitePathLink/MinimumWidth est absent.

!!! info "Cas particulier"

	Si l'attribut représentant la largeur utile de l'objet CNIG vaut 9999, on utilisera la valeur 1.80 à la place pour renseigner SitePathLink/MinimumWidth.

### SitePathLink/AllowedUse

Si le TRONCON_CHEMINEMENT est un TAPIS_ROULANT, SitePathLink/AllowedUse est rempli à partir de l'attribut TAPIS_ROULANT.sens de l'objet TAPIS_ROULANT correspondant au TRONCON_CHEMINEMENT courant :

- twoWay si sens = variable
- oneWay si sens = direct ou sens = indirect

Si le TRONCON_CHEMINEMENT est un ESCALATOR, SitePathLink/AllowedUse est rempli à partir de l'attribut ESCALATOR.transition de l'objet ESCALATOR correspondant au TRONCON_CHEMINEMENT courant :

- twoWay si transition = variable
- oneWay si transition = montée ou transition = descente

Sinon, SitePathLink/AllowedUse est absent.

### SitePathLink/Transition

Si le TRONCON_CHEMINEMENT est une CIRCULATION, SitePathLink/Transition est rempli à partir de l'attribut CIRCULATION.transition de l'objet CIRCULATION correspondant au TRONCON_CHEMINEMENT courant :

- up si transition = montée
- down si transition = descente
- level si transition = pas de changement de niveau
- SitePathLink/Transition est absent si transition = variable

Si le TRONCON_CHEMINEMENT est un ESCALATOR, SitePathLink/Transition est rempli à partir de l'attribut ESCALATOR.transition de l'objet ESCALATOR correspondant au TRONCON_CHEMINEMENT courant avec les mêmes règles de gestion

Sinon, SitePathLink/Transition est absent.

### SitePathLink/Gradient

SitePathLink/Gradient est rempli à partir de l'attribut TRONCON_CHEMINEMENT.pente, après conversion des pourcentages en degrés. La formule suivante peut être utilisée : `ceil(round(360 / (2 * PI) * 100 * arctan(pente / 100)) / 100)`.

### SitePathLink/GradientType

SitePathLink/GradientType est rempli à partir de l'attribut TRONCON_CHEMINEMENT.pente, avec les règles de gestion suivantes :

- verySteep si pente supérieur ou égal à 9%
- steep si pente entre 6 et 8%
- medium si pente = 5%
- gentle si pente entre 1 et 4%
- level si pente = 0%

### SitePathLink/TiltAngle

SitePathLink/TiltAngle est rempli à partir de l'attribut TRONCON_CHEMINEMENT.devers, après conversion des pourcentages en degrés. La formule suivante peut être utilisée : `ceil(round(360 / (2 * PI) * 100 * arctan(pente / 100)) / 100)`.

### SitePathLink/TiltType

Si TRONCON_CHEMINEMENT.devers est strictement inférieur à 2%, SitePathLink/TiltType est rempli avec la valeur fixe "nearlyFlat".

Sinon, SitePathLink/TiltType n'est pas renseigné.

### SitePathLink/AccessFeatureType

SitePathLink/AccessFeatureType est rempli à partir de la valeur de l'attribut TRONCON_CHEMINEMENT.typeTroncon avec les règles de gestion suivantes :

- footpath si typeTroncon = chemin piéton
- lift si typeTroncon = ascenseur / monte-charge / monte personne
- stairs si typeTroncon = escalier
- seriesOfStairs si typeTroncon = série d’escaliers
- escalator si typeTroncon = escalator
- travelator si typeTroncon = tapis roulant
- ramp si typeTroncon = rampe
- shuttle si typeTroncon = navette
- crossing si typeTroncon = traversée piétonne
- barrier si typeTroncon = présence de barrière(s)
- narrowEntrance si typeTroncon = passage étroit
- hall si typeTroncon = hall / couloir intérieur
- openSpace si typeTroncon = espace ouvert
- street si typeTroncon = rue
- pavement si typeTroncon = trottoir / Îlot de traversée piétonne / quai
- concourse si typeTroncon = passage
- confinedSpace si typeTroncon = espace confiné
- queueManagement si typeTroncon = gestion de queue

### SitePathLink/PassageType

Si le TRONCON_CHEMINEMENT est une CIRCULATION, SitePathLink/PassageType est rempli à partir de l'attribut CIRCULATION.typepassage de l'objet CIRCULATION correspondant au TRONCON_CHEMINEMENT courant :

- pathway si typepassage = en surface
- corridor si typepassage = couloir
- overpass si typepassage = aérien
- underpass si typepassage = passage souterrain
- tunnel si typepassage = tunnel

Sinon, SitePathLink/PassageType n'est pas renseigné.

### SitePathLink/FlooringType

Si le TRONCON_CHEMINEMENT est une CIRCULATION, SitePathLink/FlooringType est rempli à partir de l'attribut CIRCULATION.typesol de l'objet CIRCULATION correspondant au TRONCON_CHEMINEMENT courant :

- carpet si typesol = carpet
- concrete si typesol = concrete
- asphalt si typesol = asphalt
- cork si typesol = cork
- fibreglassGrating si typesol = fibreglassGrating
- glazedCeramicTiles si typesol = glazedCeramicTiles
- plasticMatting si typesol = plasticMatting
- ceramicTiles si typesol = ceramicTiles
- rubber si typesol = rubber
- steelPlate si typesol = steelPlate
- vinyl si typesol = vinyl
- wood si typesol = wood
- stone si typesol = stone
- grass si typesol = grass
- earth si typesol = dirt
- gravel si typesol = gravel
- uneven si typesol = uneven
- other si typesol a une autre valeur

Sinon, SitePathLink/FlooringType n'est pas renseigné.

### SitePathLink/TactileWarningStrip

SitePathLink/TactileWarningStrip est renseigné en utilisant l'attribut NOEUD_CHEMINEMENT.bandeEveilVigilance des deux extrémités du tronçon de cheminement, avec les règles de gestion suivantes :

- unknown si les deux extrémités ont bandeEveilVigilance = sans objet
- noTactileStrip si chaque extrémité a bandeEveilVigilance = absence/sans objet
- tactileStripAtBothEnds si les deux extrémités ont bandeEveilVigilance != absence/sans objet
- tactileStripAtBeginning si l'extrémité de départ a bandeEveilVigilance != absence/sans objet et l'extrémité d'arrivée a bandeEveilVigilance = absence/sans objet
- tactileStripAtEnd si l'extrémité d'arrivée a bandeEveilVigilance != absence/sans objet et l'extrémité de départ a bandeEveilVigilance = absence/sans objet

### SitePathLink/TactileGuidingStrip

Si le TRONCON_CHEMINEMENT est une CIRCULATION, SitePathLink/TactileGuidingStrip est rempli à partir de l'attribut CIRCULATION.repereLineaire de l'objet CIRCULATION correspondant au TRONCON_CHEMINEMENT courant :

- true si repereLineaire = bande de guidage
- false si repereLineaire != bande de guidage

Sinon, SitePathLink/TactileGuidingStrip n'est pas renseigné.

### SitePathLink/equipmentPlaces

Si le TRONCON_CHEMINEMENT comporte certains types d'OBSTACLEs, ou si une de ses extrémités correspond à une ENTREE, un ASCENSEUR ou un ELEVATEUR, SitePathLink/equipmentPlaces contient une liste de référence vers les objets NeTEx correspondant à ces objets, ainsi que leurs positions respectives.

Les équipements concernés sont :

- CrossingEquipment si le tronçon de cheminement comporte un obstacle avec typeObstacle = traversée de piste cyclable exporté en CrossingEquipment
- StaircaseEquipment si le tronçon de cheminement comporte un obstacle avec typeObstacle = ressaut exporté en StaircaseEquipment
- RoughSurface si le tronçon de cheminement comporte un obstacle avec typeObstacle = surface irrégulière exporté en RoughSurface
- EntranceEquipment si le tronçon de cheminement est le point de départ ou de destination d'un NOEUD_CHEMINEMENT qui correspond à une entrée exportée en EntranceEquipment
- LiftEquipment si le tronçon de cheminement est le point de départ ou de destination d'un NOEUD_CHEMINEMENT qui correspond à un ascenseur ou un élévateur exporté en LiftEquipment

### SitePathLink/placeEquipments

Si le TRONCON_CHEMINEMENT est un équipement d'accès, SitePathLink/placeEquipments est rempli avec une référence vers l'objet NeTEx associé à cet équipement.

Les équipements concernés sont :

- CrossingEquipment si le TRONCON_CHEMINEMENT est une TRAVERSEE
- RampEquipment si le TRONCON_CHEMINEMENT est une RAMPE
- StaircaseEquipment si le TRONCON_CHEMINEMENT est un ESCALIER
- EscalatorEquipment si le TRONCON_CHEMINEMENT est un ESCALATOR
- TravelatorEquipment si le TRONCON_CHEMINEMENT est un TAPIS_ROULANT
- QueueingEquipment si TRONCON_CHEMINEMENT.typetronçon = gestion de queue
- LiftEquipment si TRONCON_CHEMINEMENT.typetronçon = ascenseur

## CrossingEquipment

Un élément NeTEx CrossingEquipment est créé pour chaque traversée (TRAVERSEE).

Un élément NeTEx CrossingEquipment est également créé pour chaque OBSTACLE avec typeObstacle = traversée de piste cyclable.

### CrossingEquipment/ZebraCrossing

CrossingEquipment/ZebraCrossing est rempli à partir de la valeur de l'attribut TRAVERSEE.typeMarquage :

- true si typeMarquage = bandes blanches
- false sinon

Dans le cas d'un CrossingEquipment créé à partir d'un obstacle, CrossingEquipment/ZebraCrossing n'est pas renseigné.

### CrossingEquipment/PedestrianLights

CrossingEquipment/PedestrianLights est rempli à partir de la valeur de l'attribut TRAVERSEE.feuPietons.

Dans le cas d'un CrossingEquipment créé à partir d'un obstacle, CrossingEquipment/PedestrianLights n'est pas renseigné.

### CrossingEquipment/AcousticCrossingAids

CrossingEquipment/AcousticCrossingAids est rempli à partir de la valeur de l'attribut TRAVERSEE.aideSonore :

- true si aideSonore != absence
- false si aideSonore = absence

Dans le cas d'un CrossingEquipment créé à partir d'un obstacle, CrossingEquipment/AcousticCrossingAids est rempli avec la valeur fixe false.

### CrossingEquipment/TactileWarningStrip

CrossingEquipment/TactileWarningStrip est renseigné en utilisant l'attribut NOEUD_CHEMINEMENT.bandeEveilVigilance des deux extrémités du tronçon de cheminement correspondant à la traversée, avec les règles de gestion suivantes :

- unknown si les deux extrémités ont bandeEveilVigilance = sans objet
- noTactileStrip si chaque extrémité a bandeEveilVigilance = absence/sans objet
- tactileStripAtBothEnds si les deux extrémités ont bandeEveilVigilance != absence/sans objet
- tactileStripAtBeginning si l'extrémité de départ a bandeEveilVigilance != absence/sans objet et l'extrémité d'arrivée a bandeEveilVigilance = absence/sans objet
- tactileStripAtEnd si l'extrémité d'arrivée a bandeEveilVigilance != absence/sans objet et l'extrémité de départ a bandeEveilVigilance = absence/sans objet

Dans le cas d'un CrossingEquipment créé à partir d'un obstacle, CrossingEquipment/TactileWarningStrip est rempli avec la valeur fixe unknown.

### CrossingEquipment/DroppedKerb

CrossingEquipment/DroppedKerb est renseigné en utilisant l'attribut NOEUD_CHEMINEMENT.hauteurRessaut des deux extrémités du tronçon de cheminement correspondant à la traversée, avec les règles de gestion suivantes :

- true si les deux extrémités ont hauteurRessaut inférieur ou égal à 2 cm
- false sinon

Dans le cas d'un CrossingEquipment créé à partir d'un obstacle, CrossingEquipment/DroppedKerb n'est pas renseigné.

### CrossingEquipment/MarkingStatus

CrossingEquipment/MarkingStatus est rempli à partir de la valeur de l'attribut TRAVERSEE.etatMarquage avec les règles de gestion suivantes :

- good si etatMarquage = bon état
- worn si etatMarquage = dégradation sans gravité / dégradation entraînant une difficulté d'usage ou d'inconfort
- hazardous si etatMarquage = dégradation entraînant un problème de sécurité immédiat
- none si etatMarquage = absence

Dans le cas d'un CrossingEquipment créé à partir d'un obstacle, CrossingEquipment/MarkingStatus n'est pas renseigné.

### CrossingEquipment/BumpCrossing

CrossingEquipment/BumpCrossing est rempli à partir de la valeur de l'attribut TRAVERSEE.chausseeBombee.

Dans le cas d'un CrossingEquipment créé à partir d'un obstacle, CrossingEquipment/BumpCrossing n'est pas renseigné.

### CrossingEquipment/VisualObstacle

CrossingEquipment/VisualObstacle est renseigné en utilisant l'attribut NOEUD_CHEMINEMENT.masqueCovisibilite des deux extrémités du tronçon de cheminement correspondant à la traversée, avec les règles de gestion suivantes :

- none si les deux extrémités ont masqueCovisibilite = aucun
- carParking si les deux extrémités ont masqueCovisibilite = stationnement voiture
- vegetation si les deux extrémités ont masqueCovisibilite = végétation
- building si les deux extrémités ont masqueCovisibilite = bâti
- streetFurniture si les deux extrémités ont masqueCovisibilite = mobilier urbain
- other si les deux extrémités n'ont pas la même valeur

Dans le cas d'un CrossingEquipment créé à partir d'un obstacle, CrossingEquipment/VisualObstacle n'est pas renseigné.

## RampEquipment

Un élément NeTEx RampEquipment est créé pour chaque rampe d'accès (RAMPE).

### RampEquipment/Width

RampEquipment/Width est rempli avec de la valeur de l'attribut RAMPE.largeurUtile.

### RampEquipment/MaximumLoad

RampEquipment/Width est rempli avec de la valeur de l'attribut RAMPE.poidsSupporte.

### RampEquipment/Gradient

RampEquipment/Gradient est rempli à partir de la valeur de l'attribut TRONCON_CHEMINEMENT.pente du tronçon de cheminement correspondant à la rampe d'accès, après conversion des pourcentages en degrés (avec la même formule que pour SitePathLink/Gradient)

### RampEquipment/GradientType

RampEquipment/GradientType est rempli à partir de la valeur de l'attribut TRONCON_CHEMINEMENT.pente du tronçon de cheminement correspondant à la rampe d'accès, avec les mêmes règles de gestion que SitePathLink/GradientType.

### RampEquipment/HandrailType

RampEquipment/HandrailType est rempli à partir de la valeur de l'attribut RAMPE.mainCourante avec les règles de gestion suivantes :

- none si mainCourante = aucun
- oneSide si mainCourante = à droite / à gauche / au milieu
- bothSides si mainCourante = des deux côtés

### RampEquipment/Temporary

RampEquipment/Temporary est rempli avec la valeur fixe "false" car seules les rampes permanentes sont gérées.

### RampEquipment/RestStopDistance

RampEquipment/RestStopDistance est rempli avec la valeur de l'attribut RAMPE.distPalierRepos.

Cas particulier : si RAMPE.distPalierRepos vaut 9999 RampEquipment/RestStopDistance n'est pas renseigné.

### RampEquipment/SafetyEdge

RampEquipment/SafetyEdge est rempli à partir de la valeur de l'attribut RAMPE.chasseRoue avec les règles de gestion suivantes :

- none si chasseRoue = aucun
- oneSide si chasseRoue = à droite / à gauche / au milieu
- bothSides si chasseRoue = des deux côtés

### RampEquipment/TurningSpace

RampEquipment/TurningSpace est rempli à partir de la valeur de l'attribut RAMPE.aireRotation avec les règles de gestion suivantes :

- none si aireRotation = absence
- bottom si aireRotation = en bas
- top si aireRotation = en haut
- topAndBottom si aireRotation = en haut et en bas

## EscalatorEquipment

Un élément NeTEx EscalatorEquipment est créé pour chaque escalator (ESCALATOR).

### EscalatorEquipment/Width

EscalatorEquipment/Width est rempli avec de la valeur de l'attribut ESCALATOR.largeurUtile.

### EscalatorEquipment/DirectionOfUse

EscalatorEquipment/DirectionOfUse est à partir de la valeur de l'attribut ESCALATOR.transition avec les règles de gestion suivantes :

- both si transition = variable
- up si transition = montée
- down si transition = descente

### EscalatorEquipment/TactileActuators

EscalatorEquipment/TactileActuators est rempli avec de la valeur de l'attribut ESCALATOR.detecteur.

### EscalatorEquipment/MonitoringRemoteControl

EscalatorEquipment/MonitoringRemoteControl est rempli avec de la valeur de l'attribut ESCALATOR.supervision.

## TravelatorEquipment

Un élément NeTEx TravelatorEquipment est créé pour chaque tapis roulant (TAPIS_ROULANT).

### TravelatorEquipment/Width

TravelatorEquipment/Width est rempli avec de la valeur de l'attribut TAPIS_ROULANT.largeurUtile.

### TravelatorEquipment/DirectionOfUse

TravelatorEquipment/DirectionOfUse est à partir de la valeur de l'attribut TAPIS_ROULANT.sens avec les règles de gestion suivantes :

- both si sens = variable
- up si sens = direct / indirect

### TravelatorEquipment/TactileActuators

TravelatorEquipment/TactileActuators est rempli avec de la valeur de l'attribut ESCALATOR.detecteur.

## LiftEquipment

Un élément NeTEx LiftEquipment est créé pour chaque ascenseur (ASCENSEUR) et chaque élévateur (ELEVATEUR).

Un élément NeTEx LiftEquipment est également créé pour chaque TRONCON_CHEMINEMENT.typetronçon = ascenseur. Dans ce cas, aucun attribut NeTEx n'est renseigné.

### LiftEquipment/Depth

LiftEquipment/Depth est rempli avec de la valeur de l'attribut ASCENSEUR.longueurCabine ou ELEVATEUR.longueurPlateforme.

!!! info "Cas particulier"

	Si l'attribut représentant la longueur de l'objet CNIG vaut 9999, on utilisera la valeur 1.25 à la place pour renseigner LiftEquipment/Depth.

### LiftEquipment/MaximumLoad

LiftEquipment/MaximumLoad est rempli avec de la valeur de l'attribut ELEVATEUR.chargeMaximum.

Dans le cas d'un LiftEquipment créé à partir d'un ascenseur, LiftEquipment/MaximumLoad n'est pas renseigné.

### LiftEquipment/WheelchairTurningCircle

LiftEquipment/WheelchairTurningCircle est rempli avec de la valeur de l'attribut ASCENSEUR.diamManoeuvreFauteuil.

Cas particulier : si ASCENSEUR.diamManoeuvreFauteuil a pour valeur 9999 LiftEquipment/WheelchairTurningCircle n'est pas renseigné.

Dans le cas d'un LiftEquipment créé à partir d'un élévateur, LiftEquipment/WheelchairTurningCircle n'est pas renseigné.

### LiftEquipment/InternalWidth

LiftEquipment/InternalWidth est rempli avec de la valeur de l'attribut ASCENSEUR.largeurCabine ou ELEVATEUR.largeurPlateforme.

Cas particulier : si les attributs CNIG ont pour valeur 9999 LiftEquipment/InternalWidth n'est pas renseigné.

### LiftEquipment/HandrailType

LiftEquipment/HandrailType est rempli à partir de la valeur de l'attribut ASCENSEUR.mainCourante avec les règles de gestion suivantes :

- none si mainCourante = aucun
- oneSide si mainCourante = à droite / à gauche / au milieu
- bothSides si mainCourante = des deux côtés

Dans le cas d'un LiftEquipment créé à partir d'un élévateur, LiftEquipment/HandrailType n'est pas renseigné.

### LiftEquipment/HandrailHeight

LiftEquipment/HandrailHeight est rempli avec de la valeur de l'attribut ASCENSEUR.hauteurMainCourante.

Cas particulier : si ASCENSEUR.hauteurMainCourante a pour valeur 9999 LiftEquipment/HandrailHeight n'est pas renseigné.

Dans le cas d'un LiftEquipment créé à partir d'un élévateur, LiftEquipment/HandrailHeight n'est pas renseigné.

### LiftEquipment/RaisedButtons

LiftEquipment/RaisedButtons est rempli à partir de la valeur de l'attribut ASCENSEUR.boutonsEnRelief ou ELEVATEUR.boutonsEnRelief avec les règles de gestion suivantes :

- true si boutonsEnRelief = touche 0 différenciée par relief supérieur / touche 0 de relief supérieur et autres touches en braille
- false si boutonsEnRelief = aucune touche différenciée

### LiftEquipment/BrailleButtons

LiftEquipment/BrailleButtons est rempli à partir de la valeur de l'attribut ASCENSEUR.boutonsEnRelief ou ELEVATEUR.boutonsEnRelief avec les règles de gestion suivantes :

- true si boutonsEnRelief = touche 0 de relief supérieur et autres touches en braille
- false si boutonsEnRelief = aucune touche différenciée / touche 0 différenciée par relief supérieur

### LiftEquipment/MirrorOnOppositeSide

LiftEquipment/MirrorOnOppositeSide est rempli avec de la valeur de l'attribut ASCENSEUR.miroir.

Dans le cas d'un LiftEquipment créé à partir d'un élévateur, LiftEquipment/MirrorOnOppositeSide n'est pas renseigné.

### LiftEquipment/Attendant

LiftEquipment/Attendant est rempli avec des valeurs des attributs ELEVATEUR.utilisableAutonomie et ELEVATEUR.accompagnateur avec les règles de gestion suivantes :

- true si utilisableAutonomie est faux ou si accompagnateur = permanent / temporaire
- false si utilisableAutonomie est vrai ou si accompagnateur = jamais
- non renseigné sinon

### LiftEquipment/Automatic

LiftEquipment/Automatic est rempli à partir de la valeur de l'attribut ASCENSEUR.typeOuverture ou ELEVATEUR.typeOuverture avec les règles de gestion suivantes :

- true si typeOuverture = automatique
- false si typeOuverture = manuelle / ouverture manuelle assistée mécaniquement

### LiftEquipment/AlarmButton

LiftEquipment/AlarmButton est rempli à partir de la valeur de l'attribut ASCENSEUR.voyantAlerte avec les règles de gestion suivantes :

- true si voyantAlerte = voyant demande secours enregistrée / voyant demande secours en transmission / les deux
- false si voyantAlerte = manuelle / ouverture manuelle assistée mécaniquement

Dans le cas d'un LiftEquipment créé à partir d'un élévateur, LiftEquipment/AlarmButton n'est pas renseigné.

### LiftEquipment/AudioAnnouncements

LiftEquipment/AudioAnnouncements est rempli à partir des valeurs des attributs ASCENSEUR.annonceSonore et ASCENSEUR.signalEtage avec les règles de gestion suivantes :

- true si annonceSonore est vrai ou si signalEtage = sonore / visuel et sonore / tactile et sonore / visuel et tactile et sonore
- false si annonceSonore est faux et signalEtage = aucun / visuel / tactile / visuel et tactile

Dans le cas d'un LiftEquipment créé à partir d'un élévateur, LiftEquipment/AudioAnnouncements n'est pas renseigné.

### LiftEquipment/ReachedFloorAnnouncement

LiftEquipment/ReachedFloorAnnouncement est rempli à partir de la valeur de l'attribut ASCENSEUR.signalEtage avec les règles de gestion suivantes :

- none si signalEtage = aucun
- visual si signalEtage = visuel / visuel et tactile
- audio si signalEtage = sonore / tactile et sonore
- visualAndAudio si signalEtage = visuel et sonore
- tactile si signalEtage = tactile
- visualAndAudioAndTactile si signalEtage = visuel et tactile et sonore

Dans le cas d'un LiftEquipment créé à partir d'un élévateur, LiftEquipment/ReachedFloorAnnouncement n'est pas renseigné.

### LiftEquipment/MagneticInductionLoop

LiftEquipment/MagneticInductionLoop est rempli à partir de la valeur de l'attribut ASCENSEUR.boucleInducMagnet.

Dans le cas d'un LiftEquipment créé à partir d'un élévateur, LiftEquipment/ReachedFloorAnnouncement n'est pas renseigné.

## StaircaseEquipment

Un élément NeTEx StaircaseEquipment est créé pour chaque escalier (ESCALIER).

Un élément NeTEx StaircaseEquipment est également créé pour chaque OBSTACLE avec typeObstacle = ressaut.

### StaircaseEquipment/Width

StaircaseEquipment/Width est rempli avec de la valeur de l'attribut ESCALIER.largeurUtile ou OBSTACLE.largeurUtile.

### StaircaseEquipment/NumberofSteps

StaircaseEquipment/NumberofSteps est rempli avec de la valeur de l'attribut ESCALIER.nbMarches.

Dans le cas d'un StaircaseEquipment créé à partir d'un obstacle, StaircaseEquipment/NumberofSteps est rempli avec la valeur fixe 1.

### StaircaseEquipment/StepHeight

StaircaseEquipment/StepHeight est rempli avec de la valeur de l'attribut ESCALIER.hauteurMarche ou OBSTACLE.hauteurObsPoseSol.

Cas particulier : si les attributs CNIG ont pour valeur 9999 StaircaseEquipment/StepHeight n'est pas renseigné.

### StaircaseEquipment/StepLength

StaircaseEquipment/StepLength est rempli avec de la valeur de l'attribut ESCALIER.giron ou OBSTACLE.longueurObstacle.

Cas particulier : si les attributs CNIG ont pour valeur 9999 StaircaseEquipment/StepLength n'est pas renseigné.

### StaircaseEquipment/StepColourContrast

StaircaseEquipment/StepColourContrast est rempli avec de la valeur de l'attribut ESCALIER.contrasteVisuel avec les règles de gestion suivantes :

- true si contrasteVisuel = bon état / dégradation sans gravité / dégradation entraînant une difficulté d'usage ou d'inconfort / dégradation entraînant un problème de sécurité immédiat
- false si contrasteVisuel = absence

Dans le cas d'un StaircaseEquipment créé à partir d'un obstacle, StaircaseEquipment/StepColourContrast n'est pas renseigné.

### StaircaseEquipment/HandrailType

StaircaseEquipment/HandrailType est rempli à partir de la valeur de l'attribut ESCALIER.mainCourante avec les règles de gestion suivantes :

- none si mainCourante = aucun
- oneSide si mainCourante = à droite / à gauche / au milieu
- bothSides si mainCourante = des deux côtés

Dans le cas d'un StaircaseEquipment créé à partir d'un obstacle, StaircaseEquipment/HandrailType n'est pas renseigné.

### StaircaseEquipment/TopEnd/ContinuingHandrail

StaircaseEquipment/TopEnd/ContinuingHandrail est rempli à partir de la valeur de l'attribut ESCALIER.prolongMainCourante avec les règles de gestion suivantes :

- none si prolongMainCourante = aucun
- oneSide si prolongMainCourante = à droite / à gauche / au milieu
- bothSides si prolongMainCourante = des deux côtés

Dans le cas d'un StaircaseEquipment créé à partir d'un obstacle, StaircaseEquipment/TopEnd/ContinuingHandrail n'est pas renseigné.

### StaircaseEquipment/TopEnd/TexturedSurface

StaircaseEquipment/TopEnd/TexturedSurface est rempli à partir de la valeur de l'attribut ESCALIER.dispositifVigilance avec les règles de gestion suivantes :

- true si dispositifVigilance = absence
- false si dispositifVigilance = bon état / dégradation sans gravité / dégradation entraînant une difficulté d'usage ou d'inconfort / dégradation entraînant un problème de sécurité immédiat

Dans le cas d'un StaircaseEquipment créé à partir d'un obstacle, StaircaseEquipment/TopEnd/TexturedSurface est faux.

### StaircaseEquipment/BottomEnd/ContinuingHandrail

StaircaseEquipment/BottomEnd/ContinuingHandrail est rempli à partir de la valeur de l'attribut ESCALIER.prolongMainCourante avec les règles de gestion suivantes :

- none si prolongMainCourante = aucun
- oneSide si prolongMainCourante = à droite / à gauche / au milieu
- bothSides si prolongMainCourante = des deux côtés

Dans le cas d'un StaircaseEquipment créé à partir d'un obstacle, StaircaseEquipment/BottomEnd/ContinuingHandrail n'est pas renseigné.

### StaircaseEquipment/ContinuousHandrail

StaircaseEquipment/ContinuousHandrail est rempli à partir de la valeur de l'attribut ESCALIER.mainCouranteContinue avec les règles de gestion suivantes :

- none si mainCouranteContinue = aucun
- oneSide si mainCouranteContinue = à droite / à gauche / au milieu
- bothSides si mainCouranteContinue = des deux côtés

Dans le cas d'un StaircaseEquipment créé à partir d'un obstacle, StaircaseEquipment/ContinuousHandrail n'est pas renseigné.

### StaircaseEquipment/NumberOfFlights

StaircaseEquipment/NumberOfFlights est rempli avec de la valeur de l'attribut ESCALIER.nbVoleeMarches.

Dans le cas d'un StaircaseEquipment créé à partir d'un obstacle, StaircaseEquipment/NumberOfFlights n'est pas renseigné.

## EntranceEquipment

Un élément NeTEx EntranceEquipment est créé pour chaque entrée (ENTREE).

### EntranceEquipment/Width

EntranceEquipment/Width est rempli avec de la valeur de l'attribut ENTREE.largeurPassage.

!!! info "Cas particulier"

	Si l'attribut ENTREE.largeurPassage de l'objet CNIG vaut 9999, on utilisera la valeur 0.80 à la place pour renseigner EntranceEquipment/Width.

### EntranceEquipment/DoorHandleOutside

EntranceEquipment/DoorHandleOutside est rempli à partir de la valeur de l'attribut ENTREE.typePoignée avec les règles de gestion suivantes :

- lever si typePoignée = béquille
- button si typePoignée = bouton
- grabRail si typePoignée = poignée de tirage
- windowLever si typePoignée = levier de fenêtre
- vertical si typePoignée = bâton maréchal
- other sinon

### EntranceEquipment/DoorHandleInside

EntranceEquipment/DoorHandleInside est rempli à partir de la valeur de l'attribut ENTREE.typePoignée avec les règles de gestion suivantes :

- lever si typePoignée = béquille
- button si typePoignée = bouton
- grabRail si typePoignée = poignée de tirage
- windowLever si typePoignée = levier de fenêtre
- vertical si typePoignée = bâton maréchal
- other sinon

### EntranceEquipment/RevolvingDoor

EntranceEquipment/RevolvingDoor est rempli à partir de la valeur de l'attribut ENTREE.typePorte avec les règles de gestion suivantes :

- true si typePorte = porte tambour
- false si typePorte a une autre valeur 

### EntranceEquipment/DropKerbOutside

EntranceEquipment/DropKerbOutside est rempli à partir de la valeur de l'attribut NOEUD_CHEMINEMENT.hauteurRessaut du nœud de cheminement correspondant à l'entrée avec les règles de gestion suivantes :

- true si hauteurRessaut inférieur ou égal à 2 cm
- false sinon

### EntranceEquipment/AutomaticDoor

EntranceEquipment/AutomaticDoor est rempli à partir de la valeur de l'attribut ENTREE.typeOuverture avec les règles de gestion suivantes :

- true si typeOuverture = automatique
- false si typeOuverture = manuelle / ouverture manuelle assistée mécaniquement

### EntranceEquipment/GlassDoor

EntranceEquipment/GlassDoor est rempli à partir de la valeur de l'attribut ENTREE.reperageEltsVitres avec les règles de gestion suivantes :

- true si reperageEltsVitres est vrai
- non renseigné sinon

### EntranceEquipment/AudioOrVideoIntercom

EntranceEquipment/AudioOrVideoIntercom est rempli à partir de la valeur de l'attribut ENTREE.controleAcces avec les règles de gestion suivantes :

- true si controleAcces = bouton d’appel / interphone / visiophone / boucle à induction magnétique
- false si controleAcces = absence

### EntranceEquipment/EntranceAttention

EntranceEquipment/EntranceAttention est rempli à partir de la valeur de l'attribut ENTREE.controleAcces avec les règles de gestion suivantes :

- none si controleAcces = absence
- doorbell si controleAcces = bouton d’appel
- intercom si controleAcces = interphone / visiophone / boucle à induction magnétique

### EntranceEquipment/DoorstepMark

EntranceEquipment/DoorstepMark est rempli à partir de la valeur de l'attribut NOEUD_CHEMINEMENT.bandeEveilVigilance du nœud de cheminement correspondant à l'entrée avec les règles de gestion suivantes :

- true si bandeEveilVigilance = bon état / dégradation sans gravité / dégradation entraînant une difficulté d'usage ou d'inconfort / dégradation entraînant un problème de sécurité immédiat
- false si bandeEveilVigilance = absence

### EntranceEquipment/NecessaryForceToOpen

EntranceEquipment/NecessaryForceToOpen est rempli à partir de la valeur de l'attribut ENTREE.effortOuverture avec les règles de gestion suivantes :

- heavyForce si effortOuverture > 50 N
- mediumForce si effortOuverture est entre 20 et 50
- lightForce si effortOuverture < 20
- noForce si effortOuverture = 0
- noForce si effortOuverture n'est pas renseigné mais que typeOuverture = automatique
- unknown sinon

### EntranceEquipment/RampDoorbell

EntranceEquipment/RampDoorbell est rempli avec de la valeur de l'attribut ENTREE.rampeSonnette.

### EntranceEquipment/Recognizable

EntranceEquipment/Recognizable est rempli avec de la valeur de l'attribut ENTREE.reperabilite.

### EntranceEquipment/TurningSpacePosition

EntranceEquipment/TurningSpacePosition est rempli à partir de la valeur de l'attribut ENTREE.espaceManœuvre avec les règles de gestion suivantes :

- none si espaceManœuvre = absence
- inside si espaceManœuvre = intérieur
- outside si espaceManœuvre = extérieur
- insideAndOutside si espaceManœuvre = intérieur et extérieur

### EntranceEquipment/WheelchairTurningCircle

EntranceEquipment/WheelchairTurningCircle est rempli avec la plus petite valeur des attributs suivants :

- ENTREE.largManœuvreExt
- ENTREE.longManœuvreExt
- ENTREE.largManœuvreInt
- ENTREE.longManœuvreInt

Cas particulier : si tous ces attributs ont pour valeur 9999, la valeur 1.80 sera utilisée à la place pour remplir EntranceEquipment/WheelchairTurningCircle.

## QueueingEquipment

Un élément NeTEx RoughSurface est créé pour chaque TRONCON_CHEMINEMENT avec typetronçon = gestion de queue. Aucun attribut NeTEx n'est renseigné.

## RoughSurface

Un élément NeTEx RoughSurface est créé pour chaque obstacle avec typeObstacle = surface irrégulière.

### RoughSurface/Width

RoughSurface/Width est rempli avec de la valeur de l'attribut OBSTACLE.largeurUtile.

Cas particulier : si OBSTACLE.largeurUtile=9999 la valeur 1.80 sera utilisée à la place.

### RoughSurface/SurfaceType

RoughSurface/SurfaceType est rempli avec la valeur fixe other.

## AssistanceService

Un élément NeTEx AssistanceService est créé pour chaque ERP pour représenter son accueil.

### AssistanceService/AssistanceFacilityList

AssistanceService/AssistanceFacilityList est rempli avec la valeur fixe "information".

### AssistanceService/Staffing

AssistanceService/Staffing est rempli avec la valeur de l'attribut ERP.accueilPersonnel avec les règles de gestion suivantes :

- unmanned si ERP.accueilPersonnel = absence de personnel
- non renseigné sinon

### AssistanceService/AccessibilityTrainedStaff

AssistanceService/AccessibilityTrainedStaff est rempli avec la valeur de l'attribut ERP.accueilPersonnel avec les règles de gestion suivantes :

- true si ERP.accueilPersonnel = personnel formé à l’accueil des publics spécifiques
- false si ERP.accueilPersonnel = personnel non-formé à l’accueil des publics spécifiques