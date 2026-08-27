# CAP-M8.1.5-01 — Couverture du régime de travail par édition

- noeud: M8.1.5
- question_metier: "peut-on gérer permis, consignation et condamnation
                    dans l'ERP, ou faut-il un tiers ?"
- formulations_client: ["permis de travail", "régime de travail",
                        "consignation", "permit to work", "LOTO",
                        "lockout tagout", "isolation management",
                        "autorisation de travail", "habilitation chantier",
                        "plan de prévention"]
- enjeu: structurant. Décide l'édition dès que le client est en
         industrie à risque.

## public

- unite: scope item 7Z4 (Permit to Work)
- disponibilite: partiel
- echelon: 2
- pays_disponibles: France incluse (vérifié Process Navigator, 24/08/2026).
                    Livraison initiale Allemagne + États-Unis en 2602,
                    étendue depuis.

### Ce que 7Z4 couvre effectivement

Flux relevé sur le process flow officiel :

1. Déclenchement depuis un ordre de maintenance en statut **CRTD ou REL**
   (types 4HH réactive, 4HI proactive, 4WM opérationnelle et frais
   généraux, 4VT amélioration)
2. Initiation du permis par le Maintenance Planner
3. Saisie des informations du permis
4. Passage en « ready for issue »
5. **Approbation optionnelle** (branche conditionnelle) — soumission,
   revue par le Plant Manager, approuvé ou rejeté
6. Remise du permis au technicien
7. Inspection du site, mise en place des précautions de sécurité
8. Information de l'émetteur à l'achèvement des travaux
9. Retour et clôture du permis

Rôles portés : Plant Manager, Maintenance Planner, Maintenance
Supervisor, Maintenance Technician.

Un second document livre le **modèle de permis** — la bibliothèque de
gabarits réutilisables (nœud M8.2.4, confirmé existant).

### Ce que 7Z4 ne couvre pas

Absent du flux officiel, donc hors standard public :

- **M8.4 — condamnation physique.** Aucune étape de pose ou dépose
  d'étiquette, de verrouillage, de vérification d'absence de tension.
  « Ensure safety precautions at work site » est une étape déclarative
  du technicien, pas une procédure d'isolement tracée.
- **M8.1.3 / M8.1.4 — listes opérationnelles et listes d'étiquettes.**
  Pas d'objet correspondant.
- **M8.5 — travaux simultanés et interférences.** Aucune détection de
  conflit entre permis portant sur un même périmètre.
- **M8.2.2 / M8.2.3 — points de coupure et séquence de manœuvres.**
  Le permis porte de l'information, pas une séquence exécutable.
- **M8.6 — déconsignation et essais de requalification.** La clôture est
  administrative.

### Contrainte structurelle

**Le permis est piloté par l'ordre.** Il naît d'un ordre de maintenance
en CRTD ou REL. Un client qui délivre des permis indépendamment d'un
ordre — typiquement à un prestataire extérieur intervenant sans OT dans
le système — n'entre pas dans le standard.

- source: Process Navigator, process flow 7Z4 (PDF, dossier Drive) ;
          blog release Asset Management 2602 ; SAP Community
- release_evaluee: 2602
- evalue_le: 2026-08-26

## private

- unite: composant classique WCM (PM/EHS)
- disponibilite: natif
- echelon: 1
- reserve: "Licence additionnelle. Modèle simple ou étendu — choix
           structurant, difficilement réversible. Couvre permis,
           procédures d'isolation, approbations multi-niveaux, listes
           opérationnelles, étiquettes et étiquettes d'essai, application
           mobile LOTO."
- source: SAP Community
- release_evaluee: à confirmer
- evalue_le: 2026-08-23

## fsa

- disponibilite: a-verifier
- reserve: "M8.9 (mobilité du régime de travail) non instruit. Vérifier
           si le permis est consultable et signable depuis FSA, et quelle
           valeur probante en mode déconnecté."

## verdict

- edition: penche-prive
- justification: 7Z4 couvre le permis et son cycle d'approbation ; la
                 chaîne de consignation physique et la gestion des
                 interférences restent hors périmètre public. Devient
                 `bloquant-public` dès que le client exige la chaîne
                 complète.
- confiance: haute (couverture fonctionnelle établie sur process flow
             officiel ; disponibilité France vérifiée)

## pratique

- question_a_poser: "Vos interventions exigent-elles un régime formel
                     avec approbation SEULEMENT, ou aussi une
                     condamnation physique tracée ? Délivrez-vous des
                     permis sans ordre de travail associé — à des
                     prestataires par exemple ? Combien de chantiers
                     simultanés sur un même périmètre ? Qu'exige votre
                     autorité de contrôle comme preuve ?"

- piege_connu: "Deux pièges distincts.
   (1) Le sujet ne remonte presque jamais dans un cahier des charges —
   il est porté par la sécurité, pas par la maintenance, et les deux ne
   rédigent pas ensemble. Il surgit en conception détaillée, quand
   l'édition est déjà contractualisée.
   (2) « Nous avons un processus de permis de travail » ne dit rien.
   La question décisive n'est pas l'existence du permis mais la
   condamnation physique et les interférences. Un client peut décrire un
   processus qui paraît couvert par 7Z4 et ne pas l'être du tout."

- liens: [depend-de: CAP-M7.2-*, impacte: CAP-M3.3.1-*,
          precise: CAP-M8.2.4-01]

## à instruire ensuite

- CAP-M8.2.4-01 — bibliothèque de modèles de permis (document 7Z4-02
  déjà disponible)
- CAP-M8.9-01 — consultation et signature du permis en mobilité
- Le caractère optionnel de l'approbation (branche conditionnelle du
  flux) : paramétrable ou codé ? Détermine si un client peut imposer une
  approbation systématique. À chercher dans le test script.
