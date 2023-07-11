# Recherche floue d'applications via API

## Besoin global

Nous devons disposer d'un moyen de rechercher des objets Applications dans CANEL2 avec une recherche peu structurée. L'enjeu est d'identifier des moyens soutenant des usages.

## Première cible

La première réponse à ce besoin est de disposer d'une recherche lexicale dans les noms et descriptions des applications.
La formulation de la recherche est une suite de mots ou d'expressions. Une expression est une suite de mots encadrée par des guillemets.
Chaque unité lexicale est recherchée dans:
- le nom de l'application
- la description de l'application
- le libellé ou la description des données associées à l'application [sous réserve de la mise en oeuvre du référencement des données]
- le libellé ou la description des données associées à des flux, eux-même associés à des applications [sous réserve de la mise en oeuvre du référencement des données, et des flux inter-applications]

### Accès à la fonction

La recherche sera accessible via API. Elle retournera une liste d'applications sur le même principe que l'appel de l'API via "/canel/api/v1/applications/".
L'appel de l'API devra suivre une notation Google en se référant aux recommandations définies sur le site de chez Octo. La recherche globale inclue le principe de recherche approchante.
Sur le site il est proposé de définir la recherche au niveau Applications dans la mesure où cette recherche est destinée à remonter des objets application. (GET /canel/api/v1/applications/search?q=titre&limit=10).

### Remarques

il est possible de réaliser des recherches floues/approchantes/globales depuis postgresql (levenshtein) si on ne veut pas instancier dans un premier temps de solution de type elasticsearch.
solution à tester :https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/search/


## Evolutions

1. La recherche doit pouvoir intégrer le libellé des données dans les éléments soutenant la recherche.
1. La notion d'usage peut être décrite par des objets Capacité (non décrits aujourd'hui). Le champ de la recherche sera étendue à ces objets lorsqu'ils seront implémentés.
