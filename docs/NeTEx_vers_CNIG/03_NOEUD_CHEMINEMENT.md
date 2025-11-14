# Nœud de cheminement

Un objet NOEUD_CHEMINEMENT est construit pour chaque extrémité de SitePathLink, en utilisant les objets NeTEx référencés dans SitePathLink/From et SitePathLink/To.

Un objet NOEUD_CHEMINEMENT est également construit pour chaque objet NeTEx :

* ParkingPassengerEntrance, qu'on retrouve dans le fichier parking.xml
* PointOfInterestEntrance, qu'on retrouve dans le fichier poi.xml
* StopPlaceEntrance ou Entrance, qu'on retrouve dans le fichier stop.xml

Afin de simplifier la lecture, on utilisera le terme générique Entrance pour désigner ces types trois objets NeTEx.

Un objet NOEUD_CHEMINEMENT est également construit pour chaque ParkingBay (qu'on retrouve dans le fichier parking.xml).

Un objet NOEUD_CHEMINEMENT est enfin construit pour chaque LiftEquipment référencé au sein d'un SitePathLink.

On utilisera les coordonnées de l'objet NeTEx (en général Centroid/Location) pour construire la géométrie du nœud de cheminement.

Une géométrie ponctuelle est attendue. Une projection peut être nécessaire (le système de référence utilisé par défaut pour NeTEx est le WGS 84).

## idNoeud

NOEUD_CHEMINEMENT.idNoeud peut être construit à partir de l'identifiant de l'objet NeTEx d'origine en utilisant la codification des identifiants du standard CNIG.

## altitude

NOEUD_CHEMINEMENT.altitude peut être construit à partir de Centroid/Location/Altitude de l'objet NeTEx d'origine si présent.

## bandeEveilVigilance

Pour les extrémités de SitePathLink, NOEUD_CHEMINEMENT.bandeEveilVigilance est renseigné à partir de SitePathLink/TactileWarningStrip avec les règles de gestion suivantes :

* sans objet, si TactileWarningStrip=unknown
* absence, si TactileWarningStrip=noTactileStrip
* bon état, si TactileWarningStrip=tactileStripAtBothEnds
* si TactileWarningStrip=tactileStripAtBeginning : bon état si l'extrémité en question est le nœud de départ du tronçon de cheminement ; absence sinon
* si TactileWarningStrip=tactileStripAtEnd : bon état si l'extrémité en question est le nœud de destination du tronçon de cheminement ; absence sinon

Pour les ParkingBay et Entrance, NOEUD_CHEMINEMENT.bandeEveilVigilance prend la valeur fixe "sans objet".

## hauteurRessaut

NOEUD_CHEMINEMENT.hauteurRessaut prend la valeur 9999 dans les cas suivants :

* si le nœud est une extrémité d'un SitePathLink qui référence un CrossingEquipment dans SitePathLink/placeEquipments avec CrossingEquipment/DroppedKerb = true
* si le nœud est une Entrance qui référence un EntranceEquipment dans Entrance/placeEquipments, avec EntranceEquipment/DropKerbOutside = true

Sinon, NOEUD_CHEMINEMENT.hauteurRessaut ne peut être renseigné.

## abaissePente

NOEUD_CHEMINEMENT.abaissePente ne peut être renseigné.

## abaisseLargeur

NOEUD_CHEMINEMENT.abaisseLargeur ne peut être renseigné.

## masqueCovisibilite

Pour les extrémités de SitePathLink, si le SitePathLink référence un CrossingEquipment dans SitePathLink/placeEquipments, NOEUD_CHEMINEMENT.masqueCovisibilite est renseigné à partir de CrossingEquipment/VisualObstacle avec les règles de gestion suivantes :

* aucun, si VisualObstacle=none
* stationnement voiture, si VisualObstacle=carParking
* végétation, si VisualObstacle=vegetation
* bâti, si VisualObstacle=building
* mobilier urbain, si VisualObstacle=streetFurniture
* autre, si VisualObstacle=other

Sinon, NOEUD_CHEMINEMENT.masqueCovisibilite ne peut être renseigné.

## controleBEV

NOEUD_CHEMINEMENT.controleBEV ne peut être renseigné.

## bandeInterception

NOEUD_CHEMINEMENT.bandeInterception ne peut être renseigné.
