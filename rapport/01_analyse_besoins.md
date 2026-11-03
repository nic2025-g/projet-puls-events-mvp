# Projet Puls-Events — Du POC au MVP

## Introduction — Contexte et objectif du projet

Puls-Events est une entreprise proposant une plateforme Web permettant aux utilisateurs de découvrir et de suivre des événements culturels. Les informations sont collectées auprès de différentes sources, notamment OpenAgenda, puis exploitées pour proposer des recommandations personnalisées selon les préférences des utilisateurs.

Dans le cadre d'un précédent projet, un Proof of Concept (POC) a été réalisé afin de démontrer la faisabilité d'un moteur de recherche sémantique reposant sur une architecture RAG (*Retrieval-Augmented Generation*).

Ce POC utilise notamment Python, LangChain, les modèles Mistral et un index vectoriel FAISS pour rechercher des événements culturels et générer des recommandations en langage naturel. Une interface Streamlit a également été ajoutée après la validation académique du POC.

Les résultats obtenus ont permis de démontrer la faisabilité technique de cette approche. Toutefois, le prototype présente des limites pour une exploitation à plus grande échelle, notamment en matière de mémoire conversationnelle, de personnalisation géographique, d'actualisation des informations et de supervision.

L'objectif de ce nouveau projet est de concevoir la transformation du POC en un Minimum Viable Product (MVP), capable de répondre aux besoins prioritaires de Puls-Events tout en intégrant les exigences de robustesse, de sécurité, de maintenabilité et de scalabilité.

Le présent rapport propose une analyse des besoins, un plan de projet, un macro backlog, une architecture technique cible, une étude des solutions cloud et une estimation des coûts de développement et d'exploitation.

---

# 1. Analyse et synthèse des besoins formulés par l'équipe

## 1.1 Contexte et enjeux métiers

Puls-Events souhaite améliorer l'expérience de découverte des événements culturels en proposant un assistant conversationnel intelligent.

Le POC existant a démontré l'intérêt d'une recherche sémantique associée à la génération de réponses en langage naturel.

La transformation vers un MVP doit permettre de disposer d'une solution plus adaptée à une utilisation réelle par les utilisateurs de la plateforme.

Les principaux enjeux métiers sont :

- Améliorer la pertinence des recommandations culturelles.
- Personnaliser les réponses selon les préférences et les échanges précédents.
- Prendre en compte la localisation géographique.
- Fournir des informations actualisées sur les événements.
- Mesurer les performances du chatbot et la satisfaction des utilisateurs.
- Maîtriser les coûts techniques et préparer une montée en charge progressive.

## 1.2 Objectifs du MVP

Le MVP devra répondre à quatre objectifs fonctionnels prioritaires.

### Objectif 1 — Mémoire conversationnelle

Permettre au chatbot de conserver le contexte d'une conversation afin d'éviter de demander plusieurs fois les mêmes informations et de produire des réponses cohérentes au fil des échanges.

### Objectif 2 — Personnalisation géographique

Adapter les recommandations selon la ville, la localisation fournie par l'utilisateur ou un périmètre géographique défini.

### Objectif 3 — Recherche Web en temps réel

Compléter la recherche dans les données vectorisées par des informations récentes provenant de sources externes.

La bibliothèque `smolagents` de Hugging Face constitue une solution candidate à étudier pour orchestrer cette recherche.

### Objectif 4 — Monitoring et satisfaction

Mettre en place des indicateurs permettant de suivre les performances techniques, les erreurs, les coûts et les retours des utilisateurs.

## 1.3 Utilisateurs cibles

| Utilisateur | Besoin principal | Cas d'usage |
|---|---|---|
| Visiteur de la plateforme | Découvrir des événements | Rechercher des concerts, expositions ou spectacles |
| Utilisateur régulier | Obtenir des recommandations personnalisées | Poursuivre une conversation en conservant ses préférences |
| Équipe produit | Améliorer l'expérience utilisateur | Analyser les retours et les fonctionnalités utilisées |
| Équipe technique | Maintenir le service | Surveiller les performances, les erreurs et la disponibilité |
| Équipe marketing | Comprendre les attentes des utilisateurs | Étudier les tendances d'utilisation à partir de données agrégées |

## 1.4 Cas d'usage principaux

**CU01 — Rechercher un événement culturel**

Un utilisateur demande : « Quels concerts sont prévus à Marseille ce week-end ? »

Le système recherche les événements correspondant à la demande et présente les résultats pertinents.

**CU02 — Poursuivre une conversation**

Après une première recherche, l'utilisateur demande : « Et parmi ces événements, lesquels sont adaptés aux enfants ? »

Le chatbot doit comprendre que cette question fait référence aux résultats précédents.

**CU03 — Rechercher des événements à proximité**

Un utilisateur indique sa ville ou autorise l'utilisation de sa localisation.

Le système adapte les recommandations à la zone géographique concernée.

**CU04 — Obtenir des informations actualisées**

Un utilisateur souhaite vérifier les horaires ou la disponibilité d'un événement.

Le système consulte une source actualisée lorsqu'elle est disponible et indique les informations obtenues.

**CU05 — Évaluer une recommandation**

Après avoir reçu une réponse, l'utilisateur peut indiquer si celle-ci lui a été utile.

Cette information contribue au suivi de la satisfaction et à l'amélioration du service.

## 1.5 Besoins fonctionnels

| ID | Besoin fonctionnel | Priorité proposée |
|---|---|---|
| BF01 | Rechercher des événements par langage naturel | Must-Have |
| BF02 | Conserver le contexte conversationnel | Must-Have |
| BF03 | Filtrer les événements selon la localisation | Must-Have |
| BF04 | Rechercher des informations actualisées sur le Web | Must-Have |
| BF05 | Afficher des recommandations contextualisées | Must-Have |
| BF06 | Collecter les retours de satisfaction | Must-Have |
| BF07 | Personnaliser durablement les préférences utilisateur | Nice-to-Have |

## 1.6 Besoins non fonctionnels et contraintes techniques

| Domaine | Exigence |
|---|---|
| Performance | Maintenir des temps de réponse acceptables pour une application interactive |
| Scalabilité | Permettre une augmentation progressive du nombre d'utilisateurs |
| Disponibilité | Limiter les interruptions et prévoir la gestion des défaillances |
| Sécurité | Protéger les accès aux services, aux données et aux clés API |
| Confidentialité | Définir les règles de conservation des conversations et respecter le RGPD |
| Observabilité | Centraliser les logs, les métriques et les alertes |
| Maintenabilité | Séparer les composants et faciliter leur évolution |
| Coûts | Suivre les dépenses cloud et les appels aux modèles d'IA |

Les objectifs chiffrés de performance, de disponibilité et de charge devront être définis dans la phase de dimensionnement.

## 1.7 État des lieux du POC existant

| Composant | État actuel | Évolution envisagée |
|---|---|---|
| Collecte OpenAgenda | Réalisée | Actualisation automatisée et contrôlée |
| Préparation des données | Réalisée | Renforcement des contrôles qualité |
| Embeddings Mistral | Intégrés | Gestion des quotas et des coûts |
| Recherche vectorielle FAISS | Fonctionnelle | Étude de la persistance et de la montée en charge |
| Chaîne RAG LangChain | Intégrée | Ajout du contexte conversationnel |
| Interface Streamlit | Développée | Adaptation à l'architecture cible |
| Recherche géographique | À renforcer | Filtrage géographique structuré |
| Recherche Web temps réel | À concevoir | Intégration d'un service de recherche externe |
| Monitoring | À concevoir pour le MVP | Métriques, logs, alertes et satisfaction |

Le POC dispose également d'une suite de 39 tests automatisés réussis lors de la dernière vérification documentée. Ces tests valident les comportements couverts par la suite, mais ne constituent pas une mesure complète de la pertinence des recommandations.

## 1.8 Risques et points de vigilance

Les principaux risques identifiés à ce stade sont :

- **Dépendance aux API externes :** quotas, indisponibilités et erreurs HTTP 429.
- **Qualité des données :** informations manquantes, obsolètes ou incohérentes.
- **Coûts variables :** consommation des API de génération et d'embeddings.
- **Confidentialité :** conservation et exploitation des historiques de conversation.
- **Montée en charge :** limites d'une architecture initialement conçue pour un POC.
- **Qualité des réponses :** recommandations inexactes ou insuffisamment contextualisées.

Ces risques seront repris dans le macro backlog et dans le plan de projet, avec des mesures de mitigation et des critères de validation.

## 1.9 Synthèse des besoins

La transformation de Puls-Events vers un MVP repose sur la conservation des acquis du POC et l'ajout progressif de quatre capacités : mémoire conversationnelle, personnalisation géographique, recherche Web actualisée et monitoring.

La solution cible devra être suffisamment modulaire pour évoluer, tout en restant économiquement soutenable.

Les choix d'architecture, de fournisseur cloud, de dimensionnement et de déploiement seront détaillés dans les sections suivantes du rapport.