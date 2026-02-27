# Jira Tracking Plan Format Guide

> Format standard pour créer des tickets de tracking plan Firebase Analytics dans Jira.

---

## Structure du ticket

### Titre
```
[Analytics] {Nom de la fonctionnalité} - {Description courte}
```
Exemple : `[Analytics] Pages Artistes Enrichies - Tracking multi-artistes`

---

### 📋 Contexte

Expliquer :
- La situation actuelle et ses limites analytiques
- Les questions business auxquelles on ne peut pas répondre aujourd'hui
- Pourquoi ce tracking est nécessaire maintenant

---

### 🎯 Objectif

```
Objectif : {Énoncé clair de ce que le tracking permettra d'analyser}
```

---

### 👤 User Story

```
En tant que [rôle — ex: PM, Data Analyst]
J'aimerais [action — ex: mesurer le taux de clic sur les chroniques]
Afin de [bénéfice — ex: évaluer l'impact des chroniques sur la consultation d'offres]
```

---

### ⚙️ Règles de gestion

Pour chaque événement, documenter :

```
**EventName** (nouveau / modifié)
- Déclencheur : [quand exactement l'event se fire]
- Paramètres :
  - `paramName` : [valeur ou type] — [description]
  - `from` : [valeur] — [contexte de navigation]
- Providers : Firebase / AppsFlyer / Batch / Algolia
- Variations : [si plusieurs cas, les lister explicitement]
```

---

### ✅ Validation PM (Gherkin)

Format des scénarios :
- `nouveau` pour les ajouts
- `PAS {ancien comportement}` pour les remplacements
- Scénario de régression obligatoire si un event existant est modifié

```
- [ ] Scénario : {Nom descriptif du cas}
  - Given {contexte initial}
  - And {contexte additionnel si nécessaire}
  - When {action utilisateur}
  - Then {event se fire} avec :
    - `eventName` = "{valeur}"
    - `paramName` = "{valeur}"
  - And {autre assertion si nécessaire}

- [ ] Scénario : Régression — {Comportement existant préservé}
  - Given {contexte}
  - When {action}
  - Then {event existant} se fire PAS ModifiedEvent
```

---

### 🧪 Recette

```
Validation via Firebase DebugView :
- [ ] Activer DebugView sur l'appareil de test
- [ ] Reproduire chaque scénario
- [ ] Capturer screenshot confirmant chaque event et ses paramètres
- [ ] Vérifier l'absence de regressions sur les events existants
```

---

### 📚 Documentation du tracker

```
- [ ] Mettre à jour pass-culture-trackers.md avec les nouveaux events
- [ ] Vérifier cohérence avec firebase-existing-properties.md
```

---

### ✔️ Validation Data

```
- [ ] Données visibles dans BigQuery (analytics_prod.native_event)
- [ ] Nommage conforme aux conventions (firebase-best-practices.md)
- [ ] Ticket Analytics Engineering créé si nécessaire : [lien]
```

---

## Standards de qualité

| Critère | Exigence |
|---------|---------|
| Spécificité | Identifier précisément les gaps actuels |
| Mesurabilité | Objectifs permettant de nouvelles analyses |
| Couverture | Tous les edge cases documentés |
| Changements | Marquage explicite nouveau/modifié/supprimé |
| Régressions | Scénarios de non-régression pour chaque event existant modifié |
