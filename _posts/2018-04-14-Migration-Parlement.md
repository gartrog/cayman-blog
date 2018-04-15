---
layout: post
title: Migration du Parlement
---

En suivant les instructions fournies par Eden

## Contents
Tout le contenu uploadé (images/photos/enregistrements): récupération par ftp depuis ftp.orchestrerie.com:/parlement/wp-content/uploads

``` bash
lftp ftp.orchestrerie.com
cd parlement/wp-content/uploads
mirror . uploads
```

![lftp]({{ site.baseurl }}/images/lftp.png)

Et dans l'autre sens:

``` bash
cd uploads
lftp ftp.orchestrerie.com
cd devenv/wp-content/uploads
mirror -R
```

## Data
Utilisation du plugin Wordpress Importer. Les posts et commentaires sont bien importés. En revanche il semble que pas mal d'erreurs soient faites.
* Miniatures improbables sur la page listant les derniers posts
* Toutes les images liées ne sont pas affichées. Feature ? Ce sont tous les liens vers parlement.orchestrerie.com. Lié à une protection sur le cross-site, qui sera résolue quand tout sera
  migré ?

## Users
Utilisation du plugin wordpress `WordPress Users & WooCommerce Customers Import Export Plugin`
pour export/import. Attention: tout n'a pas été importé (phrases de description, photos), mais l'essentiel a l'air d'y être.

## Corrections du site
* Dans `Pages`, suppression d'un certain nombre de pages redondantes
* Dans `Apparence/Personnaliser`, modifications du menu principal pour supprimer les doublons ainsi que `Connexion`. Devrait-on aussi virer `Inscription` ?

## Problèmes
* Import des dernières partitions mises en ligne: comment le faire automatiquement ? Pas évident ; en particulier les ID des fichiers sont différents.
* Photos: le Parlement utilise des 'portfolios', mais je ne vois pas comment créer ça dans devenv. Et même si on peut en créer, comment les importer ?

