# SCHEMA.md — v2

Changement majeur depuis v1 : le sujet d'une fiche est une **capacité**,
pas un scope item. Les deux éditions s'évaluent en parallèle sous la même
capacité.

Raison : sur Public Edition le scope item est l'unité de périmètre
(énumérable, activable, bornée). Sur Private Edition ce n'est pas le cas —
le périmètre fonctionnel classique PM/CS existe indépendamment du contenu
Best Practices, et la modification du standard reste ouverte. Une fiche
par scope item avec une colonne « privé » n'aurait rien où accrocher la
moitié des capacités privées.

---

## Structure d'une fiche capacité

```
## CAP-018 — Garantie déclenchée à la mise en route
- domaine: [service/contrats-garanties]
- theme: [cs2fs/facturation-contrats, objet/contrats-garanties]
- besoin_type: "date de départ de garantie ≠ date de livraison"
- exemples_client: [EC/CSF-004]

### public
- unite: scope item <ID>
- disponibilite: natif | config | ext-key-user | btp | absent
- echelon: 1..4                      # 5 impossible par construction
- reserve: "..."                     # limite précise rencontrée
- source: <doc + section>
- release_evaluee: 2608
- evalue_le: 2026-09-14
- pays_disponibles                   #Public Edition se livre pays par pays

### private
- unite: composant classique <transaction / module> | scope item <ID>
- disponibilite: natif | config | ext-key-user | btp | modif-core | absent
- echelon: 1..5
- reserve: "..."
- source: <doc + section>
- release_evaluee: 2023 FPS02
- evalue_le: 2026-09-14

### verdict
- edition: neutre | penche-prive | bloquant-public | bloquant-partout
- justification: une phrase
```

---

## Le champ qui porte tout : `verdict.edition`

- `neutre` — les deux éditions couvrent, même échelon ou presque.
  La capacité ne pèse pas dans le choix d'édition.
- `penche-prive` — couvert des deux côtés, mais nettement plus cher
  ou plus contraint en public (échelon 3-4 contre 1-2).
- `bloquant-public` — nécessite en privé un échelon 5 (modification du
  core) ou un composant sans équivalent public. **C'est le seul
  verdict qui décide vraiment.**
- `bloquant-partout` — ni l'un ni l'autre. Va vers un tiers ou un
  side-by-side BTP, et doit être remonté très tôt en avant-vente.

Une fois la base peuplée, la question d'origine devient une requête :

> compter les `bloquant-public` sur le périmètre du client.
> Zéro → public défendable. Un ou deux → arbitrage.
> Plus → le privé n'est pas une préférence, c'est une conséquence.

C'est ce qui transforme un débat d'opinion en argumentaire comptable.

---

## Les deux éditions ne vieillissent pas au même rythme

D'où `release_evaluee` et `evalue_le` **dans chaque bloc**, jamais au
niveau de la fiche.

- Public Edition : cadence trimestrielle, upgrade subi. Un bloc `public`
  évalué il y a trois trimestres est suspect par défaut.
- Private Edition : cadence annuelle, upgrade choisi. Un bloc `private`
  vieillit lentement.

Conséquence pratique : prévoir un passage de revalidation du seul bloc
`public`, une fois par trimestre, sur les fiches à verdict
`bloquant-public` ou `penche-prive`. Les fiches `neutre` peuvent attendre.
C'est ~15 % des fiches, pas la base entière.

---

## Ce qui doit être coupé pour que ça tienne

Deux éditions, ce n'est pas deux fois plus de fiches — c'est deux fois
plus de travail par fiche. Le budget est le même. Donc on réduit la
largeur, pas la profondeur :

- **Périmètre strictement PM/CS.** Maintenance, service, exécution
  terrain, contrats, pièces. Pas de finance, pas d'achats, pas de
  production, même quand un besoin client y touche. Une fiche hors
  périmètre note simplement `hors-perimetre` et un renvoi.
- **Pas de capacité `neutre` évidente.** Créer un ordre de service
  existe partout. Ne pas produire la fiche. La base sert à décider,
  pas à documenter SAP.
- **Priorité aux zones de friction connues.** Mobilité hors ligne,
  optimisation de tournées, refonte d'écran, champs obligatoires
  conditionnels, sous-traitance, interfaces MES/PLM, sérialisation,
  multi-pays. C'est là que les verdicts non-neutres se concentrent.

Cible réaliste : **40 à 60 fiches** à fin décembre, toutes à verdict
renseigné, plutôt que 150 fiches à moitié évaluées.

---

## Test de sortie

La base est utile le jour où, sur un besoin client formulé en une
phrase, tu produis en moins de deux minutes : la ou les capacités
concernées, l'échelon dans chaque édition, la réserve, et la source
documentaire. Sans ouvrir un PDF.

Si ça prend dix minutes, le problème est l'indexation (thèmes,
`besoin_type`), pas le contenu.
