# ARBORESCENCE.md — Référentiel Maintenance & Service

Squelette de domaine, indépendant de tout client. Une fiche capacité
s'accroche à exactement un nœud feuille. Un besoin client ne rentre
jamais dans l'arbre — il se *rapproche* d'un nœud.

Convention de code : `M1.2.3`. Le code est stable à vie. On peut
renommer un libellé, jamais réattribuer un code.

---

## M1 — Référentiel technique (l'objet à maintenir)

```
M1.1  Structure fonctionnelle
      M1.1.1  Postes techniques et hiérarchie
      M1.1.2  Structuration alternative / vues multiples
      M1.1.3  Reprise et masques de codification
M1.2  Équipements
      M1.2.1  Cycle de vie (création, installation, démontage, mise au rebut)
      M1.2.2  Historique d'implantation
      M1.2.3  Hiérarchie équipement / sous-équipement
M1.3  Identification unitaire
      M1.3.1  Sérialisation
      M1.3.2  Gestion par lot
      M1.3.3  Articulation avec le stock
M1.4  Caractéristiques et classification
      M1.4.1  Classes et caractéristiques
      M1.4.2  Valeurs autorisées, dépendances, obligatoire conditionnel
      M1.4.3  Recherche et sélection par caractéristique
M1.5  Points de mesure et compteurs
      M1.5.1  Relevés et documents de mesure
      M1.5.2  Compteurs et déclenchement de maintenance
M1.6  Nomenclatures de maintenance
M1.7  Documentation technique attachée (plans, notices, DOE)
M1.8  Parc client vs parc interne
      M1.8.1  Équipement chez le client (base installée)
      M1.8.2  Propriété, responsabilité, périmètre contractuel
```

## M2 — Maintenance préventive

```
M2.1  Gammes de maintenance
      M2.1.1  Opérations, durées, qualifications
      M2.1.2  Gammes génériques vs spécifiques objet
M2.2  Stratégies et cycles
      M2.2.1  Périodicité calendaire
      M2.2.2  Périodicité sur compteur / usage
      M2.2.3  Stratégies multiples et hiérarchisées
M2.3  Plans d'entretien
      M2.3.1  Création et affectation en masse
      M2.3.2  Ordonnancement, décalage, appel
      M2.3.3  Reprise de l'historique d'échéance
M2.4  Réglementaire et métrologie
      M2.4.1  Contrôles obligatoires et preuve
      M2.4.2  Vérification périodique d'équipement
M2.5  Maintenance conditionnelle / prédictive
      M2.5.1  Seuils et alertes sur mesure
      M2.5.2  Entrée de données capteur / IoT
```

## M3 — Maintenance corrective

```
M3.1  Signalement
      M3.1.1  Avis / demande d'intervention
      M3.1.2  Canaux d'entrée (terrain, client, automate)
      M3.1.3  Qualification et priorisation
M3.2  Codification défaillance
      M3.2.1  Catalogues mode / cause / remède
      M3.2.2  Analyse de défaillance et exploitation
M3.3  Ordre de travail
      M3.3.1  Typologie et cycle de statuts
      M3.3.2  Opérations, composants, moyens
      M3.3.3  → voir M8 (consignation et régime de travail)
M3.4  Exécution et retour
      M3.4.1  Confirmation temps et avancement
      M3.4.2  Compte rendu technique
      M3.4.3  Clôture technique et administrative
M3.5  Coûts
      M3.5.1  Imputation et valorisation
      M3.5.2  Règlement / settlement
      M3.5.3  Budget et suivi d'écart
```

## M4 — Service client (dimension commerciale)

```
M4.1  Contrats de service
      M4.1.1  Typologie et niveaux de service
      M4.1.2  Cycle de vie, reconduction, révision de prix
      M4.1.3  Couverture (objets, prestations, exclusions)
M4.2  Garantie
      M4.2.1  Origine et date de départ
      M4.2.2  Garantie constructeur vs garantie vendue
      M4.2.3  Contrôle automatique à l'intervention
      M4.2.4  Réclamation de garantie et refacturation fournisseur
M4.3  Demande de service
      M4.3.1  Réception et ticketing
      M4.3.2  Engagements de délai (SLA) et escalade
M4.4  Ordre de service et devis
      M4.4.1  Devis d'intervention
      M4.4.2  Ordre de service, ressources, pièces
M4.5  Réparation en atelier
      M4.5.1  Retour, diagnostic, décision
      M4.5.2  Réparation, échange standard, rebut
M4.6  Facturation de service
      M4.6.1  Régie, forfait, contrat
      M4.6.2  Périodique et à l'acte
      M4.6.3  Refacturation pièces et déplacement
M4.7  Satisfaction et réclamation
```

## M5 — Exécution terrain

```
M5.1  Planification et affectation
      M5.1.1  Charge, capacité, compétences
      M5.1.2  Planning graphique et arbitrage
      M5.1.3  Optimisation de tournée et géolocalisation
      M5.1.4  Urgence et réaffectation en cours de journée
M5.2  Mobilité technicien
      M5.2.1  Réception et synchronisation des interventions
      M5.2.2  Saisie terrain (constat, temps, pièces)
      M5.2.3  Pièces jointes (photo, schéma, signature)
      M5.2.4  Mode déconnecté et résolution de conflit
      M5.2.5  Personnalisation d'écran mobile
M5.3  Stock embarqué
      M5.3.1  Stock camion et visibilité temps réel
      M5.3.2  Consommation, réappro, inventaire
M5.4  Sous-traitance
      M5.4.1  Affectation d'un intervenant externe
      M5.4.2  Retour d'intervention et contrôle
      M5.4.3  Achat de prestation et rapprochement
M5.5  Astreinte et travail posté
```

## M6 — Pièces et logistique de maintenance

```
M6.1  Article de maintenance et criticité
M6.2  Politique de stock
      M6.2.1  Stock mini, sécurité, calcul de besoin
      M6.2.2  Multi-magasin, multi-emplacement
M6.3  États de pièce (neuf, reconditionné, réparé, HS, sous garantie)
M6.4  Réservation et sortie sur ordre
M6.5  Approvisionnement lié à l'intervention
M6.6  Retour, échange standard, consigne
M6.7  Expédition et suivi transporteur
```

## M7 — Couches transverses

```
M7.1  Organisation et données de base
      M7.1.1  Structure organisationnelle (division, poste de travail)
      M7.1.2  Référentiel RH et qualification
      M7.1.3  Partenaires et rôles
M7.2  Habilitations
      M7.2.1  Modèle de rôles et dérivation territoriale
      M7.2.2  Restriction par type d'objet et par statut
M7.3  Extensibilité
      M7.3.1  Champ personnalisé
      M7.3.2  Logique personnalisée
      M7.3.3  Adaptation d'écran et de formulaire
      M7.3.4  Développement côte-à-côte
M7.4  Intégration
      M7.4.1  API et événements sortants
      M7.4.2  Intégration ERP ↔ exécution terrain
      M7.4.3  Interfaces tierces (MES, PLM/CAO, GTB, cartographie)
      M7.4.4  Reprise et chargement de masse
M7.5  Restitution
      M7.5.1  Analytique embarquée
      M7.5.2  Extraction et datawarehouse
      M7.5.3  Indicateurs de performance maintenance
M7.6  Cadre de déploiement
      M7.6.1  Multi-société, multi-pays, multi-devise
      M7.6.2  Localisation et langue
      M7.6.3  Cadence de release et politique d'upgrade
```

## M8 — Consignation et régime de travail (Work Clearance Management)

Couche de gouvernance de sécurité qui enveloppe l'exécution. Parenté
revendiquée avec la qualité : même logique de preuve opposable, même
exigence de traçabilité de l'approbation, même conséquence en cas
d'écart. Mais l'objet gouverné est l'intervention, pas le produit.

```
M8.1  Modèle d'objet WCM
      M8.1.1  Demande de régime de travail (Work Clearance Application)
      M8.1.2  Document / certificat de consignation (Work Clearance Document)
      M8.1.3  Liste opérationnelle
      M8.1.4  Liste d'étiquettes et étiquettes d'essai
      M8.1.5  Modèle simple vs modèle étendu
M8.2  Préparation de la consignation
      M8.2.1  Identification des énergies et des risques
      M8.2.2  Détermination des points de coupure
      M8.2.3  Manœuvres et séquence d'exécution
      M8.2.4  Bibliothèque de consignations types
M8.3  Cycle d'approbation
      M8.3.1  Niveaux de permis et rôles habilitants
      M8.3.2  Approbation, refus, révocation
      M8.3.3  Réseau de statuts et blocage de l'ordre de travail
M8.4  Condamnation physique (LOTO)
      M8.4.1  Pose et dépose d'étiquettes
      M8.4.2  Verrouillage, cadenassage, clé unique
      M8.4.3  Vérification d'absence de tension / de pression
M8.5  Travaux simultanés et interférences
      M8.5.1  Chantiers parallèles sur un même périmètre
      M8.5.2  Détection de conflit de consignation
      M8.5.3  Régimes emboîtés
M8.6  Déconsignation et remise en service
      M8.6.1  Levée des mesures, essais de requalification
      M8.6.2  Retour à l'exploitant
M8.7  Preuve et conformité
      M8.7.1  Archivage opposable et durée de conservation
      M8.7.2  Signature et non-répudiation
      M8.7.3  Piste d'audit et présentation à l'inspection
M8.8  Spécificités haut risque (nucléaire, chimie, réseaux)
      M8.8.1  Radioprotection et régime d'accès en zone
      M8.8.2  Arrêt de tranche / grand arrêt — volumétrie et pics
      M8.8.3  Sous-traitance en zone réglementée
      M8.8.4  Habilitation et validité des titres du personnel
M8.9  Mobilité du régime de travail
      M8.9.1  Consultation du permis au terrain
      M8.9.2  Signature et levée au poste de travail
      M8.9.3  Mode déconnecté et question de la valeur probante
```

Renvois : M3.3 (ordre de travail), M5.4 (sous-traitance), M7.2
(habilitations), M2.4 (réglementaire).

Renvois : M3.3 (ordre de travail), M5.4 (sous-traitance), M7.2
(habilitations), M2.4 (réglementaire).

---

# Ce qu'on attend dans une fiche accrochée à un nœud

```
## CAP-M4.2.1-01 — Date de départ de garantie à la mise en service
- noeud: M4.2.1
- question_metier: "à partir de quand court la garantie, et qui le décide ?"
- formulations_client: ["départ garantie mise en route",
                        "garantie à la livraison", "warranty start date"]
- enjeu: une erreur d'origine décale toute la couverture et fausse
         la refacturation. Sujet systématiquement sous-estimé en cadrage.

### public
- unite: scope item <ID>
- disponibilite: natif | config | ext-key-user | btp | absent
- echelon: 1..4
- reserve: "…"
- source: <document + section>
- release_evaluee: <ex. 2608>
- evalue_le: <date>

### private
- unite: composant classique <transaction/module> | scope item <ID>
- disponibilite: natif | config | ext-key-user | btp | modif-core | absent
- echelon: 1..5
- reserve: "…"
- source: <document + section>
- release_evaluee: <ex. 2023 FPS02>
- evalue_le: <date>

### fsa
- disponibilite: natif | config | absent | hors-sujet
- reserve: "…"
- source: …
- release_evaluee: <ex. 2608>

### verdict
- edition: neutre | penche-prive | bloquant-public | bloquant-partout
- justification: une phrase
- confiance: haute | moyenne | a-verifier

### pratique
- question_a_poser: "sur quel événement le client déclenche-t-il
                     réellement la garantie ?"
- piege_connu: "…"
- liens: [depend-de: CAP-M1.8.1-01]
```

Trois champs valent plus que le reste et n'existent dans aucune doc SAP :

- **`formulations_client`** — c'est l'index d'entrée réel. Un client ne
  dit jamais « M4.2.1 ». Sans ce champ le référentiel est illisible en
  situation.
- **`question_a_poser`** — ce que tu demandes en atelier quand ce nœud
  s'active. C'est la transformation de connaissance en geste de
  consultant.
- **`piege_connu`** — ce que tu as vu rater. Irremplaçable, non
  documenté, et c'est là que ton expérience GOTAM devient de la valeur
  transférable.

---


---

# Rattachement des scope items Public Edition

⚠ **Statut de cette section.** Les identifiants marqués `[confirmé]` sont
sourcés (SAP Learning, SAP Community, blogs release SAP). Ceux marqués
`[à récupérer]` n'ont **pas** été vérifiés — ne pas les inventer, aller
les chercher dans **SAP Signavio Process Navigator**
(`https://me.sap.com/processnavigator`, onglet Solution Process, filtrer
LoB *Asset Management* puis *Service*). Seule source qui fait foi, et
elle bouge à chaque release.

## Asset Management — couvre M1, M2, M3, une partie de M5 et M8

| Scope item | Libellé | Nœuds |
|---|---|---|
| **4HH** `[confirmé]` | Reactive Maintenance | M3.1, M3.2, M3.3, M3.4 |
| **4HI** `[confirmé]` | Proactive Maintenance | M2.1, M2.2, M2.3 |
| **4VT** `[confirmé]` | Improvement Maintenance | M3.3.1 |
| **4WM** `[confirmé]` | Operational and Overhead Maintenance | M3.3.1 |
| **43R** `[confirmé]` | Maintenance Resource Scheduling | M5.1.1, M5.1.2 |
| **4RV** `[confirmé]` | SAP Maintenance Assistant | M5.2 |
| **BF7** `[confirmé]` | Period-End Closing Maintenance Orders | M3.5.2 |
| **7Z4** `[confirmé]` | Permit to Work | M8.3, partiellement M8.1 |

**Dépréciés en Public Edition** — ne plus proposer, mais à reconnaître
dans un existant client : **BH1** Corrective Maintenance, **BH2**
Emergency Maintenance, **BJ2** Preventive Maintenance, **3YE**
Integration with Asset Central Foundation. Successeurs : 4HH et 4HI.
Côté Private Edition ils restent activables sans dépréciation annoncée —
divergence public/privé à noter en soi.

**Le modèle en phases.** 4HH et 4HI portent le *Phase Model* (initiation
et screening, planification et approbation, préparation et
ordonnancement, exécution, clôture). Ce n'est pas un détail de
paramétrage : c'est un cycle de vie imposé qui remplace le pilotage par
statuts système des anciens scope items. Un client habitué au
fonctionnement classique doit s'y conformer. Nœud M3.3.1, verdict
probable `penche-prive` pour qui le refuse.

## Service — couvre M4, une partie de M6

| Scope item | Libellé | Nœuds |
|---|---|---|
| **3MO** `[confirmé]` | Service Contract Management | M4.1 |
| **6GU** `[confirmé]` | Service contracts, produits configurables | M4.1.3 |
| **3NI** `[confirmé]` | Procurement for Service Management | M6.5 |
| `[à récupérer]` | Service Order Management | M4.4 |
| `[à récupérer]` | In-House Repair | M4.5 |
| `[à récupérer]` | Intégration SAP FSA / FSM | M5.2, M7.4.2 |
| `[à récupérer]` | Recurring services | M4.1.2, M4.6.2 |
| `[à récupérer]` | Warranty claim (client et fournisseur) | M4.2.4 |
| `[à récupérer]` | Service analytics / management overview | M7.5.3 |

SAP distingue trois familles de processus de service : réparation en
atelier, service terrain, services récurrents. Reprendre cette
tripartition comme axe secondaire sous M4 — c'est le vocabulaire que le
client entendra en démo.

## Nœuds sans scope item dédié

Relèvent du socle, du paramétrage ou de l'extensibilité. Ce sont **les
plus discriminants** pour l'arbitrage public/privé, donc à instruire en
priorité :

M1.4.2 (obligatoire conditionnel) · M7.2 (habilitations) · M7.3.1 à
M7.3.4 (extensibilité) · M7.4.3 (interfaces tierces) · M7.4.4 (reprise) ·
M7.6.1 et M7.6.2 (multi-pays, localisation) · M7.6.3 (cadence de
release) · M5.2.4 (mode déconnecté) · M5.2.5 (personnalisation d'écran
mobile).

---

# Fiche exemple M8 — et pourquoi elle a changé en une heure

```
## CAP-M8.1.5-01 — Couverture du régime de travail par édition
- noeud: M8.1.5
- question_metier: "peut-on gérer permis, consignation et condamnation
                    dans l'ERP, ou faut-il un tiers ?"
- formulations_client: ["permis de travail", "régime de travail",
                        "consignation", "permit to work", "LOTO",
                        "lockout tagout", "isolation management",
                        "autorisation de travail"]
- enjeu: structurant. Décide l'édition dès que le client est en
         industrie à risque.

### public
- unite: scope item 7Z4 (Permit to Work)
- disponibilite: partiel
- echelon: 2
- pays_disponibles: Allemagne, États-Unis à l'introduction ; autres pays
                    dans les mises à jour ultérieures
- reserve: "7Z4 introduit en 2602. Processus formel d'autorisation pour
           travaux à haut risque, pensé pour la collaboration
           maintenance / exploitation / sécurité. NE COUVRE PAS le
           périmètre WCM complet : SAP a indiqué ne pas envisager de
           porter la solution WCM entière, LOTO inclus, en Public
           Edition. Restent hors standard : M8.4 (condamnation
           physique), M8.5 (travaux simultanés et interférences),
           M8.1.3 et M8.1.4 (listes opérationnelles et d'étiquettes)."
- source: SAP Community, blog release Asset Management 2602 ;
          SAP Learning, cursus Asset Management Public Edition
- release_evaluee: 2602
- evalue_le: 2026-08-23

### private
- unite: composant classique WCM (PM/EHS)
- disponibilite: natif
- echelon: 1
- reserve: "Licence additionnelle. Modèle simple ou étendu — choix
           structurant, difficilement réversible. Couvre permis,
           procédures d'isolation, approbations multi-niveaux, listes
           opérationnelles, étiquettes et étiquettes d'essai, et une
           application mobile LOTO."
- source: SAP Community
- release_evaluee: à confirmer
- evalue_le: 2026-08-23

### fsa
- disponibilite: a-verifier
- reserve: "M8.9 entier non instruit."

### verdict
- edition: penche-prive
- justification: le permis simple existe désormais en public (7Z4), mais
                 la consignation physique et la gestion des interférences
                 restent hors périmètre public — donc bloquant-public dès
                 que le client exige la chaîne complète.
- confiance: moyenne

### pratique
- question_a_poser: "Vos interventions exigent-elles un régime formel
                     avec approbation ET condamnation physique ? Combien
                     de chantiers simultanés sur un même périmètre ?
                     Qu'exige votre autorité de contrôle comme preuve ?"
- piege_connu: "Le sujet ne remonte presque jamais dans un cahier des
               charges — il est porté par la sécurité, pas par la
               maintenance, et les deux ne rédigent pas ensemble. Il
               surgit en conception détaillée, quand l'édition est déjà
               contractualisée. Question de premier atelier."
- liens: [depend-de: CAP-M7.2-*, impacte: CAP-M3.3.1-*]
```

**Ce que cette fiche démontre.** Une première évaluation, fondée sur une
position SAP de fin 2023, concluait `bloquant-public` sans nuance. Une
vérification a fait apparaître 7Z4, livré en 2602. Le verdict passe à
`penche-prive`, avec une réserve pays qui, pour un client français, est
plus bloquante que la question fonctionnelle elle-même.

Trois enseignements pour la méthode :

1. Le champ `confiance` n'est pas décoratif — c'est lui qui déclenche la
   vérification qui évite l'erreur en clientèle.
2. **`pays_disponibles` manque au schéma.** À ajouter comme champ à part
   entière du bloc `public` : contrainte fréquente des livraisons Public
   Edition, invisible autrement.
3. Une réponse de forum, même émanant de SAP, périme. Ne jamais faire foi
   sans confrontation à la release courante.

# Points à contester

Cinq endroits où j'ai tranché arbitrairement. Ce sont les bons sujets
de désaccord :

1. **M3 et M4 séparés.** J'ai séparé corrective interne (M3) et service
   client commercial (M4). SAP les rapproche fortement. Argument
   inverse : un même processus d'exécution, deux cadres de facturation.
2. **M5 comme branche autonome.** L'exécution terrain pourrait être
   éclatée dans M3 et M4. Je l'isole parce que c'est le périmètre FSA,
   et donc la frontière produit — utile pour raisonner édition.
3. **M6 dans le référentiel.** C'est du MM, pas du PM. Je le garde
   parce que la moitié des points durs de maintenance sont des points
   durs de pièces.
4. **M7.3 Extensibilité comme nœud.** Discutable : ce n'est pas un
   processus métier. Mais c'est *le* déterminant public vs privé, donc
   il mérite des fiches propres.
5. **Pas de branche « projet / travaux neufs ».** Volontaire : ça
   dérive vers PS et la gestion d'ouvrage. À rouvrir si tu vises des
   clients type utilities.

6. **M8.9 dans M8 plutôt que sous M5.2** — la valeur probante du permis
   hors ligne appartient aux deux. Non tranché.
7. **Pas de branche « grand arrêt »** — traité comme note de volumétrie
   en M8.8.2. Si le nucléaire devient une cible sérieuse, l'arrêt de
   tranche mérite son propre arbre.

Et une absence assumée : aucune branche « client ». Les corpus clients
restent dehors, en jeu d'essai.
