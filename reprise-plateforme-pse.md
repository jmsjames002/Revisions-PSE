# Fichier de reprise : plateforme de révision PSE

Mise à jour : mercredi 11 novembre 2026 (soir).

## 1. Comment reprendre

Ouvre une nouvelle conversation et joins :

1. `reprise-plateforme-pse.md` (ce fichier)
2. `revisions-pse.html` (la plateforme complète, version du 11 novembre 2026)
3. `sources-pse.zip` (script de construction, moteur et un fichier par module)
4. Les PDF des Références techniques PSE et des logigrammes (seulement si du contenu doit être revu)

Puis colle ce message :

> Je reprends la plateforme de révision PSE. Lis d'abord le fichier de reprise en entier. Attaque le « Dossier GitHub final » décrit en section 6.

La plateforme est publiée ici : https://claude.ai/artifact/77GPdtZ7WQ8cTJgFcXhYvq

## 2. Objectif du projet

James, secouriste PSE2, veut une plateforme ludique pour réviser l'ensemble des références techniques PSE. Il la diffusera à ses collègues pour des tests, puis l'hébergera sur GitHub Pages. Une fois en ligne :

- un lien, chacun joue seul ;
- progression dans le navigateur de chaque utilisateur ;
- aucun compte, aucun serveur, aucune maintenance.

Préférences de James : tutoiement, réponses directes et concises, en français.

## 3. Décisions validées

### Contenu et sources

- **Les fiches priment** sur les logigrammes. Chaque contenu cite sa fiche ou son logigramme.
- **Niveaux.** Fiche marquée PSE① : `lvl:"PSE1"`. Fiche marquée PSE② : `"PSE2"`. Fiche sans marque : `"OPT"`, étiquetée « Optionnel » et visible seulement en profil PSE2. Le profil PSE2 démarre au palier 2. Un thème sans contenu pour le profil PSE1 est masqué pour ce profil.
- **Paliers 1 à 3.** Un palier se débloque après 5 bonnes réponses au palier en cours (ou moins si le thème contient moins de 5 exercices à ce palier pour le profil), avec au moins 80 % de réussite.
- **Rôles des cas concrets** : `isole`, `equipier`, `chef`. Les cas `chef` sont réservés au profil PSE2 (lvl PSE2 ou OPT).
- **Écarts entre logigrammes et fiches.** On suit les fiches.
  - Insufflations avec pouls : LOGI 05 indique 10/20/30/40 ; la fiche 05PR04 indique adulte et enfant 10, nourrisson 20, nouveau-né 30. La fiche 08PR05 prévoit, chez le nouveau-né à la naissance, 40 insufflations en 1 minute (à faire trancher par les collègues).
  - Naloxone : LOGI 13 indique FR < 6 et réinjection à 3 min ; la fiche 08PR09 indique FR < 12 et/ou perte de connaissance, à partir de 14 ans, réinjection à 2-3 min.
  - Surveillance : LOGI 14 indique 5 ou 10 min ; la fiche 04PR05 indique 5 ou 10 à 15 min.
  - 4e regard : ordre différent entre LOGI 00 et 04PR04, donc pas d'exercice d'ordre.
  - Brûlures : LOGI 10 écrit « brûlure > 30 minutes » ; la fiche 07PR01 dit moins de 30 minutes, avec une surface inférieure à 20 % (adulte) ou 10 % (enfant).
- **FARAT, FARAST, AVPC** ne figurent pas dans les références. Ne pas les inventer.

### Gamification

- **Gains d'XP** : inchangés (voir le pilote). Total disponible en première réussite : environ 9 400 XP en PSE1 et 15 500 XP en PSE2, calculé automatiquement à partir du contenu (`xpTotal()`).
- **Niveaux** : 25 niveaux, courbe calibrée sur le total du profil. Le niveau 25 (rang Master) correspond à 80 % du total. Seuil du niveau n : 0,8 × total × ((n − 1) / 24)^1,6. Rangs : Recrue (1), Équipier en formation (4), Équipier (8), Équipier aguerri (12), Référent (16), Expert (20), Master (25). Changer de profil recalcule le niveau affiché ; l'XP est conservée.
- **Badges** : 10 familles × 5 niveaux (`FAMILIES`), inchangés. « Terrain Master » (15 cas) est atteignable en PSE1 (31 cas).

### Images et vidéos

- Images de James : usage interne, erreurs mineures acceptées, affichées avec la correction sous la mention « Illustration indicative : en cas d'écart, la fiche fait foi ». Introductions de cas : image du binôme (cas en équipe) ou de la scène (nombreuses victimes). Si la plateforme devient publique, demander les autorisations.
- Toutes les images du zip sont utilisées.
- Vidéos : plusieurs par élément si complémentaires ; en doublon, la plus récente, sauf l'hémorragie (version PSE de la Protection Civile) ; sinon lien de recherche YouTube. Les vidéos Protection Civile datent des recommandations de décembre 2022 : la plateforme le signale.
- Brûlures : vidéos Protection Civile et format court de la Croix-Rouge gardés ; Doctissimo écarté. Les dates n'ont pas été vérifiées.

### Navigation

Le bouton retour du téléphone fonctionne comme le bouton « Retour » du site : activité, puis thème, puis accueil, puis choix du profil PSE1 ou PSE2. Chaque écran est une entrée de l'historique du navigateur (`go()`, `navStack`, `popstate`). Les activités (quiz, séquence, cas, cartes, logigramme, jeux du bilan, résultat) occupent un seul niveau et se remplacent. Revenir vers un écran déjà ouvert recule dans l'historique au lieu d'empiler. Test : `nav.py`.

### Apparence et téléphone

Palette claire, une couleur par thème, Auto / Clair / Sombre. Rappel Google Agenda et .ics (actif seulement hors Claude). Guide d'installation sur l'écran d'accueil. Pas de notifications, pas de bouton « Signaler une erreur ». Indexation bloquée (meta `noindex, nofollow`).

## 4. Ce qui est fait

Tous les chapitres 01 à 12 sont couverts. L'accueil regroupe les thèmes par module dépliable, avec un « Quiz du module ».

| Module (chapitres) | Thèmes |
|---|---|
| Attitude, protection et hygiène (01-03) | Attitude et abord relationnel ; Protection et sécurité ; Hygiène et asepsie |
| Le bilan (04) | Le bilan ; Techniques du bilan |
| Urgences vitales (05) | Hémorragies ; Obstruction ; Arrêt cardiaque et ventilation ; Perte de connaissance ; Détresses et oxygène |
| Malaises (06) | Malaise et aide aux médicaments ; Douleur thoracique et AVC ; Convulsions, asthme, hypoglycémie, allergie (optionnel) |
| Traumatismes (07) | Brûlures ; Plaies et amputations ; Membres ; Abdomen, thorax et face ; Rachis, crâne et bassin |
| Atteintes circonstancielles (08) | Noyade ; Chaleur et hypothermie ; Accouchement ; Électricité, intoxications, pendaison, morsures ; Plongée, gelures, montagne (optionnel) |
| Souffrance psychique (09) | Personnes en situation de crise |
| Relevage et brancardage (10) | Relevage et brancardage |
| Situations particulières (11-12) | Nombreuses victimes et alerte |

Total : 26 thèmes, 517 questions, 53 séquences, 62 cas concrets (20 « chef », 31 jouables en PSE1), 137 flashcards, logigrammes LOGI 00 à 14.

Tests Playwright : contrôle de cohérence (identifiants uniques, une seule bonne réponse par étape, clés d'images et de vidéos valides, chaque thème rattaché à un module), parcours complet de chaque thème en profil PSE1 et PSE2.

## 5. Architecture

### Fichier publié

Un seul HTML autonome (environ 4 Mo, images et logigrammes en base64).

### Sources (`sources-pse.zip`)

- `build.py` : part du HTML pilote d'origine (à placer dans `base/revisions-pse.html`), applique les modifications du moteur, intègre les images (`images-pse/`, à décompresser depuis `images-pse.zip`), les logigrammes (`logi/`) et les modules (`mods/`). Produit `revisions-pse.html`.
- `eng/` : `images_map.js` (images, `LINK_IMG`, `INTRO_IMG`), `register.js` (`MODULES`, `registerModule`), `colors_and_home.js` (couleurs des thèmes).
- `mods/m1b.js` à `m8.js` : un fichier par module, au format `registerModule({themes, q, orders, scen, cards, videos, linkVid, search, img, intro, logi})`.
- `test.py` : tests Playwright (bloquer Google Fonts). `nav.py` : test du bouton retour.

Si les sources sont perdues, tout le contenu reste lisible dans le HTML publié (blocs `registerModule`).

### Règles

- **Ne jamais changer les identifiants existants**, sinon les progressions se perdent. Préfixes utilisés : h, o, a, p, c, bq, b, be (pilote) ; dt, at, pr, hy, ms, ml, mc, mo, br, pl, mb, tr, ra, ny, th, ac…x, ix, co, ps, rl, nv. Séquences en `o…`, cas en `s…`, cartes en `f…`.
- Les paliers par défaut se créent automatiquement pour tout nouveau thème (`defaultState`).
- Sauvegarde : localStorage (`pse-revisions-v1`), plus la base de données de Claude quand la page tourne sur Claude.

## 6. Reste à faire

### Relecture par les collègues

Points à vérifier en priorité :

1. Insufflations du nouveau-né (section 3).
2. Cas « Deux détresses, un binôme » : cumul détresse respiratoire et circulatoire chez un insuffisant respiratoire chronique, non traité explicitement par les fiches.
3. Les cas « chef d'équipe » : les références décrivent peu ce rôle, la répartition des tâches est une interprétation à valider selon les pratiques de l'antenne.
4. Dates des vidéos sur les brûlures.

### Dossier GitHub final

- contenu séparé du code : un fichier JS par module, chargé par `index.html` ;
- images en fichiers séparés plutôt qu'en base64 ;
- application installable : manifeste, service worker (hors ligne), icônes ;
- `APP_URL` pointant vers l'adresse GitHub ; .ics actif ;
- retirer ou neutraliser le code propre à Claude (`window.claude`) ;
- garder `noindex` et ajouter un `robots.txt` ;
- pas-à-pas de mise en ligne sur GitHub Pages ;
- vérifier avec James la réutilisation publique des logigrammes du ministère et des images.
