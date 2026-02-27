# Firebase Analytics Properties — Pass Culture

> ⚠️ Avant de créer une nouvelle propriété, vérifier dans cette liste si une propriété similaire existe déjà.
> Mettre à jour ce fichier à chaque déploiement de nouvelles propriétés Firebase en production.

---

## Navigation et contexte

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `from` | string | ✅ Production | Source de navigation (ex: "home", "search", "artistPage") |
| `originDetail` | string | ✅ Production | Détail supplémentaire sur l'origine |

---

## Offres et contenus

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `offerId` | string | ✅ Production | Identifiant de l'offre |
| `categoryName` | string | ✅ Production | Catégorie de l'offre |
| `isHeadline` | boolean | ✅ Production | Indique si l'offre est mise en avant |

---

## Venues

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `venueId` | string | ✅ Production | Identifiant du lieu |

---

## Recherche

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `searchId` | string | ✅ Production | Identifiant de session de recherche |
| `searchDate` | string | ✅ Production | Date de la recherche |

---

## Modules home

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `moduleName` | string | ✅ Production | Nom du module |
| `moduleType` | string | ✅ Production | Type de module |
| `moduleId` | string | ✅ Production | Identifiant du module |

---

## Réservations

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `bookingId` | string | ✅ Production | Identifiant de réservation |
| `step` | string | ✅ Production | Étape du tunnel de réservation |

---

## Utilisateur

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `user_id` | string | ✅ Production | Identifiant utilisateur authentifié |
| `age` | integer | ✅ Production | Âge de l'utilisateur |

---

## Vidéo

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `videoId` | string | 🚧 Pas encore en prod | Identifiant de la vidéo |
| `seenDuration` | integer | ✅ Production | Durée visionnée en secondes |

---

## Badges et achievements

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `state` | string | ⚠️ Données non transmises | État du badge |
| `achievementName` | string | ✅ Production | Nom de l'achievement |

---

## Système

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `platform` | string | ✅ Production | iOS / Android |
| `system_theme` | string | ✅ Production | Thème système (snake_case — exception) |
| `theme_setting` | string | ✅ Production | Paramètre de thème (snake_case — exception) |

---

## Artistes

| Propriété | Type | Statut | Description |
|-----------|------|--------|-------------|
| `artistId` | string | 🚧 Pas encore en prod | Identifiant de l'artiste |
| `artistName` | string | 🚧 Pas encore en prod | Nom de l'artiste |

---

## Statuts

| Indicateur | Signification |
|-----------|--------------|
| ✅ Production | Actif et fonctionnel |
| 🚧 Pas encore en prod | Défini mais non déployé |
| ⚠️ Données non transmises | Problème technique |
| (OPEN) | Phase de test |

---

## Conventions de nommage

**Correct — camelCase :**
- `offerId` ✅
- `categoryName` ✅
- `isHeadline` ✅

**Incorrect — snake_case (sauf exceptions listées) :**
- `offer_id` ❌
- `category_name` ❌
