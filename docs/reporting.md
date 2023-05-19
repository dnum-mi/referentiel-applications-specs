# Gestion des rapports

_**Version**_ : en cours

_**Discussion**_ : ouverte


## API _ Fonction d'export
Une requête doit permettre de générer un CSV de l'objet visé.

### export des données d'une application


## IHM _ Fonction d'export :
La fonction d'export, au travers de l'IHM, doit permettre de selectionner les champs de l'objet visé qui doivent apparaitre dans le fichier CSV généré.

La fonction doit permettre l'export simplifié des objets suivants :
Application : 
- La liste des applications. les champs fournis par défaut sont : [object application] **nom, entité organisationnelle responsable,** description, statut, date de mise en production, commentaire, date de mise a jour
- Les applications d'une organisation responsable. les champs fournis par défaut sont : [object application] **entité organisationnelle responsable, nom** description, statut, date de mise en production, commentaire, date de mise a jour
- Les applications sensibles [*cette selection est soumise à un profil utilisateur particulier*]. les champs fournis par défaut sont : [object application] **sensibilté, nom, entité organisationnelle responsable,** description, statut, date de mise en production, commentaire, date de mise a jour
- Les applications présentant des conformités [variantes : dont la conformité est encore valide, dont la conformité approche d'une date d'échéance, dont la conformité n'est pas encore actée]. les champs fournis par défaut sont : [objet conformité]**type de conformité**, niveau de conformité, date decision conformité, date échéance conformité [object application] **sensibilté, nom, entité organisationnelle responsable,** description, statut, date de mise en production, commentaire, date de mise a jour


Acteur : 
- La liste des acteurs selon leur statut (actif ou inactif). Les champs fournis par défaut sont : [objet acteur] **nom**, email, entité de rattachement, commentaire, date de mise a jour
- La liste des acteurs et les applications dans lesquels ils jouent actuellement un rôle. Les champs fournis par défaut sont : [objet acteur] **nom**, email, entité de rattachement, commentaire, date de mise a jour; [objet application] **nom de l'application**, description, statut [association rôle]  rôle  


** A compléter ** 

Nota bene : en gras les champs sur lesquels se font l'ordonnancement/ regroupement
