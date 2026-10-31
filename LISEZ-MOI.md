# Le Jardin des Mariés — Joseph Marcel & Chantal · 26.12.2026

Invitation de mariage interactive sur une seule feuille vert sauge poudré (#B8CBB5) : un jardin ivoire et doré qui s’épanouit au fil du défilement, la silhouette des mariés dessinée à l’encre dorée qui danse un slow en arrière-plan, des fleurs naturelles colorées (roses poudrées, pêche, mauves et jaunes, lavande, myosotis), sur la musique *Halo* (reprise de Caleb Chan & Brian Chan).

## Structure du projet

```
jardin-des-maries/
├── index.html                      ← toute l’invitation (HTML, CSS, JS et dessins SVG)
├── vercel.json                     ← en-tête « noindex » (invitation privée)
├── LISEZ-MOI.md
└── assets/
    ├── audio/musique-mariage.mp3   ← votre fichier, copié à l’identique (MP3 192 kbit/s, 2 min 54)
    └── img/
        ├── couple-*.webp           ← silhouette dorée découpée en 7 calques animés (≈ 500 Ko au total)
        └── apercu-whatsapp.jpg     ← image d’aperçu du lien dans WhatsApp (1200 × 630)
```

Aucune bibliothèque JavaScript, aucune base de données. Les polices viennent de Google Fonts (Great Vibes, Cormorant Garamond, Outfit).

---

## 1. Paramètres

Le numéro WhatsApp de confirmation est déjà renseigné : `RSVP_WHATSAPP_NUMBER = '2250767693626'` (+225 07 67 69 36 26), dans le script de `index.html`. Pour le changer : format international, chiffres uniquement, sans « + » ni espaces.

Reste à compléter :

| Paramètre | Où | Quoi mettre |
|---|---|---|
| Adresse du site | `index.html`, balises `og:image` et `og:url` (lignes 16 à 19) | Préréglée sur `https://chantal-et-joseph-marcel.vercel.app`. Nommez le projet Vercel **chantal-et-joseph-marcel** pour obtenir exactement cette adresse ; sinon, remplacez-la par l’adresse obtenue. C’est ce qui affiche la belle image quand on colle le lien dans WhatsApp. |

Réglages facultatifs (objet `MUSIC`, en haut du script) :

- `volume: 0.55` — volume par défaut (0 à 1).
- `fadeInMs: 2600` — durée du fondu d’entrée.
- `loopStart: 0.55` et `loopEnd: 170.4` — le fichier commence par 0,6 s et finit par environ 3 s de silence ; la boucle saute ces silences. Si vous changez de musique, `loopEnd` se désactive tout seul quand le nouveau fichier est plus court.

---

## 2. Tester en local

Les navigateurs limitent certaines fonctions quand on ouvre le fichier par double-clic : servez plutôt le dossier.

```bash
cd jardin-des-maries
python3 -m http.server 8000
```

Puis ouvrez <http://localhost:8000>.

**Sur votre téléphone** (même réseau Wi-Fi que l’ordinateur) : ouvrez `http://<adresse-IP-de-l’ordinateur>:8000`. Pour trouver l’adresse IP : `ipconfig` sous Windows, `ipconfig getifaddr en0` sous macOS.

À vérifier sur un vrai iPhone et un vrai Android avant l’envoi aux invités :

1. Le bouton « Touchez pour ouvrir votre invitation » lance la musique ; les noms Joseph Marcel & Chantal apparaissent ensemble, puis « Scrollez vers le haut pour lire votre invitation ».
2. Il n’y a volontairement aucun bouton pour couper la musique : tous les invités l’entendent (le volume et le mode silencieux du téléphone restent sous leur contrôle).
3. Verrouillez l’écran ou changez d’application : la musique se met en pause, puis reprend au retour si elle était active.
4. La rose éclot, les noms s’écrivent, les lianes poussent ; en remontant, tout se replie.
5. Les deux boutons « Voir l’itinéraire » ouvrent Google Maps.
6. Le formulaire ouvre WhatsApp vers le +225 07 67 69 36 26 avec le message prérempli ; l’invité appuie sur Envoyer.
7. La silhouette dorée apparaît derrière les noms puis danse un slow : le couple se balance lentement, en continu, et danse seul au jardin final sans qu’on ait besoin de faire défiler.

---

## 3. Héberger sur HTTPS (Vercel)

Vercel fournit le HTTPS automatiquement. Il suffit d’envoyer **tout le dossier**, pour que l’audio et l’image soient servis avec la page.

### Option A — en ligne de commande (le plus rapide)

```bash
cd jardin-des-maries
npx vercel          # première fois : connexion, puis questions (accepter les valeurs proposées)
npx vercel --prod   # mise en ligne définitive
```

Vercel affiche l’adresse finale, du type `https://jardin-des-maries-xxxx.vercel.app`. Vous pouvez la renommer dans le tableau de bord Vercel (Settings → Domains), par exemple `jardin-chantal-marcel.vercel.app`.

### Option B — via GitHub

1. Créez un dépôt (privé si vous le souhaitez) et poussez le dossier.
2. Sur vercel.com : **Add New → Project → Import** du dépôt. Framework : *Other*. Pas de commande de build, dossier de sortie : la racine.
3. Chaque `git push` redéploie l’invitation.

### Après le premier déploiement

1. Si l’adresse obtenue n’est pas `chantal-et-joseph-marcel.vercel.app`, remplacez-la dans les balises `og:image` et `og:url`.
2. Redéployez (`npx vercel --prod` ou `git push`).
3. Vérifiez l’aperçu du lien **avant** de l’envoyer aux 250 invités : WhatsApp garde en mémoire le premier aperçu qu’il voit pour une adresse.

Autres hébergeurs possibles : Netlify (glisser-déposer du dossier sur app.netlify.com/drop) ou GitHub Pages. Tout hébergeur statique en HTTPS convient.

---

## 4. Bon à savoir

- **iPhone et volume** : Safari sur iPhone ne laisse pas une page web régler le volume. La musique y démarre donc au volume de l’appareil, sans fondu. Sur Android et sur ordinateur, le fondu de 2,6 s et le volume doux fonctionnent.
- **Lecture automatique** : aucun navigateur mobile n’autorise une musique à démarrer sans geste de l’invité. C’est pourquoi l’invitation s’ouvre par un toucher, qui lance la musique pour tout le monde. Si le téléphone bloque la reprise après un passage sur Google Maps ou WhatsApp, une invite « Touchez pour reprendre la musique » apparaît et le prochain toucher la relance.
- **Mouvement réduit** : si l’invité a activé « Réduire les animations », le jardin s’affiche directement en fleurs et la silhouette reste immobile, sans scène épinglée.
- **La danse** : la silhouette est une marionnette en 7 calques (marié, bras levés, mariée, robe, voile, traîne, volutes) qui pivotent autour de leurs articulations selon le défilement, avec des lignes dorées et des particules. Elle se balance en continu comme un slow ; la robe, la traîne et le voile suivent avec un léger retard. Ce n’est pas une chorégraphie image par image.
- **Confidentialité** : la page demande aux moteurs de recherche de ne pas l’indexer (`noindex`). Seules les personnes qui ont le lien la trouvent.
- **Audio en Base64 dans un seul fichier HTML** : c’est possible mais déconseillé ici. Les 3,4 Mo de musique deviendraient environ 4,5 Mo de texte dans la page, téléchargés avant le premier affichage, y compris pour les invités qui ne lancent pas la musique. La solution HTML + fichier audio ne charge la musique qu’au moment du toucher.
