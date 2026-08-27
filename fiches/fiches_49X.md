# Fiches — 49X, Intégration ordre de service ↔ FSM

Source : `49X_S4CLD2608_BPD_EN_DE.docx`, release 2608, lu le 27/08/2026
Middleware : SAP Cloud Integration (CPI), iFlows, monitoring CPI

---

## CAP-M7.4.2-01 — Mécanisme d'intégration ERP ↔ exécution terrain

- noeud: M7.4.2
- question_metier: "comment l'ordre part au terrain et comment le retour revient ?"
- formulations_client: ["envoi de l'ordre sur la tablette", "interface
                        ERP terrain", "synchro FSM", "remontée du CR"]

### public
- unite: scope item 49X
- disponibilite: natif
- echelon: 1
- release_evaluee: 2608

**Correspondance d'objets :**

| S/4HANA Cloud | FSM |
|---|---|
| Service order (libéré) | Service Call |
| Service order item | Activity (une par poste de service) |
| Pièce détachée du poste | Reserved Material |
| Repair order (3XK) | Service Call de type RPO1 (value mapping) |
| Service contract (3MO) | Service Contract (master data) |

**Bidirectionnel.** S/4 → FSM à la libération ; FSM → S/4 à la création
d'un service call, à la validation des temps, dépenses, matériels et
kilomètres.

**Déclencheur de la confirmation :** ce n'est PAS la clôture par le
technicien, c'est **l'approbation par le planificateur** dans FSM. La
confirmation S/4 est alors créée et complétée automatiquement.

**Cycle de statut :** poste en *In Planning* dès réplication vers FSM,
*In Execution* dès libération à un technicien. Ordre complété dans S/4
→ service call passe en *Technically Completed*. Rejet de l'ordre →
service call *Technically Completed*, activités *Cancelled*.

- source: 49X BPD, §4.2 à 4.7
- verdict: neutre — l'intégration existe des deux côtés
- confiance: haute

### pratique
- question_a_poser: "Qui valide les temps avant facturation ? Ce rôle
                     existe-t-il chez vous, ou le technicien clôture-t-il
                     seul ? Le standard exige une approbation."
- piege_connu: "La confirmation naît de l'approbation, pas de
   l'exécution. Un client qui n'a pas de circuit de validation des temps
   doit en créer un, ou ses ordres ne se confirment jamais."

---

## CAP-M5.1.1-01 — Affectation par compétence et équipes de service

- noeud: M5.1.1
- question_metier: "comment le bon technicien est-il choisi ?"
- formulations_client: ["compétences du technicien", "habilitations",
                        "affectation par métier", "équipe d'intervention"]

### public
- unite: 49X + FSM Dispatching Board
- disponibilite: **partiel — défaut d'intégration documenté**
- echelon: 3
- release_evaluee: 2608

Côté FSM : tableau de dispatch, compétences visibles au survol du nom,
affectation par glisser-déposer, réaffectation et duplication d'activité
possibles.

**⚠ Limitation explicitement documentée par SAP :** il n'existe
actuellement **aucun mapping des service teams entre S/4 Service et
FSM**. Conséquences :
- si le technicien affecté dans FSM n'appartient pas à la service team
  portée par l'ordre S/4, une **re-détermination d'équipe** est déclenchée
  dans S/4 ;
- si le technicien appartient à **plusieurs** service teams, l'affectation
  automatique **part en erreur, à résoudre manuellement** ;
- recommandation SAP : n'utiliser que des techniciens rattachés à
  exactement une service team.

- source: 49X BPD, §4.4.1, note du step 3
- verdict: **penche-prive** si le client a une organisation d'équipes
  riche et des techniciens polyvalents
- confiance: haute

### pratique
- question_a_poser: "Vos techniciens appartiennent-ils à une seule équipe
                     ou à plusieurs ? Combien sont polyvalents ?"
- piege_connu: "Le mono-équipe est une contrainte du standard, pas un
   choix d'organisation. Dans une entreprise où les techniciens couvrent
   plusieurs spécialités — le cas normal en maintenance — la
   recommandation SAP est inapplicable telle quelle. À chiffrer comme
   un point dur, pas comme un paramétrage."

---

## CAP-M7.4.4-01 — Prérequis référentiel de l'intégration

- noeud: M7.4.4, M7.4.1
- question_metier: "quelles données de base doivent exister des deux côtés ?"
- formulations_client: ["synchronisation des référentiels", "données de
                        base partagées", "mapping des identifiants"]

### public
- disponibilite: natif, mais **avec une exigence forte**
- echelon: 2

**Règle absolue :** pour tout objet de données de base S/4 utilisé, un
objet correspondant portant le **même External Id** doit exister dans FSM.
Sans cela la réplication échoue.

Cas concret documenté : un employé non répliqué comme *People* dans FSM
fait échouer la réplication d'un repair order.

**Mapping de priorité — perte d'information :**

| S/4HANA Cloud | FSM |
|---|---|
| Low | Low |
| Medium | Medium |
| High | High |
| **Very High** | **High** |

Quatre valeurs vers trois. Un aller-retour ne restitue pas la priorité
d'origine.

**Multi-société :** réplication vers plusieurs companies FSM configurable
par règle (sales area pour clients, contrats, ordres, produits de
service ; plant pour pièces détachées). Paramétrage via *Manage Your
Solution* → *Integration with SAP Field Service Management* → *Configure
Multiple Company Replication*, synchronisé vers CPI comme artefact de
value mapping.

- source: 49X BPD, §2.3, §2.3.1, §2.5
- verdict: neutre (le sujet existe partout), mais coût de mise en
           cohérence souvent sous-estimé
- confiance: haute

### pratique
- question_a_poser: "Combien d'entités juridiques et de pays ? Vos
                     identifiants de données de base sont-ils déjà
                     unifiés entre systèmes ?"
- piege_connu: "Deux pièges hérités d'expérience terrain.
   (1) La contrainte External Id transforme la reprise en chantier
   critique : ce n'est pas 'on charge les données', c'est 'on garantit
   une clé commune à vie sur chaque référentiel'.
   (2) L'écrasement de Very High en High est silencieux. Un client qui
   pilote ses urgences sur quatre niveaux perd son niveau le plus haut
   au terrain, sans message d'erreur. À détecter en conception, jamais
   en recette."

---

## CAP-M5.3.1-01 — Pièces réservées et consommation terrain

- noeud: M5.3.1, M5.3.2
- question_metier: "comment le technicien consomme-t-il des pièces ?"
- formulations_client: ["stock camion", "pièces embarquées",
                        "consommation de pièces", "matériel non prévu"]

### public
- unite: 49X (+ 3NI si approvisionnement externe)
- disponibilite: natif
- echelon: 1

Les pièces du poste d'ordre sont répliquées comme **reserved materials**
sur l'activité. Au terrain : consommation d'une pièce réservée
(*Reserved materials > Use*), ou ajout de **matériel non planifié** via
le bouton Create. Validation par le planificateur → confirmation S/4.

Le technicien peut aussi saisir : effort (temps), dépense (avec type et
devise), kilométrage, pièce jointe, checklist, feedback code.

- source: 49X BPD, §4.6.2
- verdict: neutre
- confiance: haute

### pratique
- piege_connu: "Le stock individuel S/4 doit être suffisant pour le
   matériel non planifié, sinon la création de confirmation part en
   erreur — après l'intervention, quand le technicien est reparti.
   Sur le kilométrage, une distance vide ou à zéro produit une erreur
   CPI. Deux causes de rejets récurrents en exploitation."

---

## CAP-M5.2.2-01 — Compte rendu d'exécution et smartforms

- noeud: M5.2.2, M5.2.3
- question_metier: "quelle forme prend le compte rendu, et remonte-t-il
                    dans l'ERP ?"
- formulations_client: ["compte rendu d'intervention", "rapport de
                        service", "signature client", "formulaire terrain",
                        "checklist"]

### public
- disponibilite: natif
- echelon: 2 (la conception des smartforms est un travail à part entière)

Parcours technicien : Travel → Work → saisie → Checkout → *Preview
Report* → **signature à l'écran** → statut *Confirmed and closed*.

**Smartforms** : templates conçus et versionnés dans FSM (catégories,
chapitres, éléments), instances rattachées à une activité. Côté S/4,
deux applications de **consultation seule** : *Smartform Template
Viewer* et *Smartform Instance Viewer*.

Pièces jointes bidirectionnelles : service call ↔ ordre, activité ↔
poste, suppression répliquée également. **Les liens ne peuvent pas être
attachés**, seulement des fichiers.

- source: 49X BPD, §4.4.4, §4.4.5, §4.6.3, §4.10
- verdict: neutre
- confiance: haute

### pratique
- question_a_poser: "Combien de formulaires terrain différents ?
                     Qui les maintiendra — c'est dans FSM, pas dans l'ERP."
- piege_connu: "Les smartforms vivent et se versionnent côté FSM ; S/4
   ne fait que les afficher. Un client qui imagine piloter ses
   formulaires depuis l'ERP se trompe d'outil et de gouvernance."

---

## CAP-M1.2.1-01 — Dépose / pose d'équipement au terrain

- noeud: M1.2.1
- question_metier: "le technicien peut-il déposer et poser un équipement
                    depuis le terrain, avec mise à jour du parc ?"
- formulations_client: ["dépose pose", "remplacement d'équipement",
                        "échange standard sur site", "mise à jour du parc"]

### public
- disponibilite: **absent de 49X**
- echelon: — (à instruire ailleurs)

49X ne porte aucun flux de dépose/pose. L'équipement n'intervient que
comme **Reference Object** de l'ordre ou de l'activité — répliqué,
consultable, marqué principal si plusieurs (premier par ordre
alphabétique). Aucune modification de la structure du parc n'est décrite.

- source: 49X BPD (absence constatée sur l'ensemble du document)
- verdict: **à instruire** — vérifier 7Z2 (ordres de travail), puis
           l'extensibilité FSM. Ne pas conclure sur ce seul document.
- confiance: moyenne (absence dans une source, pas absence prouvée)

### pratique
- piege_connu: "Capacité évidente en maintenance d'ouvrage, absente du
   flux de service commercial. À vérifier tôt : un client qui gère un
   parc installé et remplace des composants sur site attend ce geste
   comme acquis."

---

# Confrontation avec la liste de capacités attendues

| Attendu | Couvert par 49X | Fiche |
|---|---|---|
| Envoi de l'ordre sur tablette | ✅ | M7.4.2-01 |
| Compétences du technicien | ⚠️ partiel, défaut service teams | M5.1.1-01 |
| Synchronisation des référentiels | ✅ sous contrainte External Id | M7.4.4-01 |
| Conso de pièces / outils | ✅ | M5.3.1-01 |
| Mode offline et synchro a posteriori | ⚠️ peu documenté | à instruire |
| Compte rendu d'exécution | ✅ | M5.2.2-01 |
| Suivi des déposes / poses | ❌ absent | M1.2.1-01 |

Sept attendus, quatre couverts nettement, deux partiels, un absent.
**La liste établie avant lecture a tenu** : aucun attendu n'était hors
sujet, et les deux zones de friction pressenties sont exactement celles
qui posent problème.

---

# Défaut produit reconnu par SAP

À la création d'un Service Call dans FSM, une Activity est créée
implicitement — mais **cette activité n'est pas répliquée vers S/4**,
SAP indiquant des développements encore en cours côté FSM (mécanisme de
file d'attente). Conséquence : un service call créé au terrain produit
dans S/4 **un ordre sans poste**.

C'est un défaut ouvert, écrit noir sur blanc dans la documentation de la
release 2608. À poser en question directe à SAP avant tout engagement
sur un scénario où le terrain est à l'origine de la demande.

---

# Reste à instruire sur ce bloc

- **7Z2** — ordres de travail (branche M3), non encore lu
- Mode déconnecté et résolution de conflit (M5.2.4)
- Dépose/pose d'équipement (M1.2.1) — vérifier dans 7Z2
- Volumétrie et rejeu CPI : le BPD décrit le chemin nominal, pas le
  comportement en charge ni la reprise sur erreur. Chercher dans les
  *Instructions de configuration* ou la documentation d'intégration.
