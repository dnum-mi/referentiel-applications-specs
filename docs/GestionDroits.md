# Gestion des droits des utilisateurs

**_Version_** : en cours

**_Discussions_** ouvertes

**_Thèmes manquants ou à renforcer:_**
- Description chainage Authentification-CLIENT-API

## Hypothèses de départ

Un utilisateur est identifié dans la table "Acteur"
La description de ces droits décrits dans ce document est limitée aux objets suivants:
- Acteur
- Rôle
- Application
- Conformité
- Environnement
- Instance
- Données de référence

Les droits sont de type CRUD (Create - Read - Update - Delete)

## Authentification d'un utilisateur

- Un utilisateur doit s'authentifier via Passage2.
- L'authentification via Passage2 doit donc pouvoir être associée à un acteur.
- Les accès via la Console DSO du Cloud PI Native sont supposés de confiance.
- Les appels d'API à partir de la Console DSO permettent de créer éventuellement un acteur correspondant à l'utilisateur connecté à la console, une application correspondant à l'usage de la console, et d'un rôle de "responsable d'application" reliant cet acteur et cette application.

**TODO**: mécanisme d'authentification PASSAGE2-CLIENT-API à décrire.

### Diagramme de séquence générique issu du modèle de DAG

```mermaid
sequenceDiagram
Navigateur->>+Application: 1.(HTTPS) requête d'accès
Application-->>-Navigateur: 2.(HTTPS) rediredction vers PASSAGE2 pour authentification
Navigateur->>+PASSAGE2: 3.(HTTPS) l'utilisateur s'authentifie sur PASSAGE2
PASSAGE2-->>-Navigateur: 4. (HTTPS) PASSAGE2 redirige le navigateur avec l'"authorization code flow" vers l'application
Navigateur->>+Application: 5.(HTTPS) Le navigateur de l'utilisateur fournit le code à l'application
Application-->>+PASSAGE2: 6.(HTTPS) L'application demande l'id token à PASSAGE2 grâce au code
PASSAGE2-->>-Application: 7. (HTTPS) PASSAGE2 répond en envoyant l'id token
Application-->>+PASSAGE2: 8.(HTTPS) L'application demande les infos de l'utilisateur
PASSAGE2-->>-Application: 9. (HTTPS) PASSAGE2 répond en envoyant les infos de l'utilisateur
Application-->>Navigateur: 10.(HTTPS) l'application ouvre l'accès à l'utilisateur en fonction de ses droits
```

## Définition des rôles 

Les rôles disposant de droits sur les objets sont définis dans le classeur Excel [CANEL2 _ Cartographie des utilisateurs du service v0.xlsx](https://resana.numerique.gouv.fr/public/perimetre/consulter/91576?information=7329509)
Ces rôles sont:
- Responsable d'application
- Gestionnaire de portefeuille
- Architecte d'entreprise
- RSSI
- Administrateur fonctionnel

Il est possible de décrire d'autres rôles dans CANEL pour mieux décrire une application, mais hors des rôles listés ci-dessus, les autres rôles n'offrent pas de droits sur les données de CANEL.

Si un utilisateur dispose de plusieurs rôles sur un objet, les droits appliqués sont les plus ouverts.

Les droits sont contrôlés au niveau des micro-services CANEL.

## Attributions des rôles

_Remarque du 23/05/2023: l'objet "Portefeuille" n'est pas décrit; le rôle de Gestionnaire de Portefeuille ne peut donc lui être associé, or les droits sur les applications sont effectués par transitivité au travers de cet objet. Le tableau ci-dessous représente donc une anticipation._

|                              | Acteur |  Rôle  | Application | Conformité | Environnement | Instance | Données de référence |
|------------------------------|--------|--------|-------------|------------|---------------|----------|----------------------|
|  **Responsable d'application**   |   R    | CRU sur ses applications | CRU sur ses applications | CRU sur ses applications |     R         | CRU sur ses applications |         R            |
| **Gestionnaire de portefeuille** |   R    | CRU sur ses applications | CRU sur ses applications | CRU sur ses applications |     R         | CRU sur ses applications |         R            |
|   **Architecte d'Entreprise**    |  CRU   |  CRU   |     CRU     |    CRU     |    CRU        |   CRU    |         R            |
|            **RSSI**              |   R    |   R    |      R      |    CRU     |     R         |    R     |         R            |
|  **Administrateur fonctionnel**  |  CRU   |   R    |      R      |     R      |     R         |    R     |        CRUD          |
