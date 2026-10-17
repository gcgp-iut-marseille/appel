# Changelog — appel_GCGP_2627.html
Application de gestion des appels BUT1 GCGP · IUT Marseille · 2026-2027

---

## [1.3.0] — 2026-10-16

### Ajouté
- **Mode visio** : case à cocher 📹 dans la barre du haut
  - En mode visio : cycle à 2 états — Connecté·e / Non connecté·e
  - Badges dédiés : 📶 (connecté) / ✗ (non connecté)
  - Légende adaptée automatiquement (masquage de la légende présentiel)
  - Compteur mis à jour : « X connecté·e·s / N »
  - Le bouton « ✓ Tous présents » se masque en mode visio
  - Statuts remis à zéro à chaque bascule de mode
  - Payload envoyé au Google Sheet enrichi d'un champ `mode: "visio" | "presentiel"`
  - Les exports Excel et mails de secours utilisent les bons libellés selon le mode

### Corrigé
- Libellés de statut incorrects dans les exports (Excel, mail, Google Sheet) en mode visio :
  `LABELS[statut]` remplacé par `getLabelsActuels()[statut]` dans `envoyerAppel`,
  `envoyerMail`, `sauvegarderBDD` et `exportXLSX`

---

## [1.2.0] — 2026-10-16

### Ajouté
- **Badge 1/3 temps** sur DREMAZA-MATTEI Loric et LEFRERE Lily-Violet
  (s'ajoute à DEROUBAIX Elliot et VESY Céline, déjà balisés)

### Corrigé
- **Photos du trombinoscope** : 44 photos correctement injectées en base64
  depuis `2627-Trombinoscope-BUT1-GCGP.pdf` (extraction PyMuPDF)
- **Attribution erronée des photos** : les associations basées sur l'ordre
  de tri créaient un décalage dès qu'une photo manquait dans la grille.
  Remplacement par une association spatiale directe (proximité image ↔ numéro
  étudiant avec tolérance ±35 px) — 44 photos correctement attribuées,
  8 étudiants confirmés sans photo dans le trombi :
  AZZOUG, DEROUBAIX, EL AISSATI, FERRER--MAZELIER,
  MOSCATI, NAIR, SCHNEIDER, VESY

---

## [1.1.0] — 2026-10 *(session précédente)*

### Ajouté
- **Badges spéciaux** :
  - `tiers_temps` (badge « 1/3 temps ») : DEROUBAIX, VESY
  - `sport_hn` (badge « 🏅 SHN ») : MORO
  - `redoublante` (badge « Redoubl. » avec modale matières S1) : FALANGA
- Grille complète de 58 étudiants BUT1 GCGP 2026-2027

---

## [1.0.0] — 2026-09 *(session d'origine)*

### Créé
- Application HTML autonome (fichier unique, zéro dépendance serveur)
- Authentification légère par code enseignant (format `XX-2627-xxxx`)
- Grille d'appel avec cycle de 5 statuts : Présent → Absent → Retard <15 →
  Retard >15 → Exclu (bascule au clic)
- Filtres TD (A/B) et TP (1/2/3/4)
- Envoi vers Google Sheets via Apps Script (POST JSON)
- Mail de secours avec liste lisible + JSON réimportable
- Sauvegarde locale en `localStorage` (onglet Historique)
- Export Excel (SheetJS)
- Mode correction pour modifier un appel déjà enregistré
- Sélection de la matière par semestre (S1/S2 auto-détecté selon le mois)
- Créneaux horaires prédéfinis (8h30 → 17h30)
- Modale d'accueil / mode d'emploi (masquable)
