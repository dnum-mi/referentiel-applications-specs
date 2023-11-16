# Interactions with DSO Console

This page aims to specify the expected relationships with the console application of the Cloud PI Native Offer.

## Authentification

The DSO console is considered as a trusted application, so the authentification is limited to a JWT token as described into the "GestionDroits.md" file.

## POST to create a new application

To create a new application, the console makes a POST call to CANEL API. Below a sample of JSON as expected. Please take care of comments after the piece of code.    
````
{  
  "longname": "TEST202311141752",  
 	"description": "Fake application to illustrate data which are expected into a POST call from DSO Console",  
 	"organisation": "MI",
  "statut": "BLD",
 	"codeApplication": [{typeCode: "PAI", codeCourt: "TEST"}],  
 	"acteurRoles": [  
 		{  
 			"acteur":{email:"yves-marie.le-saux@interieur.gouv.fr"},  
 			"role":"SOUSC"  
 		}  
 	],  
 	"instances": [  
 		{  
 			"environnement": { "label": "Cloud PI Native" },
 			"tenant": "the.namespace.that.i.don't.remember.the.pattern",  
 			"role": "D",  
 			"statut": "PRD"  
 		}  
 	]  
}  
````
- **statut** : considering that an application initiated by the console before any instanciation on a cluster, the value will be "En construction" (code=BLD). I consider that attribute important, so thanks to DSO to hardcode it at "BLD" value
An open question is how to know that an instance is created to update this statut to "En production" (code=PRD).
- **typeApplication** : cannot be provided by DSO, so will initialized at "SVBUS" by default.
- **codeApplication** : must be optional; the information can be filled in into the console, but is not mandatory, so ...
- **acteurRoles** : we are sure that the Console can push, at least one actor (the souscripteur). **But the list can be extended to several actors.**
in addition, the console does not know the organisation of the actor (case of subcontractors), so if required into the DB, use the application's organisation.
- **instances** : showed to anticipate the next steps of CANEL.
- **instances/deploymentDate** : not kown by the console, but manage by the CICD, so ignored from now. Need additoinal work to specify.

