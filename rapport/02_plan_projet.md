# 2. Plan de projet — Transformation du POC en MVP

## 2.1 Objectifs et périmètre de la planification

Le projet Puls-Events vise à transformer un prototype de recherche sémantique fondé sur une architecture RAG (*Retrieval-Augmented Generation*) en un Minimum Viable Product (MVP) capable de répondre aux besoins prioritaires des utilisateurs.

Le POC existant constitue le socle technique du futur produit. Il repose notamment sur Python, LangChain, Mistral AI, FAISS et une interface Streamlit.

La planification distingue deux périmètres :

- **La mission de conception (50 heures)** : analyse des besoins, étude des solutions cloud, architecture cible, macro backlog, estimation des coûts BUILD et OPEX, planification et préparation des livrables.
- **La réalisation future du MVP** : développement des fonctionnalités, intégration, tests, déploiement et validation auprès des utilisateurs.

Le calendrier de réalisation présenté ci-dessous est une **hypothèse prévisionnelle**, à confirmer après estimation détaillée du backlog, disponibilité de l'équipe et arbitrage budgétaire.

**Distinction entre la mission de conception et la réalisation du MVP**

La mission OpenClassrooms est estimée à 50 heures. Elle sera réalisée sur une période optimale selon une organisation personnelle de sept heures par jour et six jours par semaine.

Cette mission consiste à produire les livrables de conception et de gestion du projet : analyse des besoins, comparaison des solutions cloud, architecture cible, macro backlog, estimation des coûts BUILD et OPEX, planification et présentation de soutenance.

Le calendrier de 12 semaines présenté pour la réalisation du MVP constitue une hypothèse de déploiement futur par l'entreprise Puls-Events. Il ne correspond ni à la durée de la mission OpenClassrooms ni à un engagement de développement effectif dans les deux semaines.

## 2.2 Phases de transformation du POC vers le MVP

La transformation est organisée en six phases.

| Phase | Description | Durée indicative |
|---|---|---|
| P1 — Cadrage | Validation des besoins, du périmètre MVP et des indicateurs de réussite | 1 semaine |
| P2 — Architecture et infrastructure | Choix cloud, conception détaillée, environnement de développement et intégration continue | 2 semaines |
| P3 — Développement fonctionnel | Mémoire conversationnelle, personnalisation géographique, recherche Web et collecte des retours | 4 semaines |
| P4 — Observabilité et sécurisation | Monitoring, alertes, sécurité, confidentialité et maîtrise des coûts | 2 semaines |
| P5 — Tests et validation | Tests fonctionnels, intégration, charge, qualité des réponses et recette | 2 semaines |
| P6 — Déploiement pilote | Mise en production contrôlée, suivi des indicateurs et corrections prioritaires | 1 semaine |

**Durée totale indicative : 12 semaines**, sous réserve des ressources affectées, des dépendances et des résultats de validation.

Certaines activités pourront se dérouler en parallèle afin de réduire le délai global.

## 2.3 Jalons, échéancier et livrables

| Jalon | Échéance relative | Livrable attendu | Critère de validation |
|---|---|---|---|
| J1 — Cadrage validé | Fin S1 | Expression des besoins et périmètre MVP | Priorités approuvées |
| J2 — Architecture validée | Fin S3 | Schéma d'architecture et choix techniques | Revue technique favorable |
| J3 — Fonctionnalités intégrées | Fin S7 | Version intégrée du chatbot | Parcours prioritaires opérationnels |
| J4 — Supervision opérationnelle | Fin S9 | Tableaux de bord, logs, alertes et contrôles de sécurité | Tests de supervision et de sécurité concluants |
| J5 — Recette validée | Fin S11 | Rapport de tests et liste des anomalies | Critères d'acceptation atteints |
| J6 — MVP pilote déployé | Fin S12 | MVP accessible aux utilisateurs pilotes | Déploiement et vérifications validés |

Les échéances sont exprimées en semaines relatives au démarrage effectif du projet. Elles ne constituent pas des engagements calendaires définitifs.

## 2.4 Dépendances et responsabilités

### Dépendances principales

La réalisation doit respecter les dépendances suivantes :

1. Le périmètre fonctionnel et les exigences non fonctionnelles doivent être validés avant les choix d'architecture définitifs.
2. L'environnement technique doit être disponible avant l'intégration des fonctionnalités.
3. Les composants conversationnels, géographiques et de recherche Web doivent être intégrés avant les tests de bout en bout.
4. Les mécanismes de supervision doivent être disponibles avant le déploiement pilote.
5. La recette et les contrôles de sécurité doivent être concluants avant l'ouverture aux utilisateurs pilotes.

### Répartition indicative des responsabilités

| Rôle | Responsabilités |
|---|---|
| Responsable produit | Priorisation des besoins et validation fonctionnelle |
| Data Engineer / AI Engineer | Pipeline de données, recherche vectorielle et intégration RAG |
| Développeur backend | API, mémoire conversationnelle et intégrations |
| Ingénieur cloud / DevOps | Infrastructure, déploiement, automatisation et monitoring |
| Responsable sécurité / référent RGPD | Revue des accès, confidentialité et conservation des données |
| Testeur / QA | Tests, recette et suivi des anomalies |

Cette répartition décrit les compétences nécessaires. Elle ne présuppose pas que Puls-Events dispose d'une personne distincte pour chaque rôle.

## 2.5 Risques et mesures de mitigation

| Risque | Impact potentiel | Mesure envisagée |
|---|---|---|
| Dépassement des coûts des API LLM | Budget non maîtrisé | Quotas, suivi de consommation, cache et limites par utilisateur |
| Indisponibilité d'une API externe | Réponses incomplètes ou service dégradé | Gestion des erreurs, délais d'attente, mécanismes de repli |
| Données événementielles obsolètes | Recommandations incorrectes | Actualisation contrôlée et indication des sources |
| Temps de réponse élevés | Dégradation de l'expérience utilisateur | Mesure des latences, optimisation des requêtes et tests de charge |
| Exposition de données personnelles | Risque de non-conformité | Minimisation, règles de conservation, contrôles d'accès |
| Retard d'intégration | Décalage du calendrier | Livraison incrémentale, revues régulières et marges de sécurité |
| Qualité insuffisante des recommandations | Insatisfaction des utilisateurs | Jeu d'évaluation, tests de pertinence et retours utilisateurs |

## 2.6 Critères de validation du MVP

La validation reposera sur plusieurs catégories d'indicateurs :

**Fonctionnalité :** les quatre capacités prioritaires doivent être opérationnelles : mémoire conversationnelle, personnalisation géographique, recherche Web actualisée et suivi de la satisfaction.

**Performance :** les temps de réponse doivent respecter des seuils définis pendant le dimensionnement.

**Qualité :** les réponses doivent être évaluées sur un jeu représentatif de questions, notamment pour la pertinence, la contextualisation et la fraîcheur des informations.

**Sécurité :** les accès, secrets techniques et données personnelles doivent faire l'objet de contrôles adaptés.

**Exploitation :** les métriques, journaux et alertes doivent permettre de diagnostiquer les incidents et de suivre les coûts.

**Acceptation métier :** les responsables du produit doivent valider les parcours utilisateurs prioritaires avant le lancement pilote.

Les seuils chiffrés et les volumes de charge seront proposés dans les documents de dimensionnement et de coûts, puis soumis à validation.

## 2.7 Organisation de la mission de conception — 50 heures

La mission OpenClassrooms est distincte des 12 semaines prévisionnelles de réalisation du MVP.

| Activité | Charge estimée |
|---|---:|
| Analyse et synthèse des besoins | 5 h |
| Veille technique et comparaison cloud | 8 h |
| Conception de l'architecture cible | 10 h |
| Construction du macro backlog | 5 h |
| Estimation BUILD et OPEX | 8 h |
| Planification et jalons | 5 h |
| Rédaction et consolidation du rapport | 5 h |
| Préparation de la soutenance | 4 h |
| **Total** | **50 h** |

Cette répartition est indicative et pourra être ajustée en fonction des difficultés rencontrées.

## 2.8 Synthèse du plan de projet

La démarche retenue privilégie une transformation progressive du POC vers un MVP, avec des jalons de validation et une livraison pilote contrôlée.

Le calendrier prévisionnel de 12 semaines permet d'organiser les travaux de développement, de supervision, de sécurisation et de recette. Il devra être consolidé à partir du macro backlog et des estimations de charge.

La mission de conception de 50 heures fournit les éléments nécessaires pour éclairer les décisions techniques, financières et organisationnelles avant le lancement effectif du développement.