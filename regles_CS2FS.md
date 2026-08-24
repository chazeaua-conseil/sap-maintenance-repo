# Exigences CS2FS — Electro Calorifique

Source : `Annexe RFP_EC_Refonte ERP_Générales.xlsx`, onglet `1_CS2FS`
Extraction : 26 exigences, CSF-001 → CSF-026

## Schéma

| Champ | Rôle |
|---|---|
| `type` | typologie (liste) |
| `theme` | axe processus + axe objet (liste, cf. `themes.md`) |
| `priorite` | échelle client : 1 must / 2 need / 3 nice |
| `enonce` | **verbatim client**, jamais reformulé |
| `resume` | reformulation courte, la mienne |
| `couverture_rfp` | échelle client 0-3 — c'est ce qui part dans le tableur |
| `echelon` | échelle interne 1-5 — ne part pas chez le client |
| `si_candidat` | scope item SAP pressenti — **à vérifier release courante** |
| `moyen` | SSCUI / key-user ext. / ABAP Cloud / BTP / FSM natif / néant |
| `liens` | depend-de, precise, contredit |

⚠ **Les deux échelles ne sont pas la même et ne se convertissent pas.**
Voir la note en fin de fichier — c'est le point le plus important du document.

---

## CSF-001
- type: [processus-metier, regle-donnee]
- theme: [cs2fs/parc-clients, objet/tracabilite-serialisation]
- priorite: 1
- processus_rfp: Gestion du parc clients
- besoin_rfp: Traçabilité
- enonce: "Traçabilité intégrée ERP pour commandes, clients, chariots et composants sérialisés avec automatisation."
- resume: Sérialisation des chariots et composants, tracée bout en bout commande → client → parc.
- liens: [depend-de: CSF-022]

## CSF-002
- type: [processus-metier, regle-ui]
- theme: [cs2fs/intervention-terrain, objet/mobilite]
- priorite: 1
- processus_rfp: Intervention technique sur site
- besoin_rfp: Intervention terrain
- enonce: "Application mobile terrain avec prise de photo, CR intervention, signature électronique client, accès documentation technique et synchronisation temps réel."
- resume: Cœur FSM. Photo, compte rendu, signature, doc technique, synchro.
- liens: [depend-de: CSF-016, INT-008]

## CSF-003
- type: [processus-metier]
- theme: [cs2fs/parc-clients, objet/portail-communication]
- priorite: 3
- besoin_rfp: Portail client
- enonce: "Portail web client avec accès au parc de chariots, dossiers techniques, plans, historique interventions."

## CSF-004
- type: [processus-metier, regle-workflow]
- theme: [cs2fs/facturation-contrats, objet/contrats-garanties]
- priorite: 1
- besoin_rfp: Gestion SAV et maintenance
- enonce: "Gestion automatisée des dates de garanties produits liées aux commandes et clients avec règle de déclenchement à la mise en route."
- resume: Point d'attention : le départ de garantie est la **mise en route**, pas la livraison ni la facturation.
- liens: [precise: CSF-025]

## CSF-005
- type: [regle-donnee]
- theme: [cs2fs/preparation-pieces, objet/stocks]
- priorite: 1
- besoin_rfp: Gestion des stocks
- enonce: "Gestion des pièces détachées et rechanges avec états multiples (neuf, reconditionné, réparé, HS, sous garantie)."
- resume: Cinq états de pièce. Détermine le modèle de données stock.

## CSF-006
- type: [processus-metier, regle-ui]
- theme: [cs2fs/preparation-pieces, objet/mobilite, objet/stocks]
- priorite: 1
- besoin_rfp: Gestion des stocks terrain
- enonce: "Accès mobilité pour consultation, prélèvement et sortie de stock avec visibilité temps réel stock camion et magasin."
- resume: Stock camion (van stock) visible en temps réel depuis le terrain.
- liens: [depend-de: INT-007]

## CSF-007
- type: [reporting]
- theme: [cs2fs/suivi-satisfaction, objet/pilotage-reporting]
- priorite: 2
- besoin_rfp: Pilotage performance
- enonce: "Dashboard indicateurs avec taux de résolution 1er passage, délai moyen intervention, rotation stock pièces, satisfaction client, nombre contrats actifs."

## CSF-008
- type: [processus-metier, regle-donnee]
- theme: [cs2fs/facturation-contrats, objet/contrats-garanties]
- priorite: 1
- besoin_rfp: Contrats maintenance
- enonce: "Typologie et gestion intégrée des contrats clients avec niveaux de service associés."

## CSF-009
- type: [processus-metier, regle-workflow]
- theme: [cs2fs/facturation-contrats, objet/contrats-garanties]
- priorite: 1
- besoin_rfp: Contrats maintenance
- enonce: "Gestion complète du cycle de vie des contrats de maintenance avec reconduction automatique."
- liens: [precise: CSF-008]

## CSF-010
- type: [processus-metier]
- theme: [cs2fs/preparation-pieces, objet/logistique-sav]
- priorite: 2
- besoin_rfp: Logistique SAV
- enonce: "Cockpit de suivi des pièces détachées avec messagerie, colisage, statut logistique et expédition liés aux interventions."

## CSF-011
- type: [reporting]
- theme: [cs2fs/parc-clients, objet/pilotage-reporting]
- priorite: 1
- besoin_rfp: Pilotage client
- enonce: "Tableau de bord client consolidé avec vue préventif/curatif et ensemble des interventions planifiées et terminées."

## CSF-012
- type: [processus-metier]
- theme: [cs2fs/preparation-pieces, objet/stocks]
- priorite: 1
- besoin_rfp: Approvisionnement
- enonce: "Gestion réapprovisionnement avec DAV (Disponible À Vente) au niveau devis et commande de vente."
- liens: [depend-de: S2P-007]

## CSF-013
- type: [regle-donnee, processus-metier]
- theme: [cs2fs/preparation-pieces, objet/stocks]
- priorite: 1
- besoin_rfp: Gestion des stocks
- enonce: "Politique de stock intégrée avec gestion CBN (Calcul Besoin Net), stocks mini et stocks sécurité."
- liens: [depend-de: S2P-009]

## CSF-014
- type: [reporting]
- theme: [cs2fs/qualification-demande, objet/pilotage-reporting]
- priorite: 1
- besoin_rfp: Pilotage support
- enonce: "Tableau de bord dimensionnement charge support avec traçage appels et mails entrants par type d'événement."
- liens: [depend-de: CSF-024]

## CSF-015
- type: [regle-donnee, processus-metier]
- theme: [cs2fs/facturation-contrats, objet/tarification-recouvrement]
- priorite: 2
- besoin_rfp: Tarification SAV
- enonce: "Gestion automatisée des tarifications et prix des interventions avec coût matière et main d'œuvre."

## CSF-016
- type: [regle-ui, regle-interface]
- theme: [cs2fs/intervention-terrain, objet/mobilite]
- priorite: 2
- besoin_rfp: Gestion hors ligne
- enonce: "Capacité de travail offline avec synchronisation automatique au retour réseau."
- resume: Mode déconnecté. Contrainte structurante, pas une option de confort.

## CSF-017
- type: [regle-donnee]
- theme: [cs2fs/reception-reclamation, objet/referentiel-client]
- priorite: 1
- besoin_rfp: Gestion clients
- enonce: "Base clients structurée avec gestion multi-contacts (facturé, payeur, livré, adresse logistique)."
- liens: [contredit-partiellement: QTO-020]
- note: QTO-020 énonce le même besoin avec une liste de rôles différente
  (contact, payeur, acheteur, livré, groupement achat, distributeur).
  **Divergence à trancher avant chiffrage** — exemple type de ce que la
  détection d'incohérence doit remonter.

## CSF-018
- type: [regle-workflow]
- theme: [cs2fs/qualification-demande, objet/ticketing-relances]
- priorite: 2
- besoin_rfp: Relances commerciales
- enonce: "Gestion automatisée des relances devis (pièces, interventions, contrats) avec paramétrage montant, délai et caractéristiques."

## CSF-019
- type: [regle-workflow]
- theme: [cs2fs/facturation-contrats, objet/tarification-recouvrement]
- priorite: 1
- besoin_rfp: Recouvrement
- enonce: "Gestion automatisée des relances factures avec gestion des impayés et relances multiples."

## CSF-020
- type: [regle-donnee]
- theme: [cs2fs/reception-reclamation, objet/referentiel-client]
- priorite: 1
- besoin_rfp: Segmentation commerciale
- enonce: "Gestion de la segmentation client multi-niveaux avec typologies adaptées (grand compte, contrat Or, priorité)."
- liens: [depend-de: CSF-017, precise-par: QTO-013]

## CSF-021
- type: [regle-ui, processus-metier]
- theme: [cs2fs/preparation-pieces, objet/mobilite, objet/stocks]
- priorite: 2
- besoin_rfp: Logistique magasin
- enonce: "Mobilité sur les mouvements de stocks avec scan codes-barres pour entrées/sorties marchandises."

## CSF-022
- type: [regle-donnee]
- theme: [cs2fs/preparation-pieces, objet/stocks, objet/tracabilite-serialisation]
- priorite: 1
- besoin_rfp: Gestion des stocks
- enonce: "Gestion multi-emplacements de stockage avec gestion par lot et sérialisé."
- resume: Lot **et** série. Choix structurant du modèle de données.

## CSF-023
- type: [regle-interface, processus-metier]
- theme: [cs2fs/intervention-terrain, objet/portail-communication]
- priorite: 1
- besoin_rfp: Communication client
- enonce: "Notification automatique BL/liste colisage expédié avec tracking transporteur (TNT, Kuhn)."
- resume: Interface transporteur non listée dans l'onglet `10_Interfaces`.
- note: **Interface manquante au recensement.** INT-001→008 ne couvre
  aucun flux transporteur. À ajouter.

## CSF-024
- type: [processus-metier, regle-workflow]
- theme: [cs2fs/qualification-demande, objet/ticketing-relances]
- priorite: 2
- besoin_rfp: Support client
- enonce: "Outil de ticketing centralisé pour tracer les demandes clients avec routage automatique."

## CSF-025
- type: [processus-metier]
- theme: [cs2fs/parc-clients, objet/contrats-garanties]
- priorite: 1
- besoin_rfp: Gestion du parc client
- enonce: "Vision consolidée du parc avec alertes de maintenance préventive et échéances de garantie."
- liens: [depend-de: CSF-004]

## CSF-026
- type: [processus-metier]
- theme: [cs2fs/planification-intervention, objet/mobilite]
- priorite: 2
- besoin_rfp: Planification interventions
- enonce: "Planification et optimisation automatique des tournées d'interventions avec géolocalisation."
- resume: Optimisation de tournées. Point de bascule classique standard / moteur dédié.

---

# Note de méthode — pourquoi deux échelles de couverture

L'onglet `Read Me first` impose l'échelle client :

```
0 = non couvert
1 = spécifique (modification du code standard OU développements spécifiques)
2 = standard, paramétrage complexe
3 = paramétrage simple
```

**Cette échelle ne peut pas répondre à la question public cloud vs private cloud.**
Son niveau 1 agrège deux réalités que le cloud public sépare radicalement :

- une extension key-user ou une app BTP side-by-side → **faisable en public cloud**
- une modification du code standard → **impossible en public cloud**

Réponse `1` pour les deux. L'information qui décide de l'architecture est
donc perdue au moment même où on remplit le tableur.

D'où la règle : **on remplit l'échelle client telle quelle** (c'est
contractuel, c'est ce qui sert à comparer les intégrateurs), et on tient
**en parallèle** l'échelon interne :

```
1 standard (scope item natif)          → répond 3 ou 2 côté client
2 configuration SSCUI                  → répond 2 ou 3
3 extensibilité key-user               → répond 1 côté client
4 ABAP Cloud / BTP side-by-side        → répond 1 côté client
5 modification du core nécessaire      → répond 1 côté client
```

Public cloud défendable si l'échelon 5 est vide et l'échelon 4 court.
C'est une affirmation **comptable**, pas une opinion — et c'est
l'argumentaire qu'aucun concurrent ne produira à partir du seul tableur.

---

# Ce que l'extraction a révélé

**Champs remplis sans effort** — `type`, `theme`, `priorite`, `enonce`,
`source`. La RFP est structurée : ses colonnes *Processus* et *Besoin
fonctionnel* donnent la hiérarchie de thèmes gratuitement.

**Champs qui ont résisté :**

1. `si_candidat` et `moyen` — laissés vides **délibérément**. Inventer des
   numéros de scope item empoisonnerait la base : les identifiants et les
   frontières d'extensibilité bougent à chaque release. À remplir contre la
   documentation SAP courante, en notant la release d'évaluation.
2. `type` — un tiers des exigences en portent deux ou trois. Confirme qu'un
   slot unique aurait menti.
3. Une catégorie manquait à ta typologie : **`reporting`** (CSF-007, 011,
   014). Ni processus, ni UI, ni autorisation, ni workflow — et un chemin
   d'implémentation distinct (analytique embarquée / SAC). Ajoutée.
4. `liens` — le champ le plus coûteux à remplir et le seul qui produise de
   la valeur immédiate. Voir ci-dessous.

**Trois incohérences remontées dès le premier onglet :**

- **CSF-017 vs QTO-020** — même besoin de référentiel client
  multi-contacts, deux listes de rôles différentes. À trancher avant
  chiffrage.
- **CSF-023** — flux transporteur (TNT, Kuhn) exigé, absent du recensement
  d'interfaces `10_Interfaces` (INT-001 à 008).
- **Dépendances hors CS2FS** — CSF-012 et CSF-013 renvoient à des exigences
  S2P (007, 009). Chiffrer CS2FS isolément fera doublon ou trou.

C'est la preuve du concept : trois anomalies exploitables sur un seul
onglet, uniquement grâce à la structure. Aucune expertise SAP mobilisée.
