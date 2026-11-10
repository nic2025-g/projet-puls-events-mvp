# 6. Bilan du passage du POC au MVP

## 6.1. Synthèse de la mission

La mission Puls-Events avait pour objectif de préparer la transformation d'un Proof of Concept (POC) de recherche sémantique en un Minimum Viable Product (MVP) destiné à la découverte et à la recommandation d'événements culturels.

Le POC existant reposait sur Python, LangChain, Mistral AI et FAISS. Il avait démontré la faisabilité technique d'un moteur de recherche sémantique fondé sur une architecture RAG (*Retrieval-Augmented Generation*).

La mission actuelle, estimée à 50 heures, a porté principalement sur la conception technique, la planification, l'analyse des besoins et l'évaluation économique de la future solution.

Elle ne constitue pas une mise en production effective du MVP.

## 6.2. Travaux réalisés

Les travaux de conception ont permis de produire les éléments suivants :

| Livrable | Résultat |
|---|---|
| Analyse des besoins | Identification des utilisateurs, des objectifs métiers et des exigences fonctionnelles et non fonctionnelles |
| Plan de projet | Définition de six phases, de six jalons et d'un calendrier prévisionnel de 12 semaines |
| Macro backlog | Priorisation des fonctionnalités et estimation d'une charge totale de 72 journées-homme |
| Comparaison cloud | Évaluation d'AWS, Azure et Google Cloud à l'aide d'une méthode multicritère AHP |
| Architecture technique | Proposition d'une architecture modulaire RAG reposant notamment sur Azure, PostgreSQL/pgvector et Mistral AI |
| Estimation financière | Élaboration d'un budget BUILD et de scénarios prévisionnels OPEX |

Ces livrables constituent une base de décision pour organiser le développement futur du MVP.

## 6.3. Décisions techniques et méthodologiques

### Conservation des acquis du POC

Le choix a été fait de conserver les technologies et les principes du POC lorsqu'ils restent adaptés aux besoins du MVP, notamment Python, LangChain et Mistral AI.

Cette approche vise à limiter les développements inutiles et à capitaliser sur les travaux précédemment réalisés.

### Évolution du stockage vectoriel

Le POC utilisait FAISS pour la recherche vectorielle.

Pour le MVP, PostgreSQL avec l'extension pgvector a été proposé afin de rapprocher les données structurées, les informations événementielles et les vecteurs dans une solution persistante.

Ce choix devra être validé par des essais de pertinence, de performance et de montée en charge.

### Sélection provisoire de Microsoft Azure

La comparaison multicritère AHP a conduit à recommander provisoirement Microsoft Azure, avec un score de 83,49/100, devant AWS (81,85/100) et Google Cloud (77,84/100).

Cette décision repose sur les critères pondérés de coût, de compatibilité RAG, de scalabilité, de sécurité, de facilité de déploiement et d'observabilité.

L'écart relativement faible entre Azure et AWS invite à conserver une vigilance sur les hypothèses et les coûts réels.

### Planification progressive

La réalisation future du MVP a été organisée en six phases sur 12 semaines, avec des jalons de validation.

Le macro backlog permet de distinguer les fonctionnalités indispensables des évolutions secondaires et de préparer l'affectation des ressources.

## 6.4. Difficultés et points de vigilance

| Difficulté ou risque | Réponse apportée ou prévue |
|---|---|
| Comparaison de services cloud aux modèles tarifaires différents | Définition d'hypothèses communes et conservation des justificatifs |
| Incertitude sur les coûts d'exploitation | Construction de scénarios et documentation des limites |
| Passage de FAISS à une solution persistante | Proposition de PostgreSQL/pgvector, à valider par des tests |
| Dépendance aux API externes | Prévision de quotas, délais d'attente, mécanismes de repli et supervision |
| Confidentialité des conversations | Définition de principes de minimisation, de conservation limitée et de contrôle d'accès |
| Risque de dépassement du calendrier | Priorisation du backlog, jalons et livraison progressive |

Les mesures décrites correspondent à des décisions de conception ou à des actions prévues. Leur efficacité devra être vérifiée pendant la réalisation du MVP.

## 6.5. Bilan financier prévisionnel

Le macro backlog estime la réalisation du MVP à 72 journées-homme.

Avec un taux journalier moyen hypothétique de 500 € HT, le coût direct de développement est estimé à 36 000 € HT.

Une provision de 15 % pour les imprévus porte le budget BUILD prévisionnel à **41 400 € HT**.

Les dépenses d'exploitation OPEX ont été étudiées selon trois scénarios de charge. Elles incluent notamment l'hébergement applicatif, PostgreSQL, les appels aux modèles d'IA et les services d'exploitation.

Ces estimations sont indicatives et doivent être actualisées selon les tarifs fournisseurs, les configurations retenues et les volumes d'utilisation réels.

## 6.6. Limites du travail réalisé

À ce stade, les livrables concernent principalement la conception et la gestion du projet.

Les éléments suivants restent à réaliser ou à valider :

- Développement et intégration des nouvelles fonctionnalités du MVP.
- Migration et tests du stockage vectoriel vers PostgreSQL/pgvector.
- Déploiement effectif sur une infrastructure cloud.
- Tests de charge, de disponibilité et de sécurité.
- Évaluation quantitative de la pertinence des recommandations.
- Validation des hypothèses financières avec des mesures réelles.
- Recette fonctionnelle auprès d'utilisateurs pilotes.

Il est donc important de distinguer les résultats du POC existant des performances attendues du futur MVP.

## 6.7. Prochaines étapes

La suite du projet pourrait s'organiser autour des actions suivantes :

1. Faire valider le périmètre MVP, l'architecture cible et le budget prévisionnel.
2. Détailler les user stories prioritaires et leurs critères d'acceptation.
3. Préparer l'environnement de développement et la chaîne CI/CD.
4. Implémenter progressivement la mémoire conversationnelle, la personnalisation géographique et la recherche actualisée.
5. Mettre en place le monitoring, les contrôles de sécurité et la collecte de satisfaction.
6. Réaliser les tests de performance, de pertinence et de sécurité.
7. Déployer une version pilote et analyser les retours utilisateurs.

## 6.8. Conclusion du bilan

La mission a permis de structurer le passage du POC Puls-Events vers un MVP à travers une démarche de conception, de planification et d'aide à la décision.

Les principaux résultats sont la formalisation des besoins, la priorisation du backlog, la définition d'une architecture cible, la comparaison argumentée des fournisseurs cloud et l'estimation des coûts.

Le projet dispose ainsi d'un cadre prévisionnel pour engager la réalisation du MVP, sous réserve de validation des choix techniques, des hypothèses financières et des critères de performance.