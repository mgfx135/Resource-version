# Notes de version des ressources GN

Les versions publiées sont listées dans `versions.json` (lu par GN_Bridge). Ce fichier détaille ce qui change d'une version à l'autre.

---

## Renommage OPW vers GN (03/11/2026)

Toutes les ressources OPW s'appellent désormais GN_*. **Aucun alias : les anciens noms ne fonctionnent plus.**

- Global `GN`, permissions `gn.<ressource>.admin`, hub `/gn`, tables `gn_*`, comptes `GN-####-####`.
- `GN_Fuel` désigne l'ex-opw_fuel. L'ancien script GN_Fuel n'est plus pris en charge, ni ses niveaux en litres.
- `opw_notif`, `opw_location` et `opw_minimap` ne sont plus détectés.

## GN_Bridge 1.5.1 et GN_Clothing 1.13.1 (08/11/2026)

- **GN_Bridge 1.5.1** : chaque vérification des mises à jour écrit une ligne en console : la liste des ressources en retard avec leur changelog, « les N ressources GN installées sont à jour », ou la raison d'un échec (HTTP, fichier illisible, vérification désactivée). `gn updates` dans la console du serveur vérifie tout de suite.
- **GN_Clothing 1.8.0 à 1.13.1** : animations fournies avec la ressource (dossier `stream`) pour enfiler et retirer chaque pièce : tête (chapeau, masque, lunettes, boucles d'oreilles), buste (haut, sous-vêtement, gilet, collier, sac, tenue complète), mains (gants, montre, bracelet), pantalon et chaussures en corps entier. Réglées par pièce dans `Config.CustomAnims`, repli sur les animations GTA. Commande `/clothinganim <pièce> <on|off>` pour les voir. Les poses de l'écran des personnages ajoutées en 1.13.0 ont été retirées en 1.13.1.

## GN_Housing 1.7.0 et GN_Identity 1.2.0 (08/11/2026)

- **GN_Housing 1.7.0** : huit animations fournies avec la ressource (dossier `stream`) : clé dans la serrure, sonner et frapper à la porte, fouille du coffre, remise des clés, signature du contrat, présentation par l'agent, cambriolage, perquisition.
- **GN_Identity 1.2.0** : animations fournies avec la ressource : regarder sa carte, la montrer (et celui qui la regarde), scanner de la police, guichet (l'agent tape et tend la carte, le joueur la prend). Correctif : « Ajouter une catégorie » au guichet ne transmettait pas la catégorie.
- Dans les deux ressources, chaque animation se coupe dans `Config.CustomAnims` ; si un fichier ne se charge pas, l'animation GTA d'origine est jouée à la place.

## GN_Ambulance 1.3.0 (08/11/2026)

- **Animations custom** fournies avec la ressource (dossier `stream`) : patient allongé sur le brancard (conscient ou inconscient), poussée du brancard, attente des soins selon la zone blessée, gestes du secouriste (compression, pansement, attelle, suture, garrot).
- Chaque animation se coupe dans `Config.CustomAnims` ; si un fichier ne se charge pas, l'animation GTA d'origine est jouée à la place.

## GN_Ambulance 1.2.0 (08/11/2026)

- **Missions PNJ refaites** : missions perso lancées depuis le menu F6, objets requis pour chaque geste (défibrillateur, sédatif, crème contre les brûlures, etc.), PNJ médecin et bonus de fin de mission, brancard repris.
- **Base de données** : migration 4 (table `gn_ambulance_mission_spots`), appliquée au démarrage.
- **ox_inventory** : nouveaux items dans `ox_items.lua`, images dans `install/ox_inventory/web/images` à copier dans `ox_inventory/web/images`.

## GN_Identity 1.1.0 et GN_Ambulance 1.1.1 (07/11/2026)

- **GN_Identity 1.1.0** : conditions d'achat par document et par catégorie de permis, réglées dans le panel (licence esx_license / QBCore, ou autre papier GN : le permis C exige le B). Permis de conduire, bateau, pilote et port d'arme achetés au guichet, qui indique ce qui manque. Plaque et image du véhicule sur la carte grise (image lue dans GN_Garage).
- **GN_Ambulance 1.1.1** : `/revive me`, `/heal me` et `/kill me` visent soi-même ; `/heal`, le lit de l'accueil et l'export `Heal` remettent aussi la faim et la soif au maximum ; commande `/blessures` retirée.

## Mise à jour du 07/11/2026

**Nouvelles ressources**

- **GN_Police 1.2.0** : métier de policier sur le terrain (départements et commissariats, service, menottes, fouille, contrôles, garde à vue, armurerie, route, preuves, K9, hélicoptère, missions PNJ animées, tableau du patron, API, version lite). Remplace esx_policejob.
- **GN_Ambulance 1.1.0** : mort des joueurs et métier d'ambulancier (services médicaux et hôpitaux, réanimation, blessures, soins en mini-jeux, brancard, pharmacie, morgue, application lb-phone, tableau du patron, API, version lite). Remplace esx_ambulancejob : arrêtez-le, ou coupez « GN_Ambulance gère la mort des joueurs ».
- **GN_Clothing 1.7.7** : vêtements en items ox_inventory et slots d'équipement, sélection des personnages, identité et créateur, magasins avec stock et soldes, coiffeur et tatoueur façon GTA Online, vestiaires de métier, panel et statistiques, API, version lite. Remplace esx_skin et skinchanger. Images dans la ressource GN_Clothing_images.
- **GN_Identity 1.0.0** : papiers officiels (carte d'identité, passeport, permis et licences synchronisés avec esx_license, cartes grises, cartes professionnelles), points de permis, guichet de mairie, faux papiers, contrôle par la police, application Wallet, API, version lite.
- **GN_Restaurant 1.1.0** : restauration générique (fast-food, restaurant, bar, café, food truck), cuisine en mini-jeux, borne libre-service, salle et réservations, clients PNJ, approvisionnement, livraisons, alcool, application lb-phone GN Food, API, version lite.
- **GN_News 1.0.0** : métier de journaliste (médias concurrents, articles et relecture, journal papier, application lb-phone GN News, carte de presse, reportage et drone, directs, alertes à couvrir, publicités, API, version lite).

**Mises à jour**

- **GN_Bridge 1.5.0** : module GN.Status faim et soif (esx_status, QBCore), module emotes, adaptateurs de vêtements, GN_MDT détecté en premier comme dispatch, lb-phone étendu (Wallet, mail, localisation, déverrouillage), `GN.Invoice.Pay`. Requis par GN_Police, GN_Clothing, GN_Ambulance et GN_Restaurant.
- **GN_MDT 1.1.5** : tablette façon iPad (accueil, apps, dock, sélecteur d'apps), panneau d'appel en jeu, patrouilles, alertes automatiques, amendes et convocations par mail, mandats de localisation et de déverrouillage du téléphone, formations des agents pour GN_Police, dossiers médicaux ouverts à GN_Ambulance.
- **GN_Dealership 1.6.0** : concessions métier (achat payé par la société du job, grade minimum par concession et par véhicule, livraison au garage métier GN_Garage, remise en %). Migration SQL 005. Police, Ambulance et Restaurant achètent désormais leurs véhicules ici, et les sortent par GN_Garage.
- **GN_Customs 1.12.1** : portes, capot et coffre ouverts selon la pièce travaillée (réglage par atelier), tunnels de lavage façon GTA, couleurs de peinture addon lues depuis la ressource `gn_paints`.
- **GN_Bank 1.3.0** : application Wallet de lb-phone (opérations du compte courant, message à chaque virement).
- **GN_Garage 1.4.1** : GN_Ambulance dans la liste blanche par défaut de l'API. Si la liste a déjà été enregistrée dans le panel, l'y ajouter à la main.

---

## Versions publiées le 03/11/2026

- **GN_Bridge 1.1.3** : Socle GN.Api pour les exports publics, relais de toutes les alertes GN.Dispatch, journal aligne malgre les champs vides, hierarchie des groupes dans les permissions.
- **GN_Bank 1.2.0** : API d'exports 2.0.0 (anciens exports retires), facade de distributeur realiste, application lb-phone refaite, choix de la carte au paiement.
- **GN_Customs 1.9.0** : Preparation (kit drift, transmission, boite), taille et largeur des roues, carnet d'entretien et usure des organes, application lb-phone, API d'exports 2.0.0 (anciens exports retires).
- **GN_Dealership 1.5.0** : Reprise selon le carnet d'entretien, types de garage et kilometrage lus depuis GN_Garage, application Concession refaite, API d'exports 2.0.0 (anciens exports retires).
- **GN_Fuel 1.3.0** : Facteur de consommation par vehicule, commande /fuelconso, API d'exports 2.1.0 (anciens exports retires). Prend le nom de l'ancien script GN_Fuel, qui n'est plus pris en charge.
- **GN_Garage 1.4.0** : Kilometrage des vehicules, types de garage forces par modele, nombre de places, masquage du HUD a l'ouverture, API d'exports 2.0.0 (anciens exports retires).
- **GN_Housing 1.6.1** : Catalogue de 106 interieurs, vie quotidienne, multi-agences, application Dynasty, menu F6 de l'agence, zones MLO, API d'exports 2.0.0 (anciens exports retires), hook beforeRaid.
- **GN_Invoice 1.2.0** : API d'exports 2.0.0 (anciens exports retires), comptes GN_Bank pour la facturation.
- **GN_Taxi 1.1.0** : Metier taxi : compagnies, courses, application lb-phone, tableau du patron, progression, API 2.0.0, version lite. 1.1.0 : menu F6 du chauffeur, vraie carte GTA, missions PNJ, avis des clients.
- **GN_MDT 1.0.0** : Premiere version : departements, fiches, code penal, rapports, prison, mandats, dispatch, RH, secours, justice, mairie, API 2.0.0, version lite.
- **GN_VehicleKeys 1.2.0** : API d'exports 2.0.0 (anciens exports retires), carte bancaire independante au serrurier.
- **GN_VehicleMenu 1.0.0** : Renommage OPW vers GN (tables, ACE, exports).

---

## GN_Customs 1.1.0 (18/10/2026)

Version de correctifs issue d'un audit complet de la ressource. Les tables se mettent à jour toutes seules au premier démarrage (migrations versionnées dans `gn_customs_schema`).

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
- GN Invoice : une facture payée après la fermeture de l'atelier, ou après un redémarrage, est appliquée au véhicule ; si c'est impossible, le client est remboursé. Le mode « Facturer après » est réservé au propriétaire du véhicule.

**Menu patron**
- **Recrutement par invitation** : le joueur accepte ou refuse l'offre d'embauche (45 s).
- Plafonds sur 24 h : primes (100 000 $ par défaut) et retraits du coffre (réglable, sans limite par défaut).
- Statistiques justes sur 7 / 30 / 90 jours, ventes payées par une société comprises ; un bandeau signale une période trop chargée.
- Paiements par carte comptés avec la banque.
- Codes promo : 5 caractères minimum pour un nouveau code, remise plafonnable par l'admin, l'auteur d'un code ne peut ni se le réserver ni l'utiliser.

**Menu métier (F6)**
- Fourrière sans GN_Garage : les véhicules créés par un script (location, service) ne sont plus supprimés, seulement la circulation PNJ.
- Une facture GN Invoice par minute et par client.

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
- Ventes enregistrées dans une table dédiée `gn_customs_sales`, jamais purgée et indépendante des journaux.
- Colonne `payment` élargie : les ventes payées par une société sont de nouveau journalisées.
- Purge des journaux par lots, index ajoutés pour le menu patron.
- Remboursement ligne par ligne si un élément ne peut pas être enregistré ; plus aucun remboursement sur un autre compte que celui débité.

### À faire avant de mettre à jour

1. Si vous masquez des HUD d'autres ressources que `hud`, `gn_minimap` ou `GN_Hud`, ajoutez-les dans `Config.HudActionResources` : sinon ces actions sont retirées au démarrage.
2. Remplacez les logos et images en `http://` par des adresses `https://`.
3. Vérifiez *Paramètres > Propriétaire uniquement* selon votre usage (véhicules partagés entre joueurs).

---

## GN_Dealership 1.1.0 (18/10/2026)

Version de correctifs issue d'un audit complet de la ressource. Nécessite **GN_Bridge 1.0.1**. La migration `003_reliability` s'applique au premier démarrage (nouvelles colonnes et tables, index).

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
- Aucun versement d'une société sans débit (dettes `gn_dealership_debts`) ; grand livre de tous les mouvements (`gn_dealership_ledger`).
- Un devis ou une commande ne donne lieu qu'à une seule vente ; prélèvements et remboursement anticipé ne se chevauchent plus.
- Plaques personnalisées réservées de façon atomique et persistante ; aucun doublon de plaque, y compris sous QBCore.
- Stock jamais réécrit depuis le cache (plus de survente).
- Les joueurs ne peuvent plus modifier les fiches du catalogue (stats, énergie) depuis l'aperçu.
- Table ESX `vehicles` : seules les lignes créées par la concession sont modifiées, jamais sous QBCore.
- Codes promo : même réponse pour tout code refusé, 10 essais ratés par 10 minutes.
- Recherches et requêtes de plaques indexées ; liste des reprises en 4 requêtes ; plus de rechargement des véhicules d'exposition à chaque vente.

### À faire avant de mettre à jour

1. Mettre à jour **GN_Bridge en 1.0.1** en même temps.
2. Ajouter dans *Paramètres › Intégrations › Ressources autorisées* (groupe racine) les scripts qui appellent `GiveVehicle` ou `GeneratePlate` : sinon ils sont refusés.
3. Vérifier la console au premier démarrage : `migration 003_reliability appliquee`.

---

## GN_Bridge 1.0.1 (18/10/2026)

- Permissions : un administrateur qui n'est pas du groupe racine ne peut plus modifier ni supprimer un groupe dont les droits dépassent les siens.
- Les codes d'erreur d'une ressource ne sont plus modifiés par le module de permissions.
