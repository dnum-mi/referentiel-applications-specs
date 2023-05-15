# Gestion des environnements


## Introduction

Un environnement représente un espace d'hébergement d'applications.
Il est associée à une application par le concept d'instance.

Une instance est la mise en œuvre d'une application dans un espace d'hébergement.
Elle est associée à un rôle (production/master, production/slave, pré-production, métrologie, qualification, intégration, développement)
Elle est associée à un statut (en préparation, en exécution, en retrait de service ou décommissionnée).
Ce statut est distinct du statut de l'application, même si ce dernier en est dépendant.

Il n'est pas pertinent de recenser par ce type de description les instances logicielles sur poste de travail.
Si l'on souhaite toute de même tracer un certain niveau de déploiement, il est possible de décrire un environnement "virtuel" représentant les postes de travail, et d'y instancier les applications concernées.
La maintenance de ce grain d'information me semble toutefois trop fine, et relève plus d'une CMDB que d'un référentiel d'entreprise.

## Modèle de données conceptuel

### Environnement

Un environnement représente un espace d'hébergement physique.
Par conséquent, chaque datacenter sera représenté par au moins un environnement.
Un environnement est cohérent dans son modèle de gestion (principes et outils).
Par conséquent, dans le cas de l'offre Cloud PI Native, nous aurons un environnement par cluster.
De même, l'offre IaaS de Cloud PI Gen2 constitue un plusieurs environnements, selon le nombre de datacenters portant cette capacité.

Ses attributs sont:
- un __label__ sur 100 caractères [obligatoire]
- l'__organisation__ responsable de l'environnement  [obligatoire] - nous recommandons de pas lier cette information à la table "Organisation" pour d'y inclure des opérateurs privés.
- le __type__ [obligatoire]: Enum [CaaS, IaaS, VM, Serveur]
- la __protection__ [obligatoire]: Enum [NP, DR]
- la __localisation__ [facultatif] - texte libre
- un __commentaire__ [facultatif] - texte libre
- Les données de __suivi__ (auteur et date de CRU) [obligatoire]

## Instance

Une instance fait le lien entre une application et un environnement.
Elle porte en outre des caractéristiques propres.

Ses attributs sont donc:
- lien vers une __application__ [obligatoire]
- lien vers un __environnement__ [obligatoire]
- __rôle__ [obligatoire] : Enum [production/actif, production/passif, pre-production, metrologie, qualification, integration, developpement, formation]
- __statut__ [obligatoire]: Enum [construction, production, retrait de service, décomissionnée]
	- **_Construction_**: l'instance existe, mais n'est pas terminée. Ce statut ne devrait exister que pour des rôles de développement ou intégration.
	- **_Production_**: l'instance est complète, et est disponible pour les usages relatifs à son rôle
	- **_Retrait de service_**: l'instance persiste, mais son usage est limité à des motifs techniques préliminaires à son décommissionnement
	- **_Décommissionnée_**: l'instance a été retiré de l'environnement technique
- __Tenant__ [facultatif]: adresse du tenant, ou namespace (dans le cas d'un déploiement K8S)
- __FIP__ [facultatif]: adresse externe de l'application; il peut y avoir plusieurs FIP pour une seule application, donc zone de texte libre; remarque: dans le cas d'une application dans un cluster Kubernetes, les FIP sont attribuées au cluster, donc pas de FIP pour l'application.
- __URL__ [facultatif]: adresse logique de l'application; il peut y avoir plusieurs URL pour une seule application, donc zone de texte libre
- __Date de déploiement__ [facultatif]: date de dernier 
- __Commentaire__ [facultatif]
- Les données de __suivi__ (auteur et date de CRU) [obligatoire]
