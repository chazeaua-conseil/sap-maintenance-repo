# Fiches — 7Z2, Intégration ordre de travail ↔ FSM

Source : `7Z2_S4CLD2608_BPD_EN_DE.docx`, release 2608, lu le 27/08/2026
Prérequis : **4HH uniquement** (maintenance réactive)

---

## CAP-M7.4.2-02 — Intégration ordre de travail ↔ FSM

- noeud: M7.4.2, M3.3
- question_metier: "comment un ordre de travail de maintenance part-il
                    au terrain ?"
- formulations_client: ["ordre de travail sur tablette", "interface GMAO
                        terrain", "envoi de l'OT au technicien"]

### public
- unite: scope item 7Z2
- disponibilite: natif
- echelon: 2 (paramétrage lourd — voir CAP-M7.4.2-03)
- release_evaluee: 2608

**Correspondance d'objets — différente de 49X :**

| S/4HANA Cloud | FSM |
|---|---|
| Ordre de travail (YA01) | Service Call (External Id = n° d'ordre) |
| **Opération** de l'ordre | Activity |
| Composant d'opération | Reserved Material |
| Poste de travail (work center) | **Region** `WC_<Plant>_<WorkCenter>` |
| Phase / sous-phase de l'ordre | Service Call Status (mappé) |

**Déclencheur de réplication : configurable, et ce n'est PAS la
libération.** Par défaut l'ordre part vers FSM au passage en *Ready to
Schedule* (phase Scheduling). Les couples phase/sous-phase déclenchants
se paramètrent (06/0060, 07/0065, 07/0070, 08/0080, 09/0085).

**Chaîne amont complète documentée :** avis de maintenance (F5777) →
screening par le superviseur, accepté / rejeté / complément demandé
(F4072) → création et planification de l'ordre (F4604) → **workflow
d'approbation flexible** (F4989 ; approbation automatique si aucun
workflow personnalisé n'est défini) → libération → demandes d'achat
pour non-stock et prestations → *Ready to Schedule* → FSM.

**Bidirectionnel et plus riche que 49X :** depuis FSM, la création
d'une **nouvelle activité** crée une **nouvelle opération** dans
l'ordre S/4. La modification du service call remonte sur l'en-tête
(description, texte long, priorité, activity type, dates, responsable) ;
la modification d'une activité remonte sur l'opération (description,
texte long, durée, dates planifiées).

- source: 7Z2 BPD, §2.6.9, §4.1 à §4.5
- verdict: neutre
- confiance: haute

### pratique
- question_a_poser: "À quel moment de votre processus l'ordre doit-il
                     partir au terrain — à la libération, ou seulement
                     une fois ordonnancé ? Le déclencheur est
                     paramétrable, c'est une décision de conception."
- piege_connu: "Contrairement au flux service, le déclencheur n'est pas
   la libération. Un client qui raisonne 'libéré = parti au terrain' se
   trompe de modèle : entre libération et Ready to Schedule il y a la
   préparation et les achats."

---

## CAP-M3.3.1-02 — Types d'ordre réplicables vers FSM

- noeud: M3.3.1, M7.4.2
- question_metier: "tous mes ordres de travail peuvent-ils aller au
                    terrain ?"

### public
- disponibilite: **restreint**
- echelon: 4 ou plus selon le besoin

**⚠ Limitation majeure, écrite deux fois dans le document :**
*« Currently Order Type YA01 is only supported in FSM. »*

YA01 = *Reactive Maintenance*. Et la condition métier de 7Z2 ne cite
que **4HH**. Conséquences à vérifier d'urgence :

- La maintenance **préventive** (4HI), l'amélioration (4VT), la
  maintenance opérationnelle et frais généraux (4WM) **ne semblent pas
  réplicables vers FSM** en 2608.
- Un client dont les techniciens exécutent du préventif sur tablette —
  c'est-à-dire la quasi-totalité des industriels — se heurte
  directement à cette limite.

- source: 7Z2 BPD, §2.4 et §2.6.5 note du step 7
- verdict: **bloquant-public probable** pour tout client à forte
           composante préventive au terrain
- confiance: **moyenne** — l'absence de mention du préventif n'est pas
             une interdiction formelle. **À confirmer auprès de SAP
             avant tout engagement.** C'est la question la plus
             importante ouverte sur ce bloc.

### pratique
- question_a_poser: "Quelle proportion de vos interventions terrain est
                     préventive plutôt que curative ?"
- piege_connu: "Une démo réussie sur du curatif ne dit rien du
   préventif. Poser la question du type d'ordre avant, pas après."

---

## CAP-M7.4.2-03 — Charge de paramétrage de l'intégration

- noeud: M7.4.2, M7.3
- question_metier: "que coûte la mise en place de cette intégration ?"

### public
- disponibilite: natif mais **paramétrage substantiel**
- echelon: 2

**Onze activités de configuration SSCUI**, en plus du paramétrage FSM :

| SSCUI | Objet |
|---|---|
| 106807 | Configure Multiple Company Replication |
| 107205 | Define Plant Specific Order Types |
| 107206 | Define System Status to Filter Maintenance Order Replication |
| 107208 | Configure Mapping for Expense Type |
| 107209 | Configure Mapping for Expense Type Item |
| 107210 | Configure Mapping for Priority Codelist |
| 107211 | Configure Mapping for Problem Type Codelist |
| 107212 | Configure Region |
| 107213 | Configure Mapping for Service Call Type Codelist |
| 107215 | Default Business Partner Customer |
| 107247 | Configure Mapping for Phase Codelist |

Plus, côté S/4 : taux de coût (F3162), fiches info achat, workflow
flexible (F4989), stock initial. Côté FSM : création des **Regions**
depuis les postes de travail, au format `WC_<Plant>_<WorkCenter>`.

**Chaque mapping est à répéter pour chaque Company ID** en scénario
multi-société.

**Mapping de priorité — ici configurable** (contrairement à 49X) :

| S/4 Priority | FSM Priority |
|---|---|
| 1 | HIGH |
| 2 | HIGH |
| 3 | MEDIUM (défaut) |
| 4 | LOW |

Toujours quatre vers trois, mais le client choisit l'écrasement.

**Business Partner par défaut obligatoire :** un ordre de maintenance
n'a pas de client. Il faut donc désigner un BP fictif pour que la
réplication fonctionne. Symptôme d'un outil orienté service commercial
employé pour de la maintenance interne — à connaître, sans gravité.

- source: 7Z2 BPD, §2.6
- verdict: neutre
- confiance: haute

### pratique
- piege_connu: "Onze SSCUI de mapping, chacun à répéter par company.
   Ce n'est pas 'activer un scope item', c'est un chantier de
   paramétrage à part entière. À chiffrer explicitement — c'est
   typiquement ce qui est absorbé dans un forfait sous-évalué."

---

## CAP-M6.6-01 — Retour de pièce endommagée

- noeud: M6.6, M6.3
- question_metier: "comment tracer une pièce déposée et renvoyée au
                    magasin ?"

### public
- disponibilite: natif
- echelon: 2

Sur l'opération, un composant peut être saisi en **quantité négative**
pour planifier le retour d'une pièce endommagée au magasin. Le champ
**Batch** porte alors le **type de valorisation** (par exemple
`DAMAGED`) si l'article est en valorisation séparée ; sinon le champ
reste vide.

C'est le mécanisme standard pour l'état de pièce (nœud M6.3 : neuf,
reconditionné, réparé, HS) — **via la valorisation séparée**, pas via
un statut dédié.

- source: 7Z2 BPD, §4.1.4 step 7
- verdict: neutre
- confiance: haute

### pratique
- question_a_poser: "Vos pièces réparables sont-elles valorisées
                     différemment selon leur état ?"
- piege_connu: "L'état de pièce passe par la valorisation séparée
   (split valuation), décision structurante côté finance et logistique,
   à prendre tôt et difficile à reprendre ensuite."

---

## CAP-M1.2.1-01 — Dépose / pose d'équipement (mise à jour)

Absence **confirmée sur les deux scope items**. Dans 7Z2, l'équipement
est un champ de l'activité, modifiable depuis FSM et répliqué sur
l'opération — mais aucun flux de dépose, pose, ni mise à jour de la
structure du parc n'existe.

- verdict: **absent du standard d'intégration terrain**
- confiance: **haute** (deux sources indépendantes, absence constatée)
- à instruire: le geste existe-t-il en S/4 hors mobilité (4HH seul), et
  peut-il être porté au terrain autrement ? Sinon, c'est un écart à
  poser dès le premier atelier pour tout client gérant un parc
  d'équipements interchangeables.

---

## Limitation 2608 relevée

*« Expense confirmation does not support multiple company scenario in
2608. »* Un client multi-société perd la confirmation de frais. À
recroiser avec la roadmap.

---

# 49X vs 7Z2 — deux mécanismes, pas un

| | 49X (service) | 7Z2 (maintenance) |
|---|---|---|
| Origine | Ordre de service, ordre de réparation | Ordre de travail YA01 |
| Branche | M4 | M3 |
| Déclencheur | Libération | Phase configurable (défaut *Ready to Schedule*) |
| Granularité | Poste → Activity | **Opération** → Activity |
| Portée technicien | Service team (**non mappée**) | Work center → **Region FSM** |
| Priorité | Table figée | **Configurable** |
| Client | Réel | **BP par défaut fictif** |
| Création depuis FSM | Activité implicite **non répliquée** (défaut ouvert) | Nouvelle activité → **nouvelle opération** ✅ |
| Types supportés | Service et réparation | **YA01 seul** |
| Prérequis | 3D2, 3NI, 3MO | 4HH, 3NI |

**Conséquence de cadrage.** Un client qui exécute au terrain à la fois
des interventions vendues et de la maintenance sur ses propres actifs a
besoin des **deux** scope items, avec deux paramétrages distincts, deux
modèles de portée d'équipe, et deux comportements de déclenchement. Ce
n'est pas un chantier d'intégration, c'en est deux.

Le point 1 des « Points à contester » de `ARBORESCENCE.md` — faut-il
séparer M3 et M4 — est **tranché par la preuve** : SAP lui-même livre
deux scope items le long de cette frontière. À marquer comme réglé.

---

# Reste ouvert sur ce bloc

1. **Le préventif est-il réplicable vers FSM ?** Question la plus
   importante. À poser à SAP.
2. Mode déconnecté et résolution de conflit (M5.2.4) — non documenté
   dans les deux BPD. Chercher dans la documentation FSM.
3. Dépose / pose d'équipement (M1.2.1) — absent, contournement à
   instruire.
4. Comportement en charge, rejeu et reprise sur erreur CPI — les BPD
   décrivent le chemin nominal uniquement.
