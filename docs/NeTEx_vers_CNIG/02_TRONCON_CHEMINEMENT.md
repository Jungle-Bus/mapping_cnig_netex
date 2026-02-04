# Tronçon de cheminement

Un objet TRONCON_CHEMINEMENT est construit pour chaque objet NeTEx SitePathLink.

On les retrouve

- dans le fichier accessibility.xml (cas général)
- dans le fichier stop.xml (StopPlace/pathLinks/SitePathLink)
- dans le fichier poi.xml (PointOfInterest/pathLinks/SitePathLink)

On utilisera la géométrie de l'objet NeTEx (en général SitePathLink/gml:LineString) pour construire la géométrie du tronçon de cheminement. Une géométrie linéaire est attendue.

!!! info "Cas particulier"

    On ignorera les objets SitePathLink avec :

    - SitePathLink/AccessFeatureType = lift et SitePathLink/Distance = 0
    - SitePathLink/AccessFeatureType = lift et SitePathLink/LineString et SitePathLink/gml:LineString absents
    - SitePathLink/AccessFeatureType = lift et plusieurs éléments Level ou LevelRef dans SitePathLink/levels

    En effet, il s'agit d'objets réprésentant un déplacement uniquement vertical en utilisant un ascenseur ou un élévateur, ce qui n'est pas modélisé par un TRONCON_CHEMINEMENT dans le standard CNIG.

    [Voir l'annexe sur la modélisation des ascenseurs pour en savoir plus](../annexe_ascenseurs.md).

## idTroncon

TRONCON_CHEMINEMENT.idTroncon peut être construit à partir de l'identifiant de l'objet NeTEx (SitePathLink/@id) en utilisant la codification des identifiants du standard CNIG.

## from

TRONCON_CHEMINEMENT.from est construit en utilisant SitePathLink/From.

Il s'agit de l'identifiant du NOEUD_CHEMINEMENT qui représente le point de départ du SitePathLink.

## to

TRONCON_CHEMINEMENT.to est construit en utilisant SitePathLink/To.

Il s'agit de l'identifiant du NOEUD_CHEMINEMENT qui représente le point de destination du SitePathLink.

## longueur

TRONCON_CHEMINEMENT.longueur est rempli avec la valeur de SitePathLink/Distance.

## typeTroncon

TRONCON_CHEMINEMENT.typeTroncon est construit à partir de SitePathLink/AccessFeatureType avec les règles de gestion suivantes :

- ascenseur si AccessFeatureType = lift
- escalator si AccessFeatureType = escalator
- tapis roulant si AccessFeatureType = travelator
- rampe si AccessFeatureType = ramp
- escalier si AccessFeatureType = stairs
- série d’escaliers si AccessFeatureType = seriesOfStairs
- traversée piétonne si AccessFeatureType = crossing
- présence de barrière(s) si AccessFeatureType = barrier
- passage étroit si AccessFeatureType = narrowEntrance
- hall si AccessFeatureType = hall
- espace confiné si AccessFeatureType = confinedSpace
- gestion de queue si AccessFeatureType = queueManagement
- espace ouvert si AccessFeatureType = openSpace
- rue si AccessFeatureType = street
- trottoir si AccessFeatureType = pavement
- chemin piéton si AccessFeatureType = footpath
- passage si AccessFeatureType = concourse
- navette si AccessFeatureType = shuttle

## statutVoie

TRONCON_CHEMINEMENT.statutVoie ne peut être renseigné.

## pente

TRONCON_CHEMINEMENT.pente est rempli à partir de l'attribut SitePathLink/Gradient après conversion des degrés en pourcentages.
La formule suivante peut être utilisée : `100 * tan( Gradient / 2 * PI / 360)`

Si SitePathLink/Gradient est absent mais que SitePathLink/GradientType est renseigné, l'attribut TRONCON_CHEMINEMENT.pente pourra être approximé avec les règles de gestion suivantes :

- 12 si GradientType = verySteep
- 8 si GradientType = steep
- 5 si GradientType = medium
- 3 si GradientType = gentle
- 0 si GradientType = level

Si SitePathLink/Gradient est absent mais que SitePathLink/AccessFeatureType = stairs / seriesOfStairs, l'attribut TRONCON_CHEMINEMENT.pente est renseigné avec la valeur fixe 8888.

## devers

TRONCON_CHEMINEMENT.devers est rempli à partir de l'attribut SitePathLink/TiltAngle après conversion des degrés en pourcentages.
La formule suivante peut être utilisée : `100 * tan( TiltAngle / 2 * PI / 360)`

Si SitePathLink/TiltAngle est absent mais que SitePathLink/TiltType est renseigné, l'attribut TRONCON_CHEMINEMENT.devers pourra être approximé avec les règles de gestion suivantes :

- 5 si TiltType = strongLeftTilt / strongRightTilt
- 2 si TiltType = mediumLeftTilt / mediumRightTilt
- 0 si TiltType = nearlyFlat

## urlMedia

TRONCON_CHEMINEMENT.urlMedia peut être renseigné avec la valeur de l'attribut Equipment/Image de l'objet NeTEx Equipment référencé dans SitePathLink/placeEquipments.
