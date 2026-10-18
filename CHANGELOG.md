# Notes de version des ressources OPW

Les versions publiées sont listées dans `versions.json` (lu par opw_bridge). Ce fichier détaille ce qui change d'une version à l'autre.

---

## opw_customs 1.1.0 (18/10/2026)

Version de correctifs issue d'un audit complet de la ressource. Les tables se mettent à jour toutes seules au premier démarrage (migrations versionnées dans `opw_customs_schema`).

### Changements visibles en jeu

**Atelier**
- Hors mode mécanicien, seul le **propriétaire** d'un véhicule possédé peut le customiser (*Paramètres > Propriétaire uniquement*, activé par défaut).
- Une plaque recopiée sur un autre véhicule est refusée (le modèle enregistré doit correspondre).
- Les réparations se paient au prix des dégâts **au moment de payer**.
- Payer avec le compte de son entreprise demande désormais le grade de gestion d'un menu patron ou le droit **Retrait** (sans menu patron : le plus haut grade du métier seulement).
- Carte refusée faute d'argent : le message indique « fonds insuffisants ».

**Factures du mécanicien**
- Le client peut payer **par carte** (choix de la carte et code PIN).
- Échap ou la croix ne refusent plus la facture : seul le bouton « Refuser » la refuse.
- Le mécanicien n'est plus bloqué quand son client se déconnecte pendant une facture.
- La facture au compte de l'entreprise suit la règle de dépense ci-dessus ; elle est désactivée par défaut dans les nouveaux ateliers.
- OPW Invoice : une facture payée après la fermeture de l'atelier, ou après un redémarrage, est appliquée au véhicule ; si c'est impossible, le client est remboursé. Le mode « Facturer après » est réservé au propriétaire du véhicule.

**Menu patron**
- **Recrutement par invitation** : le joueur accepte ou refuse l'offre d'embauche (45 s).
- Plafonds sur 24 h : primes (100 000 $ par défaut) et retraits du coffre (réglable, sans limite par défaut).
- Statistiques justes sur 7 / 30 / 90 jours, ventes payées par une société comprises ; un bandeau signale une période trop chargée.
- Paiements par carte comptés avec la banque.
- Codes promo : 5 caractères minimum pour un nouveau code, remise plafonnable par l'admin, l'auteur d'un code ne peut ni se le réserver ni l'utiliser.

**Menu métier (F6)**
- Fourrière sans opw_garage : les véhicules créés par un script (location, service) ne sont plus supprimés, seulement la circulation PNJ.
- Une facture OPW Invoice par minute et par client.

**Administration**
- Nouveaux réglages : Propriétaire uniquement, Remise maximale des codes promo, Primes sur 24 h, Retraits sur 24 h, Fourrière : véhicules de script.
- Masquage HUD : seules les ressources et events autorisés (`Config.HudActionResources` / `Config.HudActionEvents` dans `config/server.lua`) sont acceptés.
- Logos et images d'atelier en `https` uniquement ; une image qui ne charge pas affiche l'icône de l'atelier.
- Journal : nouvelles actions « Facture remboursée » et « Remboursement impossible ».

### Sécurité et fiabilité

- Son moteur, stance, anti-lag et chargement de dépanneuse ne peuvent plus être posés par un client modifié.
- Listes de modèles autorisés / interdits, dépanneuse et valeur du véhicule fonctionnent pour tous les modèles (hash normalisés).
- Classe du véhicule fixée par modèle (annonces contradictoires ignorées et tracées).
- Codes promo : une seule réponse pour tout code refusé, vérification limitée (6 essais / 15 s), limite par joueur atomique.
- Ventes enregistrées dans une table dédiée `opw_customs_sales`, jamais purgée et indépendante des journaux.
- Colonne `payment` élargie : les ventes payées par une société sont de nouveau journalisées.
- Purge des journaux par lots, index ajoutés pour le menu patron.
- Remboursement ligne par ligne si un élément ne peut pas être enregistré ; plus aucun remboursement sur un autre compte que celui débité.

### À faire avant de mettre à jour

1. Si vous masquez des HUD d'autres ressources que `hud`, `opw_minimap` ou `GN_Hud`, ajoutez-les dans `Config.HudActionResources` : sinon ces actions sont retirées au démarrage.
2. Remplacez les logos et images en `http://` par des adresses `https://`.
3. Vérifiez *Paramètres > Propriétaire uniquement* selon votre usage (véhicules partagés entre joueurs).

---

## opw_dealership 1.1.0 (18/10/2026)

Version de correctifs issue d'un audit complet de la ressource. Nécessite **opw_bridge 1.0.1**. La migration `003_reliability` s'applique au premier démarrage.

- Les exports `GiveVehicle` et `GeneratePlate` sont réservés aux ressources autorisées (`integrations.allowedResources`, vide par défaut).
- Marge minimale de vente (`sales.minNetPercent`, 50 %).
- Reprise d'un véhicule vendu en concession possible après 24 h, plafonnée au prix payé × coefficient.
- Les factures de vente expirent (48 h, 2 en attente au maximum).
- Les commandes arrivées et non retirées sont annulées après 7 jours.
- En mode vendeur obligatoire, un client ne peut plus commander seul.
- La suppression d'une concession est bloquée tant qu'il reste des opérations en cours.

---

## opw_bridge 1.0.1 (18/10/2026)

- Permissions : un administrateur qui n'est pas du groupe racine ne peut plus modifier ni supprimer un groupe dont les droits dépassent les siens.
- Les codes d'erreur d'une ressource ne sont plus modifiés par le module de permissions.
