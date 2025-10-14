# CNIG vers NeTEx

Cette partie de la documentation illustre le cas d'usage suivant : on dispose d'un ensemble de données conforme au standard CNIG Accessibilité et on souhaite le convertir vers le format NeTEx.

Un export NeTEx conforme au profil français se présente sous la forme d'une archive zip contenant plusieurs fichiers xml :

- le fichier [accessibility.xml](accessibility.md) regroupe les équipements et les informations de cheminement. C'est le fichier le plus important pour le cas d'usage de la conversion depuis le standard CNIG Accessibilité
- le fichier [parking.xml](parking.md) regroupe les informations sur les parkings. On y trouvera donc les informations sur les places de stationnement réservées aux personnes à mobilité réduite
- le fichier [poi.xml](poi.md) regroupe les informations sur les points d'intérêts. On y trouvera donc les informations relatives aux ERP et à leurs entrées
- le fichier [stop.xml](stop.md) regroupe les informations sur les arrêts, les stations, et les entrées sorties de gares
- d'autres fichiers xml non concernés par notre cas d'usage peuvent être présents, pour exporter les lignes de transport, les horaires, les tarifs, etc

Au sein de chaque fichier xml, les différents objets sont représentés en suivant le modèle de données européen [Transmodel](https://transmodel-cen.eu/), qui définit les concepts ainsi que les attributs utilisables pour les échanges de données. Les définitions des concepts sont reprises en français en préambule de chaque partie du profil NeTEx.

Voici les principaux concepts mobilisés pour convertir les données du standard CNIG Accessibilité :

- le CHEMINEMENT du modèle CNIG est exporté sous la forme d'un *NavigationPath* (fichier accessibility.xml)
- le TRONÇON_CHEMINEMENT du modèle CNIG est exporté sous la forme d'un *SitePathLink* (fichier accessibility.xml). S'il s'agit d'un équipement d'accès, d'autres objets seront exportés en complément.
- la CIRCULATION du modèle CNIG n'a pas réellement d'équivalent : ses caractéristiques sont utilisées pour compléter le *SitePathLink* correspondant au TRONÇON_CHEMINEMENT
- le NOEUD_CHEMINEMENT du modèle CNIG peut être exporté sous la forme d'un *PathJunction* (fichier accessibility.xml), principalement losqu'il s'agit d'une extrémité de tronçon de cheminement ne correspondant à aucun équipement.
- l'OBSTACLE n'a pas d'équivalent dans le modèle de données Transmodel. Certains types d'obstacles peuvent être exportés sous la forme d'*Equipment* (fichier accessibility.xml) mais pour l'essentiel, on utilisera leurs caractéristiques pour modifier les attributs du *SitePathLink* où ils se situent.
- la TRAVERSEE du modèle CNIG est exportée sous la forme d'un *CrossingEquipment* (fichier accessibility.xml)
- la RAMPE du modèle CNIG est exportée sous la forme d'un *RampEquipment* (fichier accessibility.xml)
- l'ESCALIER du modèle CNIG est exporté sous la forme d'un *StaircaseEquipment* (fichier accessibility.xml)
- l'ESCALATOR du modèle CNIG est exporté sous la forme d'un *EscalatorEquipment* (fichier accessibility.xml)
- le TAPIS_ROULANT du modèle CNIG est exporté sous la forme d'un *TravelatorEquipment* (fichier accessibility.xml)
- l'ASCENSEUR et l'ELEVATEUR du modèle CNIG sont exportés sous la forme d'un *LiftEquipment* (fichier accessibility.xml)
- l'ENTREE du modèle CNIG est exportée sous la forme d'un *EntranceEquipment* (fichier accessibility.xml), ainsi que d'un *StopPlaceEntrance* (fichier stop.xml) ou *PointOfInterestEntrance* (fichier poi.xml)
- le PASSAGE_SELECTIF n'a pas d'équivalent dans le modèle de données Transmodel. Ses caractéristiques peuvent cependant être utilisées pour modifier les attributs du *SitePathLink* où il se trouve.
- le QUAI du modèle CNIG est exporté sous la forme d'un *SitePathLink* (fichier accessibility.xml) et éventuellement d'un Quay (fichier stop.xml)
- le STATIONNEMENT_PMR du modèle CNIG est exporté sous la forme d'un *ParkingBay* (fichier parking.xml)
- l'ERP du modèle CNIG est exporté sous la forme d'un *PointOfInterest* (fichier poi.xml) et éventuellement d'un *StopPlace* (fichier stop.xml)
- le CHEMINEMENT_ERP peut être exporté sous la forme d'un *SitePathLink*

!!! info "Remarque"

    Il existe plusieurs manières de représenter une même réalité avec NeTEx. Ce documentation propose une approche, conforme à la norme NeTEx, au profil français et s'efforçant de respecter les usages recommandés dans le profil européen (EPIP). D'autres approches et d'autres modélisations restent possibles et valables.

    De même, il existe une grande quantité d'attributs NeTEx ; cette documentation s'efforce de couvrir tout ceux mobilisés par le standard CNIG Accessibilité, ainsi que les attributs obligatoires dans le cadre de la norme NeTEx et du profil français.

La suite de cette documentation présente chaque fichier de l'export NeTEx et les correspondances entre les attributs du standard CNIG et ceux de NeTEx pour chacun des objets.
