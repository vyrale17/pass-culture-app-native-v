# Example Jira Tickets

## 1. User Story: Feedback Collection

**Title:** [Front] Collect user feedback on review usefulness

**Context:**
Users currently have no way to signal whether cultural reviews help their decision-making. Adding a simple rating mechanism will improve content quality and provide engagement data for the editorial team.

**User Story:**
En tant que jeune utilisateur, j'aimerais pouvoir indiquer si un avis critique m'a été utile, afin d'aider à valoriser les contenus pertinents.

**Business Rules:**
- Display "Trouves-tu ces avis utiles ?" with yes/no buttons below each review section
- Feature flag controlled, disabled by default
- Only shown when review section is visible (≥1 review)
- Linking to external survey on button tap

**Acceptance Criteria:**
- [ ] Scénario : Affichage du module feedback
  - Given l'utilisateur est sur une fiche offre avec des avis
  - And le feature flag est activé
  - When la section avis est visible
  - Then le module "Trouves-tu ces avis utiles ?" s'affiche sous les avis

- [ ] Scénario : Interaction avec le bouton "Oui"
  - Given le module feedback est affiché
  - When l'utilisateur tape "Oui"
  - Then l'utilisateur est redirigé vers le lien du survey externe

---

## 2. Bug Report: Search Duplicates

**Title:** [Back] Fix duplicate results in team member search for large groups

**Context:**
Team member searches return 2-3 duplicate entries for groups exceeding 10 members, creating confusion and degrading trust in search accuracy.

**Environment:** Chrome 131, macOS 14.2, v2.4.1

**Steps to reproduce:**
1. Navigate to team management
2. Search for any member in a group with >10 members
3. Observe duplicate entries in results

**Root Cause:** Missing DISTINCT clause in the SQL query joining member and group tables.

**Acceptance Criteria:**
- [ ] Scénario : Recherche sans doublons
  - Given un groupe avec plus de 10 membres
  - When l'utilisateur effectue une recherche
  - Then chaque membre n'apparaît qu'une seule fois dans les résultats

---

## 3. Task: Cloud Migration

**Title:** [Back] Migrate avatar images from S3 to Cloudflare R2

**Context:**
Current S3 costs are $450/month for 2.4M avatar images. Migration to Cloudflare R2 reduces this to $130/month with zero-downtime requirements.

**Business Rules:**
- Batch processing: 10,000 images per batch
- Validation: 0.5% sample testing after each batch
- Rollback window: 30 days
- Zero downtime required during migration

**Acceptance Criteria:**
- [ ] Scénario : Migration sans interruption
  - Given le service est en production
  - When la migration s'exécute
  - Then aucune interruption de service ne survient

---

## 4. Epic: Offline Functionality

**Title:** [Front] Enable core features in offline mode

**Context:**
60% of mobile users experience connectivity issues affecting document viewing, task creation, and calendar access. Offline support will maintain engagement during network outages.

**Business Rules:**
- Storage limit: 500MB per user
- Supported features: document viewing, task creation, calendar access
- Conflict resolution via IndexedDB and service workers

**Acceptance Criteria:**
- [ ] Scénario : Consultation de document hors ligne
  - Given l'utilisateur a préalablement chargé un document
  - When la connexion est perdue
  - Then le document reste accessible en lecture
