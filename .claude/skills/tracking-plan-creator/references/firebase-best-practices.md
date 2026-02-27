# Firebase Analytics Naming Conventions — Pass Culture

> Ces conventions sont spécifiques à Pass Culture et diffèrent des conventions Firebase par défaut.

## Principes clés

**Events → PascalCase** : Première lettre majuscule, puis camelCase.
```
✅ ClickBookOffer
✅ ConsultOffer
✅ UpdateAppTheme
❌ click_book_offer
❌ clickBookOffer
```

**Parameters → camelCase** : Première lettre minuscule.
```
✅ offerId
✅ categoryName
✅ venueId
❌ OfferID
❌ offer_id (sauf exceptions listées ci-dessous)
```

## Exceptions snake_case (paramètres uniquement)
- `call_id`
- `theme_setting`
- `system_theme`

---

## Structure des événements

### Patterns de nommage

| Type | Pattern | Exemples |
|------|---------|---------|
| Click | `Click{Object}` ou `Click{Action}{Object}` | `ClickBookOffer`, `ClickSocialNetwork` |
| Consultation | `Consult{Object}` | `ConsultOffer`, `ConsultVenue` |
| Statut/état | `Has{Action}{Object}` ou `{Object}Status` | `HasAddedOffer`, `BookingStatus` |
| Affichage | `{Object}Displayed` | `ModuleDisplayed` |
| Recherche | `PerformSearch`, `Search{Action}` | `SearchScrollToPage` |

**Contraintes :**
- Longueur maximale : 40 caractères
- Éviter les préfixes réservés Firebase (`firebase_`, `google_`, `ga_`)

---

## Paramètres standards

### Identifiants
| Pattern | Exemples |
|---------|---------|
| `{entity}Id` | `offerId`, `venueId`, `moduleId`, `searchId` |
| `{entity}Name` | `categoryName`, `moduleName` |
| `is{State}` (boolean) | `isHeadline`, `isFree` |

### Paramètre `from` (spécial)
Le paramètre `from` indique la source de navigation. Utilisations :
- Standalone : `from = "home"`, `from = "search"`, `from = "artistPage"`
- Composé : `fromMultivenueOfferId` (origine avec contexte)

---

## Authentification — Conventions spéciales

| Contexte | Convention | Exemple |
|----------|-----------|---------|
| Méthode de login | camelCase avec préfixe | `fromLoginApple`, `fromSignupGoogle` |
| Type de compte | snake_case | `SSO_login`, `email_signup` |

---

## Erreurs fréquentes à éviter

1. **Mélanger les systèmes de casse** : `ClickOffer_Id` ❌
2. **Omettre le paramètre `from`** quand il y a un contexte de navigation ❌
3. **Utiliser snake_case** pour de nouveaux paramètres qui devraient suivre camelCase ❌
4. **Dépasser 40 caractères** pour les noms d'événements ❌

---

## Arbre de décision — Nommer un nouvel événement

```
1. L'événement existe-t-il déjà dans pass-culture-trackers.md ?
   → OUI : Réutiliser l'événement existant
   → NON : Continuer

2. Quel est le type d'interaction ?
   → Clic → Click{Object}
   → Consultation/Affichage → Consult{Object}
   → État/Statut → {Object}Status ou Has{Action}{Object}

3. Vérifier : longueur ≤ 40 caractères ?
   → OUI : Valider
   → NON : Raccourcir l'objet

4. Vérifier : respecte PascalCase ?
   → OUI : Approuver
   → NON : Corriger
```
