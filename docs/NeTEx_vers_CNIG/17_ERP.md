# ERP

Un objet ERP est construit pour chaque objet NeTEx PointOfInterest, qu'on retrouve dans le fichier poi.xml.

On utilisera la géométrie de l'objet NeTEx (en général PointOfInterest/gml:Polygon) pour construire la géométrie de l'ERP. 

Une géométrie polygonale est attendue. Une projection peut être nécessaire (le système de référence utilisé par défaut pour NeTEx est le WGS 84).

## idERP

ERP.idERP peut être construit à partir de l'identifiant de l'objet NeTEx (PointOfInterest/@id) en utilisant la codification des identifiants du standard CNIG.

## nom

ERP.nom est rempli avec la valeur de PointOfInterest/Name.

## adresse

ERP.adresse est rempli avec la valeur de PointOfInterest/PostalAddress/AddressLine1.

À défaut, on concaténera les valeurs des attributs suivants pour construire ERP.adresse :

* PointOfInterest/PostalAddress/BuildingName
* PointOfInterest/PostalAddress/HouseNumber
* PointOfInterest/PostalAddress/Street

## codePostal

ERP.codePostal est rempli avec la valeur de PointOfInterest/PostalAddress/PostCode.

## erpCategorie

ERP.erpCategorie ne peut être renseigné.

## erpType

ERP.erpType ne peut être renseigné.

## dateMiseAJour

ERP.dateMiseAJour peut être renseigné à partir de PointOfInterest/@changed.

À défaut, il est également possible d'utiliser PublicationDelivery/PublicationTimestamp du fichier poi.xml.

## sourceMiseAJour

ERP.sourceMiseAJour peut être renseigné à partir de PointOfInterest/@dataSourceRef.

## stationnementERP

ERP.stationnementERP ne peut être renseigné.

## stationnementPMR

ERP.stationnementPMR ne peut être renseigné.

## accueilPersonnel

ERP.accueilPersonnel est renseigné à partir des attributs de l'objet AssistanceService référencé dans PointOfInterest/equipmentPlaces avec les règles de gestion suivantes :

* personnel formé à l’accueil des publics spécifiques si AssistanceService/AccessibilityTrainedStaff est vrai
* personnel non-formé à l’accueil des publics spécifiques si si AssistanceService/AccessibilityTrainedStaff est faux
* absence de personnel si AssistanceService/Staffing=unmanned

À défaut, on utilisera l'élément Staffing de PointOfInterest/facilities avec les régles de gestion suivantes :

* absence de personnel si Staffing contient la valeur unmanned

## accueilBIM

ERP.accueilBIM ne peut être renseigné.

## accueilBIMPortative

ERP.accueilBIMPortative ne peut être renseigné.

## accueilLSF

ERP.accueilLSF ne peut être renseigné.

## accueilST

ERP.accueilST ne peut être renseigné.

## accueilAideAudition

ERP.accueilAideAudition ne peut être renseigné.

## accueilPrestations

ERP.accueilPrestations ne peut être renseigné.

## sanitairesERP

ERP.sanitairesERP est vrai s'il y a au moins un objet SanitaryEquipment référencé dans PointOfInterest/equipmentPlaces.

## sanitairesAdaptes

ERP.sanitairesAdaptes est le nombre d'objets SanitaryEquipment avec WheelchairAccess=true (dans SanitaryEquipment/AccessibilityAssessment) référencés dans PointOfInterest/equipmentPlaces.

## telephone

ERP.telephone est rempli à partir de PointOfInterest/OperatingOrganisationView/ContactDetails/Phone.

## siteWeb

ERP.siteWeb est rempli avec la valeur de l'attribut PointOfInterest/Url.

## siret

ERP.siret ne peut être renseigné.

## latitude

ERP.latitude est construit à partir de PointOfInterest/Centroid/Location/Latitude. À défaut, il est aussi possible de le calculer à partir de la géométrie du PointOfInterest (PointOfInterest/Polygon).

Une projection peut être nécessaire (le système de référence utilisé par défaut pour NeTEx est le WGS 84).

## longitude

ERP.longitude est construit à partir de PointOfInterest/Centroid/Location/Longitude.À défaut, il est aussi possible de le calculer à partir de la géométrie du PointOfInterest (PointOfInterest/Polygon).

Une projection peut être nécessaire (le système de référence utilisé par défaut pour NeTEx est le WGS 84).
