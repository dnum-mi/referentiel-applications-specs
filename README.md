# Spécification du produit CANEL

## Modalités de gestion

Ce chapitre décrit les modalités de gestion des spécifications fonctionnelles du projet CANEL. Les spécifications sont réalisées au format markdown (md).
Nous disposons d'une spécification par objet. Pour l'usage de ces objets, des fiches de spécifications sont réalisées spécifiquement.

La branche **main** contient les spécifications validées du projet CANEL. Cette branche est initialisée avec l'état de l'application en cours.
Les remarques, propositions d'évolutions et besoins de nouvelles spécifications sont exprimées vies des **issues**.

Une **issue** peut avoir deux statut: OPEN ou CLOSED.

Les propositions d'évolution des spécifications sont faites au travers de branches, au travers des branches.
Lorsque la proposition est validée et formalisée dans la spécification, la branche est fondue dans la branche **main**.

Une nouvelle **issue** est alors créée dans le repository de l'application pour prise en compte.
Cette nouvelle **issue** est lors associée à deux labels: **Test to implement**, et **To implement**.
Lorsque les tests sont codés, le label **Test to implement** est supprimé, et un label **Test covergage OK** est ajouté.
Lorsque l'issue est prise en compte dans le code applicatif, le label **To implement** est supprimé, et un label **Implemented** est ajouté.


```mermaid
graph TD
id01[Les spécifications sont initialisées dans la branche **main** du référentiel **specs**] --> idIssue01[Les demandes d'évolutions sont ajoutées sous forme d'issues, de façon unitaire]
idIssue01 --> idSpec01[Une nouvelle branche de spécification est créée pour les évolutions des documents de spécification]
idSpec01 --> idSpec02((Evol Spécification complètes))
idSpec02 --> idSpec03[La branche de spécification est fusionnée dans la branche **main**]
idSpec03 --> idAppli01[Une issue est créée dans le référentiel de l'application]
idSpec03 --> idSpec04[Cloturer l'issue de spécification]
idAppli01 --> idAppli02[Deux labels sont ajoutés à cette issue: **To Implement** et **Tests to Implement**]
idAppli02 --> idAppli03((Tests implémentés))
idAppli03 --> idAppli04[Supprimer le label **Tests to Implement** et ajouter un label **Tests implemented**]
idAppli02 --> idAppli05((Code updated))
idAppli05 --> idAppli06[Supprimer le label **To Implement** et ajouter un label **Implemented**]
idAppli06 --> idAppli07[Cloturer l'issue applicative]
idAppli04 --> idAppli07
```


## Vue globale des objets

```mermaid
classDiagram
direction LR

class Application {
	}
class Role {
	}
class Acteur {
	}
class Conformite {
	}
class TypeConformite {
	}
class Environnement {
  }
class Instance {
  }
class Pile  {
  }
class Technologie {
  }
  
link Application "https://github.com/dnum-mi/canel-specs/blob/main/docs/Application.md" "Application"
link Role "https://github.com/dnum-mi/canel-specs/blob/main/docs/Application.md" "Role"
link Acteur "https://github.com/dnum-mi/canel-specs/blob/main/docs/Application.md" "Acteur"
link Conformite "https://github.com/dnum-mi/canel-specs/blob/main/docs/Application.md" "Conformite"
link TypeConformite "https://github.com/dnum-mi/canel-specs/blob/main/docs/Application.md" "TypeConformite"

link Environnement "https://github.com/dnum-mi/canel-specs/blob/main/docs/Environnement.md" "Environnement"
link Instance "https://github.com/dnum-mi/canel-specs/blob/main/docs/Environnement.md" "Instance"

link Technologie "https://github.com/dnum-mi/canel-specs/blob/main/docs/Technologie.md" "Technologie"
link Pile "https://github.com/dnum-mi/canel-specs/blob/main/docs/Technologie.md" "Pile"

Application "1" <--> "*" Role
Application "1" <..> "*" Application
Role "*" <--> "1" Acteur
Application "1" <--> "*" Conformite
Conformite "*" <--> "1" TypeConformite
Application "1" <--> "*" Instance
Instance "*" <--> "1" Environnement
Application "1" <--> "*" Pile
Pile "*" <--> "1" Technologie
```
