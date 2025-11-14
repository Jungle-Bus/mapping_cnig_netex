# Obstacle

Un objet OBSTACLE est construit pour chaque objet NeTEx CrossingEquipment, StaircaseEquipment ou RoughSurface référencé dans un SitePathLink/equipmentPlaces.

On utilisera la géométrie de l'objet telle qu'indiquée dans SitePathLink/equipmentPlaces (en général EquipmentPlace/equipmentPositions/EquipmentPosition/Location) pour construire la géométrie de l'obstacle.

Une géométrie ponctuelle est attendue. Une projection peut être nécessaire (le système de référence utilisé par défaut pour NeTEx est le WGS 84).

## idObstacle

OBSTACLE.idObstacle peut être construit à partir de l'identifiant de l'objet NeTEx (Equipment/@id) en utilisant la codification des identifiants du standard CNIG.

## typeObstacle

Si l'objet NeTEx est un CrossingEquipment, OBSTACLE.typeObstacle = traversée de piste cyclable.

Si l'objet NeTEx est un StaircaseEquipment, OBSTACLE.typeObstacle = ressaut.

Si l'objet NeTEx est un RoughSurface, OBSTACLE.typeObstacle = surface irrégulière.

## largeurUtile

OBSTACLE.largeurUtile ne peut être renseigné.

## positionObstacle

Si l'objet NeTEx est un CrossingEquipment ou un RoughSurface, OBSTACLE.positionObstacle = en surface.

Si l'objet NeTEx est un StaircaseEquipment, OBSTACLE.typeObstacle = obstacle posé au sol.

## longueurObstacle

OBSTACLE.longueurObstacle ne peut être renseigné.

## rappelObstacle

OBSTACLE.rappelObstacle ne peut être renseigné.

## reperabiliteVisuelle

OBSTACLE.reperabiliteVisuelle ne peut être renseigné.

## urlMedia

OBSTACLE.urlMedia est rempli avec la valeur de Equipment/Image.

## hauteurSousObs

OBSTACLE.hauteurSousObs ne peut être renseigné.

## hauteurObsPoseSol

Si l'objet NeTEx est un StaircaseEquipment, OBSTACLE.hauteurObsPoseSol est rempli avec la valeur de StaircaseEquipment/StepHeight.
