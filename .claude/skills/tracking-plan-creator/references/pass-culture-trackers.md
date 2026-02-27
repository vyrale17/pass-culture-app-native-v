# Pass Culture — Tracking Documentation

> Référence authoritative de tous les événements analytics. Consulter ce fichier EN PREMIER avant de créer de nouveaux événements.

---

## Architecture multi-provider

| Provider | Nombre d'événements | Usage |
|----------|--------------------|----|
| Firebase Analytics | 204 | Tracking principal — toutes les interactions |
| AppsFlyer | 4 | Attribution campagnes et conversions |
| Batch | 16 | Segmentation push notifications |
| Algolia Analytics | Variable | Interactions et conversions de recherche |

**Architecture :** TrackingManager centralisé avec buffering pour garantir la livraison malgré les problèmes réseau. Couverture équivalente iOS, Android et web via des adapteurs spécifiques à chaque provider.

---

## Firebase Analytics — 204 événements

### Authentification & Comptes (18 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `SignUp` | `method` | Inscription nouvel utilisateur |
| `Login` | `method` | Connexion utilisateur |
| `Logout` | — | Déconnexion |
| `CancelSignup` | `nextContainerId` | Abandon du parcours d'inscription |
| `HasActivateGeolocFromTutorial` | — | Activation géolocalisation depuis tutoriel |
| `DeleteProfile` | — | Suppression de compte |
| `ReactivateAccount` | — | Réactivation de compte |
| `ChangeEmailRequest` | — | Demande de changement d'email |
| `ChangePassword` | — | Changement de mot de passe |
| `ForgotPasswordClicked` | — | Clic sur "Mot de passe oublié" |
| `IdentityCheckAbort` | `step` | Abandon vérification d'identité |
| `VerifyEligibility` | — | Vérification éligibilité |
| `YoungUserEngaged` | — | Premier engagement jeune utilisateur |
| `OnboardingStarted` | — | Démarrage onboarding |
| `TutorialPageDisplayed` | `page` | Page tutoriel affichée |
| `AccountCreated` | — | Compte créé avec succès |
| `EmailValidated` | — | Email validé |
| `PhoneValidated` | — | Téléphone validé |

### Réservations (15 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `BookingConfirmation` | `offerId`, `bookingId` | Confirmation de réservation |
| `BookingError` | `offerId`, `errorCode` | Erreur lors de la réservation |
| `CancelBooking` | `offerId`, `bookingId` | Annulation de réservation |
| `CancelBookingFunnel` | `step` | Étape du funnel d'annulation |
| `BookOfferConfirmDates` | `offerId` | Confirmation des dates |
| `SelectAge` | `age` | Sélection de l'âge |
| `BookingDetailsClicked` | `bookingId` | Clic sur détails réservation |
| `SeeMyBooking` | `offerId` | Consultation de ma réservation |
| `UserSetLocation` | `locationType` | Localisation définie par l'utilisateur |
| `ExternalBookingStep` | `step`, `offerId` | Étape réservation externe |
| `SeeDuoOffer` | `offerId` | Consultation offre duo |
| `SelectCinemaSeance` | `offerId` | Sélection séance cinéma |
| `ChangeDuoSelection` | `offerId` | Modification sélection duo |
| `DuoConfirm` | `offerId` | Confirmation choix duo |
| `BookingImpossibleIOS` | `offerId` | Réservation impossible sur iOS |

### Consultation d'offres (23 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `ConsultOffer` | `offerId`, `from`, `moduleId` | Consultation d'une fiche offre |
| `ConsultWholeOffer` | `offerId` | Consultation complète de l'offre |
| `HasAddedOfferToFavorites` | `offerId`, `from` | Ajout aux favoris |
| `HasRemovedOfferFromFavorites` | `offerId` | Suppression des favoris |
| `ConsultDescriptionDetails` | `offerId` | Consultation description détaillée |
| `ClickBookOffer` | `offerId`, `from` | Clic sur "Réserver" |
| `Share` | `offerId`, `type` | Partage d'une offre |
| `ConsultArtist` | `artistId`, `from` | Consultation page artiste |
| `ClickSocialNetwork` | `network`, `artistId` | Clic réseau social artiste |
| `ConsultVideo` | `offerId`, `videoId` | Consultation vidéo |
| `HasSeenAllVideo` | `offerId`, `videoId` | Vidéo visionnée en entier |
| `ClickVenueMap` | `venueId` | Clic carte du lieu |
| `ConsultAccessibilityModalities` | `offerId` | Consultation accessibilité |
| `ConsultItinerary` | `venueId` | Consultation itinéraire |
| `OpenExternalUrl` | `url` | Ouverture URL externe |
| `ScreenShot` | `screen` | Capture d'écran |
| `ConsultChronicle` | `offerId`, `from` | Consultation d'une chronique |
| `ClickReactionLike` | `offerId` | Réaction "j'aime" |
| `ClickReactionDislike` | `offerId` | Réaction "je n'aime pas" |
| `ViewedOffer` | `offerId`, `moduleId` | Offre vue (impression) |
| `TileDisplayed` | `offerId`, `moduleId` | Tuile affichée |
| `OfferSeen` | `offerId` | Offre aperçue |
| `HasSeenOffer` | `offerId` | A vu l'offre |

### Recherche (11 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `PerformSearch` | `searchId`, `query` | Exécution d'une recherche |
| `SearchScrollToPage` | `searchId`, `page` | Pagination des résultats |
| `NoSearchResult` | `searchId`, `query` | Aucun résultat |
| `SearchFilter` | `searchId`, `filterType` | Application d'un filtre |
| `SearchFilterPage` | `searchId` | Page des filtres affichée |
| `ResetSearchFilter` | `searchId` | Réinitialisation des filtres |
| `SaveNewSearch` | `searchId` | Sauvegarde de recherche |
| `SearchLocationUpdate` | `locationType` | Mise à jour localisation recherche |
| `ConsultSearchSuggestion` | `searchId` | Consultation suggestion |
| `ClickSearchSuggestion` | `searchId`, `suggestionType` | Clic sur suggestion |
| `ConsultSearchHistory` | — | Consultation historique de recherche |

### Home & Modules (15 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `ModuleDisplayed` | `moduleId`, `moduleName`, `moduleType` | Module home affiché |
| `AllTilesDisplayed` | `moduleId` | Toutes les tuiles vues |
| `ExclusivityBlockClicked` | `moduleId` | Clic bloc exclusivité |
| `RecommendationModuleSeen` | `moduleId` | Module recommandation vu |
| `StepperDisplayed` | `moduleId` | Stepper affiché |
| `StepperClicked` | `moduleId`, `step` | Clic sur stepper |
| `CategoryBlockClicked` | `moduleId`, `categoryName` | Clic bloc catégorie |
| `HighlightBlockClicked` | `moduleId` | Clic bloc highlight |
| `ConsultHome` | `entryPoint` | Consultation page home |
| `HomeModuleDisplayed` | `moduleId` | Module home affiché |
| `BusinessBlockClicked` | `moduleId` | Clic bloc business |
| `SimilarOfferPlaylist` | `offerId`, `moduleId` | Playlist offres similaires |
| `VenueMapBlockClicked` | `moduleId` | Clic bloc carte venues |
| `TrendingOffersModule` | `moduleId` | Module tendances |
| `GeolocationUpdate` | `locationType` | Mise à jour géolocalisation |

### Venues (10 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `ConsultVenue` | `venueId`, `from` | Consultation page venue |
| `VenueContact` | `venueId`, `type` | Contact avec un lieu |
| `SeeVenueOffers` | `venueId` | Voir les offres du lieu |
| `ClickVenueMap` | `venueId` | Clic sur carte du lieu |
| `ConsultLocationFilter` | — | Consultation filtre localisation |
| `VenueMapSeenOffer` | `venueId`, `offerId` | Offre vue sur carte venue |
| `PinMapPressed` | `venueId` | Pin carte pressé |
| `SeeMoreVenueOffers` | `venueId` | Voir plus d'offres venue |
| `ConsultVenueMap` | — | Consultation carte des venues |
| `VenueMapClicked` | `venueId` | Carte venue cliquée |

### Vérification d'identité (7 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `IdentityCheckStep` | `step` | Étape de vérification |
| `IdentityCheckAbort` | `step` | Abandon vérification |
| `IdentityCheckSuccess` | — | Vérification réussie |
| `SelectIdOrigin` | `type` | Sélection origine pièce d'identité |
| `SelectIdRecto` | — | Recto sélectionné |
| `SelectIdVerso` | — | Verso sélectionné |
| `ContactFraudTeam` | — | Contact équipe fraude |

### Accessibilité & Paramètres (12 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `UpdateAppTheme` | `theme_setting`, `system_theme` | Mise à jour du thème |
| `NotificationToggle` | `type`, `enabled` | Toggle notification |
| `LocationToggle` | `enabled` | Toggle localisation |
| `AccessibilityActionViewed` | `action` | Action accessibilité vue |
| `UseFilter` | `filterType` | Utilisation d'un filtre |
| `ConsultSettingsMenu` | — | Consultation menu paramètres |
| `ConsultNotificationSettings` | — | Consultation paramètres notifications |
| `ConsultPrivacySettings` | — | Consultation paramètres vie privée |
| `ConsultCookiesSettings` | — | Consultation paramètres cookies |
| `ConsultLocationSettings` | — | Consultation paramètres localisation |
| `OpenMapSettings` | `platform` | Ouverture paramètres carte |
| `ConsultAccessibilitySettings` | — | Consultation paramètres accessibilité |

### Vie privée & Cookies (5 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `HasAcceptedAllCookies` | — | Acceptation tous les cookies |
| `HasDeclinedAllCookies` | — | Refus tous les cookies |
| `HasCustomizedCookies` | — | Cookies personnalisés |
| `AcceptCookiesV2` | — | Acceptation cookies v2 |
| `CookiesConsent` | `type` | Consentement cookies |

### Social & Partage (8 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `Share` | `offerId`, `type` | Partage d'une offre |
| `ClickSocialNetwork` | `network`, `artistId` | Clic réseau social |
| `ShareApp` | — | Partage de l'application |
| `ScreenShot` | `screen` | Capture d'écran |
| `ConsultWhatsNew` | — | Consultation nouveautés |
| `ClickCopyMail` | — | Copie email |
| `RateInStoreClicked` | — | Clic noter dans le store |
| `LongPress` | `type` | Appui long |

### Onboarding (6 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `OnboardingStarted` | — | Démarrage onboarding |
| `TutorialPageDisplayed` | `page` | Page tutoriel affichée |
| `HasActivateGeolocFromTutorial` | — | Géoloc activée depuis tutoriel |
| `AppOpened` | — | Application ouverte |
| `ConsultWhatsNew` | — | Consultation nouveautés |
| `SkipTutorial` | — | Tutoriel passé |

### Enquête culturelle (4 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `CulturalSurveyStarted` | — | Enquête culturelle démarrée |
| `CulturalSurveyScrolledToBottom` | — | Défilement jusqu'en bas |
| `CulturalSurveyAnswersValidated` | — | Réponses validées |
| `CulturalSurveyFinished` | — | Enquête terminée |

### Achievements (3 événements)

| Événement | Paramètres principaux | Description |
|-----------|----------------------|-------------|
| `AchievementUnlocked` | `achievementName`, `state` | Achievement débloqué |
| `ConsultAchievementModal` | `achievementName` | Consultation modale achievement |
| `AchievementsDisplayed` | — | Achievements affichés |

---

## AppsFlyer (4 événements)

| Événement | Description |
|-----------|-------------|
| `af_complete_registration` | Inscription complète |
| `af_first_booking` | Première réservation |
| `af_n_booking` | N-ième réservation |
| `af_activate_account` | Activation de compte |

---

## Batch (16 événements)

Événements de segmentation pour le ciblage des notifications push, couvrant :
- Engagement avec les offres culturelles
- Comportements de recherche
- Statut de réservation
- Préférences de catégorie

---

## Algolia Analytics

Tracking des interactions de recherche :
- Clics sur résultats
- Conversions (réservations depuis résultats de recherche)
- Requêtes sans résultat
