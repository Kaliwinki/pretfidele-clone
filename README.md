# PrêtFidèle — copie temporaire (site séparé)

Copie statique temporaire de **https://pretfidele.com** (site du propriétaire,
même compagnie 9370-0250 Québec inc. que MonsieurPrêts), publiée sur GitHub
Pages pour test : **https://kaliwinki.github.io/pretfidele-clone/**

## Contenu

- `fr/go/` — le formulaire (Demande / Vérifications / Signatures)
- `fr/default/` — accueil
- `fr/legal/` — informations légales
- `fr/privacy/` — politique de confidentialité
- `_next/`, `brand/` — coquille Next.js et logos

## Comment ça marche

La page `/fr/go/` est une coquille Next.js dont le vrai formulaire est chargé
en direct depuis le SDK Solicorp (`creditf.ca`), comme sur l'original ; sans
ce chargement, la page reste sur « Chargement en cours ». Les infos du premier
formulaire (Heyflow, sur MonsieurPrêts) arrivent par les paramètres de
l'adresse : `leadSourceId`, `email`, `tel`, `fname`, `lname`, `amount`.

Le chemin public de webpack (`r.p="/_next/"`) est corrigé en relatif
(`../../_next/`) pour fonctionner sous le sous-chemin GitHub Pages. Les
étapes Demande, Vérifications et Signatures sont rendues par le SDK, pas par
des pages séparées.

## Différences volontaires avec l'original

- Liens internes réécrits en relatif pour GitHub Pages.
- `robots.txt` = `Disallow: /` (protection noindex : la copie ne doit pas
  concurrencer l'original sur Google).
- Pas de backend WordPress/Next : pas de `wp-json`, pas d'admin, pas de base
  de données. `.nojekyll` ajouté.

## Scripts

- `download_pretfidele.py` — dans le dépôt `monsieurprets-clone` : télécharge
  les pages et les chunks Next.js, corrige les chemins.
- `push.py` — publie tout le dossier en un seul commit via l'API GitHub.
