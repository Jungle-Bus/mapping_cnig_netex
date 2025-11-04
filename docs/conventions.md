# Conventions de représentation

NeTEx s'appuie sur le format XML, qui repose sur une syntaxe avec des balises entourées de chevrons.

Dans l'exemple suivant représentant un *TravelatorEquipment* :

```xml
<TravelatorEquipment id="ALM:TravelatorEquipment:w45561_n2_n502:LOC" version="152">
        <PublicCode>FC2</PublicCode>
        <Width>0.2</Width>
        <DirectionOfUse>both</DirectionOfUse>
        <TactileActuators>true</TactileActuators>
</TravelatorEquipment>
```

`TravelatorEquipment/@id` représente l'attribut xml `id` de l'élément TravelatorEquipment.

`TravelatorEquipment/PublicCode` représente l'élément `PublicCode`, contenu dans l'élément TravelatorEquipment. Dans cette documentation, on pourra parler de l'attribut NeTEx PublicCode de l'objet TravelatorEquipment, mais il ne s'agira ici pas de l'attribut au sens xml mais au sens modèle de données.

Le standard CNIG Accessibilité s'appuie sur des classes d'objets disposant chacune d'attributs.

TAPIS_ROULANT.idTapisRoulant représente l'attribut idTapisRoulant de la classe d'objet TAPIS_ROULANT

Étant donné un attribut (CNIG ou NeTEx) *attribut_qcq*, les conventions suivantes sont utilisées pour décrire les valeurs qu'il peut prendre :

- attribut_qcq=* signifie que l'attribut est renseigné avec n'importe quelle valeur
- attribut_qcq=42 signifie que l'attribut est renseigné avec la valeur "42"
- attribut_qcq=haut/bas signifie que l'attribut est renseigné soit avec la valeur "haut" soit avec la valeur "bas"
- attribut_qcq!=haut signifie que l'attribut est renseigné et que valeur est différente de "haut"
- attribut_qcq!=haut/bas signifie que l'attribut est renseigné et que valeur n'est ni "haut" ni "bas" (par exemple attribut_qcq=milieu)
- attribut_qcq non renseigné signifie que l'attribut n'est pas présent ou qu'il a une valeur vide
