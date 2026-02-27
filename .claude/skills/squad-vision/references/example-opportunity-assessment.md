# Exemple — Opportunity Assessment : Favoris Artistes & Venues

**Auteur :** PM Squad Découverte
**Date :** Janvier 2025

---

## TL;DR

Un utilisateur qui découvre un artiste via la home ou la recherche n'a aucun moyen de le retrouver lors de sessions ultérieures. Cette friction limite l'engagement récurrent. Nous proposons d'ajouter une fonctionnalité de favoris sur les pages artistes et venues. Si 10% des utilisateurs actifs créent au moins un favori, chaque retour représente une session de découverte qualifiée supplémentaire. Recommandation : GO conditionnel (budget T2 + alignement Squad Conversion).

---

## Problème

### Observations
- Aucun mécanisme de sauvegarde d'artistes ou de venues n'existe aujourd'hui
- Les utilisateurs qui découvrent un artiste via la home n'ont aucun moyen de le retrouver
- [Taux de re-visite des pages artistes — À compléter]

### Utilisateurs impactés
Tous les utilisateurs actifs ayant consulté au moins une page artiste ou venue (~[À compléter]% de la base active).

### Sévérité
- [x] Important — crée une friction significative entre la découverte et le ré-engagement

---

## Opportunité

### Pourquoi maintenant ?
Les pages artistes enrichies (T1 2025) vont augmenter le trafic sur ce type de page. C'est le moment idéal pour ajouter un mécanisme de rétention.

### Impact potentiel
Si 10% des utilisateurs actifs créent au moins un favori, chaque retour initié depuis les favoris génère une session de découverte qualifiée (score NSM supérieur à la moyenne).

### Conséquence de l'inaction
Sans favoris, l'investissement dans les pages enrichies profite à la découverte ponctuelle mais ne crée pas de boucle de ré-engagement.

---

## Impact attendu

| Métrique | Baseline | Estimation post-lancement | Confiance |
|----------|----------|--------------------------|-----------|
| Sessions initiées depuis favoris | 0 | [À compléter après fake door] | Faible |
| Points NSM par session favoris | [À compléter] | > moyenne sessions | Moyenne |

**Hypothèses sous-jacentes :**
- 10% des utilisateurs actifs créeront au moins 1 favori
- Les sessions depuis favoris génèrent plus de points de découverte que la moyenne

---

## Solution proposée

### Direction haut niveau
- Ajouter un bouton "Mettre en favori" sur les pages artistes et venues
- Créer une section dédiée aux favoris accessible depuis la home
- Intégrer des notifications via la Squad Conversion (phase 2)

### Hors scope
- Favoris sur les offres (traité séparément)
- Recommandations basées sur les favoris (phase ultérieure)

---

## Effort & Risques

| Dimension | Évaluation |
|-----------|-----------|
| Complexité | Moyenne |
| Durée estimée | 6-8 semaines |
| Équipes nécessaires | Front, Back, Data, Design |

### Risques principaux
| Risque | Mitigation |
|--------|-----------|
| Faible adoption utilisateur | Fake door test à 5% avant développement |
| Dépendance Squad Conversion (notifications) | Lancer sans notifications en phase 1 |

### Alternatives rejetées
- Historique de navigation — rejeté car passif, ne reflète pas l'intention

---

## Recommandation

- [x] **GO** — Lancer en Q2. Prochaines étapes :
  1. Valider budget T2 avec direction
  2. Aligner Squad Conversion sur les notifications
  3. Lancer fake door test (5% utilisateurs)
  4. Intégrer les sessions favoris dans le système de points NSM

---

## Informations manquantes

- Baseline du taux de re-visite des pages artistes
- Confirmation de la disponibilité Squad Conversion pour les notifications
- Résultats du fake door test avant engagement développement complet
