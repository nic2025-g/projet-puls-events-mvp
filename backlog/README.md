# Macro-backlog — MVP Puls-Events

## 1. Objectif

Ce macro-backlog a pour objectif de planifier la transformation du POC RAG de Puls-Events en un MVP exploitable, sécurisé et évolutif.

Il traduit les besoins fonctionnels et non fonctionnels identifiés dans `rapport/01_analyse_besoins.md` en éléments de travail priorisés et estimés.

Le backlog concerne le **développement futur du MVP**, et non les 50 heures consacrées à la mission de conception OpenClassrooms.

## 2. Périmètre fonctionnel

Le MVP s'appuie sur les composants déjà réalisés dans le POC : Python, LangChain, Mistral, FAISS et une interface Streamlit.

Les principaux lots de travail sont :

- LOT-01 : Recherche sémantique et recommandations.
- LOT-02 : Mémoire conversationnelle.
- LOT-03 : Personnalisation géographique.
- LOT-04 : Recherche Web actualisée.
- LOT-05 : Monitoring et satisfaction utilisateur.
- LOT-06 : Industrialisation, sécurité et déploiement.
- LOT-07 : Préférences utilisateur persistantes.

## 3. Méthode de priorisation

Deux niveaux de priorité sont retenus :

- **Must-Have** : fonctionnalité ou exigence indispensable au fonctionnement du MVP.
- **Nice-to-Have** : amélioration pouvant être reportée à une version ultérieure.

Les fonctionnalités BF01 à BF06 et les exigences techniques essentielles sont classées Must-Have.

La personnalisation durable des préférences (BF07) est classée Nice-to-Have.

## 4. Méthode d'estimation

Les charges sont exprimées en **jours-homme (JH)**.

Un jour-homme représente une journée de travail d'une personne. Il ne correspond pas nécessairement à un jour calendaire.

Les estimations devront prendre en compte :

- L'analyse et la conception technique.
- Le développement ou l'adaptation des composants existants.
- Les tests et la validation.
- L'intégration et la documentation.

Ces estimations seront prévisionnelles et devront être révisées après validation des choix techniques et des ressources disponibles.

## 5. Dépendances et risques

Chaque élément du backlog comportera ses dépendances techniques, ses principaux risques et les mesures envisagées pour les réduire.

Les risques identifiés concernent notamment les API externes, la qualité des données, les coûts des modèles d'IA, la confidentialité des conversations, la montée en charge et la pertinence des recommandations.

## 6. Livrables

Le dossier `backlog/` contiendra :

- `README.md` : méthodologie de construction et d'estimation.
- `macro_backlog_mvp.xlsx` : backlog priorisé, charges, critères d'acceptation, dépendances et risques.

Les estimations serviront à consolider le calendrier prévisionnel du futur MVP et à préparer l'évaluation des coûts BUILD.

Le calendrier de développement de 12 semaines présenté dans le plan de projet constitue une hypothèse initiale, à confirmer après estimation et identification des ressources nécessaires.