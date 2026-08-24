# sap-maintenance-repo

Référentiel de processus et de capacités maintenance & service SAP
(PM/CS, S/4HANA Cloud Public Edition, S/4HANA Private Edition, SAP
Field Service and Asset Management), indépendant de tout client.

## Ce que c'est

Une arborescence de domaine (`ARBORESCENCE.md`) qui décompose la
maintenance et le service de façon stable — la même chez n'importe quel
client. Chaque nœud peut porter une ou plusieurs **fiches capacité**
(`fiches/`), qui évaluent comment chaque édition SAP couvre ce besoin,
avec verdict, source documentaire et date d'évaluation.

L'objectif : sur un besoin exprimé en une phrase par un client, retrouver
en moins de deux minutes la ou les capacités concernées, le niveau de
couverture par édition, et la source — sans rouvrir un PDF.

## Ce qui y entre

- La structure de domaine (`ARBORESCENCE.md`), ses nœuds et ses renvois.
- Le schéma de fiche (`SCHEMA.md`).
- Les fiches capacité (`fiches/`), une par capacité, remplies au fil de
  l'eau, sourcées, datées.
- La méthode d'ingestion d'un document en fiche (`METHODE.md`).

## Ce qui n'y entre pas

- **Aucun besoin client dans la structure.** Un besoin client sert à
  tester le référentiel (voir `cas-tests/`), jamais à créer ou renommer
  un nœud. La structure vient du domaine, pas du client.
- Le contenu verbatim de la documentation SAP — on garde la référence
  (document, section, release), jamais une copie qui périmera sans
  qu'on le sache.
- Toute information confidentielle propre à un client au-delà de ce qui
  est nécessaire pour comprendre un cas de test.

## `cas-tests/`

Corpus de besoins d'un client réel, reformatés dans le schéma, utilisés
pour vérifier la couverture du référentiel et détecter des incohérences
internes à la demande du client. Un dossier par client
(`cas-tests/<client>/`). Ce contenu ne fait jamais autorité sur la
structure — il s'y confronte.

## État au 24/08/2026

- Arborescence : 8 branches (M1 à M8), ~130 nœuds.
- Fiches capacité : 1 (CAP-M8.1.5-01, exemple travaillé).
- Cas de test : Electro Calorifique, 26 besoins (onglet CS2FS de la RFP).
- Scope items Public Edition confirmés : 11. Restants à vérifier via
  SAP Signavio Process Navigator — voir statut dans `ARBORESCENCE.md`.
