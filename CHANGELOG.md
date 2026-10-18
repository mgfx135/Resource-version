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

Version de correctifs issue d'un audit complet de la ressource. Nécessite **opw_bridge 1.0.1**. La migration `003_reliability` s'applique au premier démarrage (nouvelles colonnes et tables, index).

### Changements visibles en jeu

**Clients**
- Promotions, codes promo et remises ne font plus descendre un véhicule sous **50 % de son prix** (`sales.minNetPercent`) : plus de véhicule gratuit.
- Prix augmenté entre l'affichage et l'achat (promotion terminée, prix modifié) : achat refusé avec « Le prix a changé », nouveau prix affiché, confirmation à refaire.
- Réessayer après un échec (fonds insuffisants, facture refusée…) fonctionne : la fenêtre ne reste plus bloquée sur « en attente de paiement ».
- Solde affiché à jour à l'étape de paiement.
- Factures de vente : à payer sous **48 h** (`sales.invoiceValidityHours`), sinon la vente est annulée et tout est libéré ; **2 factures en attente** au maximum par joueur.
- Reprise d'un véhicule acheté en concession : possible après **24 h** (`tradein.minOwnedHours`), jamais plus chère que le prix payé × coefficient de reprise.
- Commandes hors stock : à finaliser sous **7 jours** (`stock.orderReadyDays`), sinon annulées et remboursées ; plus de commande seul en mode vendeur obligatoire ni hors des horaires ; acompte payé avec un compte accepté par la concession.
- Essais routiers : caution remboursée sur le compte qui l'a payée, pires dégâts de l'essai retenus (réparer avant de rendre ne sert plus à rien), retour dans l'instance d'origine, délai entre deux essais conservé au redémarrage.
- Remboursement ou excédent de reprise que la société ne peut pas payer : « versement en attente », versé automatiquement dès que son compte le permet.

**Vendeurs**
- Validité d'un devis limitée au réglage de la concession.
- Devis remisé refusé à la signature si le vendeur a perdu le droit d'accorder cette remise.
- Remises répétées au même client signalées dans le journal.

**Patrons**
- Promotion en montant fixe limitée comme une promotion en pourcentage (une promotion « tout gratuit » est refusée).
- Commissions par grade plafonnées à 20 % (`commission.maxRate`).
- Nouvelle carte « Versements en attente » dans le tableau de bord.

**Administration**
- Tableau de bord : encart « À traiter » (ventes payées non livrées, factures remboursées après livraison, contrats sans échéance, dettes des sociétés) ; derniers logs réservés à la permission « logs ».
- « Relancer la livraison » reprend à l'étape manquante, sans second véhicule ni second paiement.
- Annulation refusée pour une vente dont la facture est déjà en partie payée.
- Suppression d'une concession refusée tant qu'il reste ventes, financements, commandes ou occasions.
- Import « Remplacer » : modèles absents désactivés (jamais supprimés), import refusé si une ligne est invalide ; suppression d'un modèle encore utilisé refusée.
- Financement : « Libérer » laisse un délai de paiement ; un véhicule financé passé à un autre joueur n'est jamais saisi (contrat gelé et signalé).
- Identifiants des joueurs visibles seulement avec la permission de don de véhicule.
- Nouveaux réglages : prix plancher, validité des factures, factures en attente par joueur, délai avant reprise, délai de finalisation des commandes, commission maximale, ressources autorisées.

### Sécurité et fiabilité

- Achat puis reprise immédiate d'un véhicule bon marché avec options d'usine : la boucle qui créait de l'argent est fermée.
- Livraison reprenable étape par étape ; client remboursé si la livraison échoue avant l'inscription du véhicule.
- Aucun versement d'une société sans débit (dettes `opw_dealership_debts`) ; grand livre de tous les mouvements (`opw_dealership_ledger`).
- Un devis ou une commande ne donne lieu qu'à une seule vente ; prélèvements et remboursement anticipé ne se chevauchent plus.
- Plaques personnalisées réservées de façon atomique et persistante ; aucun doublon de plaque, y compris sous QBCore.
- Stock jamais réécrit depuis le cache (plus de survente).
- Les joueurs ne peuvent plus modifier les fiches du catalogue (stats, énergie) depuis l'aperçu.
- Table ESX `vehicles` : seules les lignes créées par la concession sont modifiées, jamais sous QBCore.
- Codes promo : même réponse pour tout code refusé, 10 essais ratés par 10 minutes.
- Recherches et requêtes de plaques indexées ; liste des reprises en 4 requêtes ; plus de rechargement des véhicules d'exposition à chaque vente.

### À faire avant de mettre à jour

1. Mettre à jour **opw_bridge en 1.0.1** en même temps.
2. Ajouter dans *Paramètres › Intégrations › Ressources autorisées* (groupe racine) les scripts qui appellent `GiveVehicle` ou `GeneratePlate` : sinon ils sont refusés.
3. Vérifier la console au premier démarrage : `migration 003_reliability appliquee`.

---

## opw_bridge 1.0.1 (18/10/2026)

- Permissions : un administrateur qui n'est pas du groupe racine ne peut plus modifier ni supprimer un groupe dont les droits dépassent les siens.
- Les codes d'erreur d'une ressource ne sont plus modifiés par le module de permissions.
