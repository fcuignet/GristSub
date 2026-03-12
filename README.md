# Widget Grist --- Intégration Data.Subvention

Ce projet fournit un **widget HTML pour Grist** permettant d'interroger
automatiquement l'API **Data.Subvention** afin de récupérer les
informations relatives à une association et aux subventions qui lui sont
attribuées.

Le widget s'intègre directement dans une vue **Custom Widget** de Grist
et permet d'alimenter automatiquement des colonnes d'une table à partir
du **SIRET / SIREN** d'une organisation.

------------------------------------------------------------------------

# Fonctionnalités

-   Connexion à l'API **Data.Subvention**
-   Recherche automatique d'une association à partir du **SIREN**
-   Récupération des **subventions associées**
-   Enregistrement du **JSON complet de réponse** dans Grist
-   Traitement :
    -   d'une **ligne sélectionnée**
    -   de **toutes les lignes visibles**
-   Configuration dynamique du **mapping des colonnes**
-   Gestion des erreurs API
-   Temporisation configurable entre appels API
-   Limitation optionnelle du nombre de lignes traitées

------------------------------------------------------------------------

# Architecture

Le widget fonctionne entièrement côté client.

    Grist Table
         │
         │ (plugin API)
         ▼
    Widget HTML / JavaScript
         │
         │ requêtes HTTP
         ▼
    API Data.Subvention

Les données récupérées sont ensuite **écrites directement dans la table
Grist** via l'API du plugin.

------------------------------------------------------------------------

# Données récupérées

Le widget interroge les endpoints suivants :

    https://api.datasubvention.beta.gouv.fr/association/{SIREN}
    https://api.datasubvention.beta.gouv.fr/association/{SIREN}/grants

Les réponses JSON sont stockées dans des colonnes dédiées dans la table.

------------------------------------------------------------------------

# Pré‑requis

-   un document **Grist**
-   une table contenant au minimum :
    -   un **SIRET**
    -   un **SIREN**
-   un **token API Data.Subvention**

Documentation API :

https://api.datasubvention.beta.gouv.fr

------------------------------------------------------------------------

# Structure des colonnes recommandées

  Colonne           Description
  ----------------- -------------------------------
  SIRET             identifiant établissement
  SIREN             identifiant organisation
  ds_status         statut du traitement
  ds_error          message d'erreur
  ds_assos_json     JSON complet de l'association
  ds_assos_grants   JSON complet des subventions

------------------------------------------------------------------------

# Installation

## 1 --- Ajouter un widget dans Grist

Dans votre document :

Add Widget → Custom Widget

## 2 --- Charger le widget

Deux possibilités :

### Option A --- URL

héberger le fichier HTML du widget sur un serveur accessible.

### Option B --- fichier local

utiliser le fichier HTML directement dans Grist.

------------------------------------------------------------------------

# Configuration

Au premier lancement :

1.  saisir votre **token Data.Subvention**
2.  sélectionner les colonnes à utiliser

Mapping recommandé :

    SIRET
    SIREN
    ds_status
    ds_error
    ds_assos_json
    ds_assos_grants

Le mapping est sauvegardé dans le **localStorage du navigateur**.

------------------------------------------------------------------------

# Utilisation

## Traitement d'une ligne

1.  sélectionner une ligne dans la table
2.  cliquer sur :

```{=html}
<!-- -->
```
    Charger la ligne sélectionnée

Le widget :

1.  récupère le **SIREN**
2.  appelle l'API
3.  écrit les données dans la ligne

------------------------------------------------------------------------

## Traitement en lot

Cliquer sur :

    Traiter toutes les lignes visibles

Options disponibles :

  paramètre   rôle
  ----------- --------------------------------
  délai       temporisation entre appels API
  limite      nombre maximum de lignes

Exemple :

    délai : 3000 ms
    limite : 100

------------------------------------------------------------------------

# Gestion des erreurs

Les erreurs API sont stockées dans la colonne :

    ds_error

Le statut global est écrit dans :

    ds_status

Valeurs possibles :

    ok_partiel_ou_total
    erreur

------------------------------------------------------------------------

# Sécurité

Le **token API** :

-   n'est **jamais stocké dans Grist**
-   est conservé uniquement **dans la session du widget**

------------------------------------------------------------------------

# Cas d'usage

Ce widget peut servir à :

-   analyser les financements publics des associations
-   enrichir une base **SIREN / SIRET**
-   croiser des données d'organisations avec les subventions publiques
-   automatiser l'enrichissement d'une base Grist

------------------------------------------------------------------------

# Améliorations possibles

-   extraction automatique de champs JSON vers des colonnes
-   historisation des subventions
-   filtrage par dispositif
-   normalisation des montants
-   intégration avec d'autres APIs publiques (INSEE, RNA)

------------------------------------------------------------------------

# Licence


MIT

------------------------------------------------------------------------

# Auteur

Widget développé pour l'intégration **Grist + Data.Subvention** par frederic cuignet royer
