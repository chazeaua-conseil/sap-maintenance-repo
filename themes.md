# Hiérarchie des thèmes — Electro Calorifique

Fichier séparé volontairement : le lien règle → thème doit rester
réétiquetable sans toucher aux règles elles-mêmes.

Deux axes coexistent. Une règle porte normalement un thème de chaque axe.
C'est la raison pour laquelle `theme` est une liste et non un slot unique.

## Axe 1 — Chaîne de processus (issue de la colonne « Processus » de la RFP)

```
cs2fs/
├── reception-reclamation        (CSF-017, 020)
├── qualification-demande        (CSF-014, 018, 024)
├── planification-intervention   (CSF-026)
├── intervention-terrain         (CSF-002, 016, 023)
├── preparation-pieces           (CSF-005, 006, 010, 012, 013, 021, 022)
├── parc-clients                 (CSF-001, 003, 011, 025)
├── facturation-contrats         (CSF-004, 008, 009, 015, 019)
└── suivi-satisfaction           (CSF-007)
```

Cet axe est **donné par le client**. Ne pas le renommer : c'est son
vocabulaire, il servira à la comparaison des réponses intégrateurs.

## Axe 2 — Objet fonctionnel (issu de la colonne « Besoin fonctionnel »)

```
objet/
├── mobilite                     (CSF-002, 006, 016, 021)
├── stocks                       (CSF-005, 012, 013, 021, 022)
├── contrats-garanties           (CSF-004, 008, 009, 025)
├── referentiel-client           (CSF-017, 020)
├── pilotage-reporting           (CSF-007, 011, 014)
├── tarification-recouvrement    (CSF-015, 019)
├── tracabilite-serialisation    (CSF-001, 022)
├── portail-communication        (CSF-003, 023)
├── ticketing-relances           (CSF-018, 024)
└── logistique-sav               (CSF-010)
```

## Axe 3 (transverse, hors CS2FS)

L'onglet `0_Transverse` (T01→T51) et `10_Interfaces` (INT-001→008)
alimenteront des thèmes transverses : `socle/habilitations`,
`socle/personnalisation`, `socle/extraction-import`, `socle/workflow`,
`interfaces/*`. À rattacher lors de l'ingestion de ces onglets.

Note : INT-007 et INT-008 (ERP ↔ FSM) sont les interfaces qui
conditionnent une grande partie du CS2FS.
