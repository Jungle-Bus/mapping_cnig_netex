# NeTEx vers CNIG

Cette partie de la documentation illustre le cas d'usage suivant : on dispose d'un export NeTEx conforme au profil français et on souhaite le convertir vers le standard CNIG Accessibilité.

Un export conforme au standard CNIG Accessibilité se présente sous la forme d'un jeu de données comportant un catalogue d'objets désignés ici en lettres capitales : TRAVERSEE, RAMPE, ESCALIER, etc

Le SitePathLink NeTEx est l'élément central de notre cas d'usage :

- il sera converti en TRONÇON_CHEMINEMENT
- dans certains cas, il sera converti une seconde fois, en TRAVERSEE, RAMPE, ESCALIER, ESCALATOR, TAPIS_ROULANT ou CIRCULATION
- les équipements NeTEx référencés par le SitePathLink (CrossingEquipment, StaircaseEquipment, etc) peuvent venir compléter les objets CNIG ainsi créés en apportant des attributs spécifiques

Le NavigationPath NeTEx sera converti en CHEMINEMENT.

Les Entrance NeTEx (StopPlaceEntrance, PointOfInterestEntrance ou ParkingPassengerEntrance) seront converties en ENTREE, en s'appuyant sur l'EntranceEquipment NeTex pour compléter les attributs.

Le PointOfInterest NeTEx permettra de créer l'ERP.

Le ParkingBay NeTEx sera converti en STATIONNEMENT_PMR.

D'autres objets NeTEx seront mobilisés au cas par cas mais ont une équivalence plus limitée avec le modèle CNIG.

!!! info "Remarque"

    Il existe plusieurs manières de représenter une même réalité avec NeTEx. Ce documentation s'appuie sur une approche, conforme à la norme NeTEx et au profil français. D'autres approches et d'autres modélisations non mentionnées ici restent possibles et valables.

    Par ailleurs, sur de plusieurs notions, l'approche du standard CNIG Accessibilité est plus précise que celle choisie par NeTEx. En conséquence, des approximations seront parfois réalisées dans les conversions d'attributs. 
    
    De plus, il y a plus de champs obligatoires dans le standard CNIG que côté NeTEx, donc la transformation depuis un export NeTEx ne peut garantir la complétude de tous les attributs obligatoires.

La suite de cette documentation présente chaque classe d'objet CNIG et les correspondances entre les attributs de NeTEx et ceux du standard CNIG.

