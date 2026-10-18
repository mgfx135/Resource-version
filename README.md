# Resource-version

Dernieres versions publiees des ressources OPW, lues par **opw_bridge** (hub `/opw`,
console `opw diag` / `opw updates`) pour signaler les mises a jour disponibles.

Fichier lu : `versions.json`
URL : `https://raw.githubusercontent.com/mgfx135/Resource-version/main/versions.json`

## Publier une mise a jour

1. Augmenter `version '1.x.y'` dans le `fxmanifest.lua` de la ressource.
2. Mettre la meme version dans `versions.json` (champ `changelog` facultatif, 500 caracteres,
   champ `url` facultatif : lien de telechargement).
3. Detailler les changements dans `CHANGELOG.md` (notes de version).
4. Pousser ce depot. Les serveurs verifient au demarrage puis toutes les 6 h (reglable dans le hub).

Un serveur dont la version installee est plus ancienne voit l'avertissement en console et
la mise a jour dans le hub (page Ressources OPW).
