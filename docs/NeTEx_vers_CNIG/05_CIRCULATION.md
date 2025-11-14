# Circulation

Un objet CIRCULATION est construit pour chaque objet NeTEx SitePathLink avec AccessFeatureType != crossing / seriesOfStairs / stairs / ramp / travelator / escalator / lift

## idCirculation

CIRCULATION.idCirculation peut être construit à partir de l'identifiant de l'objet NeTEx (SitePathLink/@id) en utilisant la codification des identifiants du standard CNIG.

## typeSol

CIRCULATION.typeSol est renseigné à partir de SitePathLink/FlooringType avec les règles de gestion suivantes :

* carpet si FlooringType = carpet
* concrete si FlooringType = concrete
* asphalt si FlooringType = asphalt
* cork si FlooringType = cork
* fibreglassGrating si FlooringType = fibreglassGrating
* glazedCeramicTiles si FlooringType = glazedCeramicTiles
* plasticMatting si FlooringType = plasticMatting
* ceramicTiles si FlooringType = ceramicTiles
* rubber si FlooringType = rubber
* steelPlate si FlooringType = steelPlate
* vinyl si FlooringType = vinyl
* wood si FlooringType = wood
* stone si FlooringType = stone
* grass si FlooringType = grass
* dirt si FlooringType = earth
* gravel si FlooringType = gravel
* uneven si FlooringType = uneven
* autre si FlooringType = other

## largeurUtile

CIRCULATION.largeurUtile est rempli avec SitePathLink/MinimumWidth

## etatRevetement

CIRCULATION.etatRevetement ne peut être renseigné.

## eclairage

CIRCULATION.eclairage est rempli à partir de l'attribut SitePathLink/Lighting avec les règles de gestion suivantes :

* bon éclairage si Lighting = wellLit
* éclairage insuffisant si Lighting = poorlyLit
* absence d’éclairage si Lighting = unlit

## transition

CIRCULATION.transition est rempli à partir de l'attribut SitePathLink/Transition avec les règles de gestion suivantes :

* montée si Transition = up
* descente si Transition = down
* pas de changement de niveau si Transition = level

## typePassage

CIRCULATION.typePassage est rempli à partir de l'attribut SitePathLink/PassageType avec les règles de gestion suivantes :

* en surface si PassageType = pathway
* passage souterrain si PassageType = underpass
* couloir si PassageType = corridor
* tunnel si PassageType = tunnel
* aérien si PassageType = overpass

## repereLineaire

CIRCULATION.repereLineaire est rempli à partir de TactileGuidanceAvailable (SitePathLink/AccessibilityAssessment) et de SitePathLink/TactileGuidingStrip avec les règles de gestion suivantes :

* bande de guidage si TactileGuidingStrip = true
* aucun si TactileGuidanceAvailable = false

## couvert

CIRCULATION.couvert est rempli à partir de l'attribut SitePathLink/Covered avec les règles de gestion suivantes :

* intérieur si Covered = indoors
* extérieur non couvert si Covered = outdoors
* extérieur couvert si Covered = covered
