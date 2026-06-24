---
permalink: /
---

# Diakho CAMARA
**Développeuse Drupal fullstack confirmée**  
[diakho.camara@gmail.com](mailto:diakho.camara@gmail.com) &nbsp;|&nbsp; [0631003506](tel:+33631003506)

---

## Références projets

### Depuis mars 2024 · Galileo Global Education (groupe privée)

#### Refonte technique et graphique du site de l'école HETIC
Projet de refonte complète du site de l'école sur Drupal 10, avec modernisation de l'architecture et mise en place d'une gestion de contenus flexible via Group CMS et Layout Builder.

<details markdown="1">
<summary>Contributions</summary>

- Mise en place des briques de base Drupal : contrib modules, nodes, blocks, menus, taxonomies, views.
- Développement de modules custom pour répondre à des besoins spécifiques (field formatters, entités custom, etc.).
</details>

`Drupal 10` `PHP 8.3` `MySQL` `Composer` `Git` `DDEV` `Docker`

---

#### Middleware offres d'emploi
Développement d'un middleware en Drupal 10 servant de passerelle entre différents sites pour la centralisation et l'exposition des offres d'emploi via API, avec une attention particulière à l'optimisation SEO.

<details markdown="1">
<summary>Contributions</summary>

- Déploiement du middleware Drupal 10 (système de configuration, Composer, features, Drush, etc.).
- Conception et développement d'entités personnalisées pour modéliser les offres d'emploi.
- Développement et consommation d'API (exposition et intégration de données).
- Mise en place de la génération de rich snippets (données structurées Google) pour améliorer le référencement.
- Gestion des permissions et workflows pour un partage de données sécurisé.
- Optimisation des vues pour l'affichage et la structuration des données exposées.
</details>

`Drupal 11` `PHP 8.3` `MySQL` `Composer` `Git` `DDEV` `Docker`

---

#### Migration PHP 7.4 — sites écoles Drupal 7
Mise à niveau technique de plusieurs sites Drupal 7 dans le cadre d'une migration vers PHP 7.4, incluant la compatibilité des modules et la sécurité des plateformes.

<details markdown="1">
<summary>Contributions</summary>

- Audit des modules contrib et custom pour identifier les incompatibilités avec PHP 7.4.
- Mise à jour et adaptation du code custom (fonctions dépréciées, compatibilité).
- Tests et validation du fonctionnement global des sites après migration.
- Mise à jour des modules contrib pour garantir sécurité et stabilité.
</details>

`Drupal 7` `PHP 7.4` `MySQL` `Git` `Lando` `Docker`

---

#### Bloc "Hot Content" — mise en avant de contenus configurables
Module Drupal fournissant un bloc configurable en back office permettant aux éditeurs de sélectionner et filtrer dynamiquement des contenus mis en avant. Le module repose sur une introspection automatique des champs du bundle cible pour générer les options de filtrage sans configuration statique.

<details markdown="1">
<summary>Contributions</summary>

- Développement d'un service métier (`HotContentManager`) : détection automatique du bundle le plus peuplé via requête SQL directe, introspection des champs `entity_reference`, requêtage par conditions dynamiques et chargement des options de sélection.
- Plugin Block (`HotContentBlock`) avec formulaire back office : réglage du nombre d'éléments, génération dynamique des filtres (termes de taxonomie, nœuds liés), amélioration UX via jQuery SumoSelect.
- Enum PHP 8.1 (`EntityReferenceFieldsTargeted`) pour typer et contraindre les cibles de champs autorisées.
- Cache Drupal par tag d'entité pour l'invalidation automatique du bloc.
- Tests Kernel PHPUnit couvrant les quatre méthodes publiques du service.
- Intégration avec le système de rendu Drupal (view builder, mode d'affichage `teaser_hot_content`, template Twig dédié).
</details>

`Drupal 10/11` `PHP 8.3` `Symfony DI` `EntityQuery API` `PHPUnit (Kernel)` `jQuery / SumoSelect`

---

#### Bloc "Video Hub" — vidéothèque paginée avec données structurées Schema.org
Module Drupal fournissant une vidéothèque paginée en front end, avec injection automatique de données structurées Schema.org (`ItemList` + `VideoObject`) en `<head>` pour le référencement, extraction automatique de la durée des vidéos et provisionnement programmatique du type de médias à l'installation.

<details markdown="1">
<summary>Contributions</summary>

- Plugin Block (`VideoHubBlock`) avec pagination Drupal native, mode d'affichage dédié (`video_hub`) et génération de JSON-LD Schema.org injecté dynamiquement en `<head>`.
- Service `VideoHubManager` : récupération paginée via `PagerManagerInterface`, compilation des données template (URLs, dates formatées en français, durées ISO 8601) et construction des données Schema.org.
- Service `VideoMediaInstaller` exécuté à l'installation : détection ou création du type de médias vidéo, création programmatique des quatre champs requis, mode d'affichage et configuration des formulaires (avec support `field_group`).
- `hook_media_presave` pour l'extraction automatique de la durée via `getID3`, avec protection contre les ré-extractions inutiles.
- `hook_preprocess_media__video_hub` pour exposer URLs brutes et métadonnées formatées aux templates Twig.
- Cache par tag d'entité (`media_list`) et contexte de requête (`url.query_args:page`) pour l'invalidation ciblée.
</details>

`Drupal 10/11` `PHP 8.3` `Media API` `PagerManager` `getID3` `Schema.org / JSON-LD` `Twig`

---

#### Entité "Service externe" et intégration Avis Vérifiés (Skeepers)
Module Drupal combinant une entité de contenu personnalisée pour centraliser la gestion des services tiers (widgets, avis) et une intégration complète avec l'API Skeepers Verified Reviews : authentification OAuth2, récupération des notes de marque et injection de données structurées Schema.org `AggregateRating`.

<details markdown="1">
<summary>Contributions</summary>

- Entité `ExternalService` avec handlers complets (formulaires CRUD, list builder, contrôle d'accès, route provider) et interface d'administration (menus, onglets, permissions).
- Enum PHP 8.1 (`ServiceType`) pour typer les services disponibles et piloter le rendu du bloc via `match` expression.
- Plugin Block (`ExternalServiceBlock`) avec sélection par autocomplete et rendu adaptatif selon le type de service.
- Client API (`VerifiedReviewsClient`) : authentification OAuth2 `client_credentials`, token mis en cache jusqu'à expiry et retry automatique sur 401.
- Service `VerifiedReviewsRatingBuilder` construisant le JSON-LD `AggregateRating`, avec cache positif (1 h) et cache négatif (60 s) contre les indisponibilités API.
- Formulaire de configuration dédié pour la saisie sécurisée des credentials API.
</details>

`Drupal 10/11` `PHP 8.3` `Guzzle HTTP` `OAuth2` `Schema.org / JSON-LD` `Cache API Drupal`

---

#### Extension Schema.org `Course` — propriétés metatag personnalisées
Module Drupal étendant `schema_metatag` pour ajouter trois propriétés Schema.org manquantes dans le groupe `Course`, nécessaires au référencement des pages de formation des sites GGE.

<details markdown="1">
<summary>Contributions</summary>

- Trois plugins `@MetatagTag` dans le groupe `schema_course` : `educationalLevel`, `timeRequired` (ISO 8601) et `teaches`.
- Extension par héritage de `SchemaNameBase` pour une intégration native sans surcharge des handlers existants.
- Enrichissement des données structurées `Course` au-delà des propriétés couvertes par le module contrib.
</details>

`Drupal 10/11` `PHP 8.3` `schema_metatag` `Schema.org / JSON-LD`

---

#### Intégration IndexNow — notification automatique des moteurs de recherche (Drupal 7)
Développement de la fonctionnalité IndexNow au sein du module SEO GGE pour Drupal 7 : soumission automatique des URLs aux moteurs de recherche compatibles à chaque événement de cycle de vie d'un nœud.

<details markdown="1">
<summary>Contributions</summary>

- Hooks `hook_node_insert`, `hook_node_update` et `hook_node_delete` avec filtrage par type de contenu activé.
- Client HTTP (`client_submit`) envoyant une requête POST JSON à l'endpoint IndexNow via `drupal_http_request`, avec normalisation de la réponse et journalisation `watchdog`.
- Génération sécurisée de la clé IndexNow (32 caractères hex via `drupal_random_bytes`), formulaire de régénération et route `/{key}.txt` dédiée.
- Formulaire d'administration complet : endpoint configurable, timeout, soumission optionnelle à la suppression, sélection des types de contenu éligibles.
</details>

`Drupal 7` `PHP 7.4` `IndexNow API` `watchdog`

---

#### Synchronisation des produits de formation depuis Salesforce — Cours Florent
Développement en équipe distribuée (dont un développeur anglophone) d'un module Drupal 10 assurant l'import automatique des produits de formation depuis l'API Salesforce vers une entité personnalisée, avec synchronisation planifiée par cron. Projet conduit entièrement en anglais.

<details markdown="1">
<summary>Contributions</summary>

- Entité de contenu personnalisée `Product` avec handlers complets : storage, list builder, contrôle d'accès, Views data, route provider.
- Client Salesforce (`SalesforceClient`) via Guzzle : authentification OAuth2 avec token persisté en State API / TempStore, retry automatique (2 tentatives max) et journalisation PSR-3.
- Pattern Provider (`ProductProviderServiceInterface`) découplant la source réelle d'un service factice pour les environnements locaux et les tests.
- Service `ImportService` orchestrant la récupération et la création/mise à jour des entités, déclenché manuellement via formulaire back office ou automatiquement par cron.
- `CronHandler` : exécution planifiée avec intervalle configurable (défaut 1 h) et horodatage via State API.
- Commande Drush `cf_module:generate-products` pour la génération d'entités factices en développement.
- Outillage qualité : pipeline GitLab CI, PHP CS Fixer, PHP Mess Detector.
</details>

`Drupal 10/11` `PHP 8.3` `Guzzle` `Salesforce API` `OAuth2` `Drush` `GitLab CI` `PHP CS Fixer`

---

### De juin 2022 à mars 2024 · Opsone (agence web)

#### Refonte technique et graphique du site de la Mutuelle Familiale
Refonte sous Drupal 10 avec un focus sur la modularité de la création de contenus et la facilité d'administration.

<details markdown="1">
<summary>Contributions</summary>

- Mise en place des briques de base Drupal : contrib modules, nodes, blocks, menus, taxonomies, views.
- Mise en place de composants réutilisables.
- Développement de formulaires (demandes de devis, informations, etc.).
- Optimisation du back-office pour l'édition de contenus structurés.
</details>

`Drupal 10` `PHP 8.1` `Composer` `Git` `ElasticSearch`

---

#### Évolution du site Delphia Group Beneteau
Développement sous Drupal 10 pour la création d'une architecture modulaire et flexible permettant aux équipes éditoriales de créer et organiser efficacement les contenus.

<details markdown="1">
<summary>Contributions</summary>

- Mise en place des briques de base Drupal : contrib modules, nodes, blocks, menus, taxonomies, views.
- Mise en place de composants réutilisables pour l'édition des pages.
- Structuration des contenus via des logiques de taxonomie.
</details>

`Drupal 10` `PHP 8.1` `Composer` `Git` `ElasticSearch`

---

#### Refonte technique et graphique du site Terre de Vins
Refonte complète sous WordPress 6 pour améliorer la visibilité et les conversions (abonnements numériques/papier, espaces publicitaires) et répondre à des besoins métier complexes (imports, gestion éditoriale).

<details markdown="1">
<summary>Contributions</summary>

- Mise en place des briques de base WordPress (custom post types, taxonomies, hooks, champs personnalisés).
- Automatisation du processus d'import mensuel des fiches vins (description, notation, conseils, images).
- Gestion technique des contenus liés aux trophées et médailles.
- Personnalisation de l'interface d'administration (Meta Box, champs éditoriaux adaptés).
</details>

`WordPress 6` `PHP 8.1` `Composer` `Git`
