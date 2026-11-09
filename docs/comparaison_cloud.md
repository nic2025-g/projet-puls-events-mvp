# Étude comparative des fournisseurs cloud — Puls-Events

## 1. Objectif de l'étude

L'objectif de cette étude est d'identifier le fournisseur cloud le plus adapté à la transformation du POC RAG de Puls-Events en un MVP sécurisé, maintenable, évolutif et économiquement soutenable.

Trois fournisseurs sont étudiés :

- Amazon Web Services (AWS)
- Microsoft Azure
- Google Cloud Platform (GCP)

La comparaison repose sur les besoins identifiés dans `rapport/01_analyse_besoins.md`, le calendrier prévisionnel de `rapport/02_plan_projet.md` et le macro-backlog du MVP.

Cette étude prépare la conception de l'architecture cible et l'estimation des coûts d'exploitation (OPEX).

### 1.1. Justification du périmètre de comparaison

L'étude du choix d'un fournisseur cloud pour le MVP Puls-Events s'appuie sur une présélection de six acteurs :

- Amazon Web Services (AWS)
- Microsoft Azure
- Google Cloud Platform (GCP)
- OVHcloud
- Scaleway
- DigitalOcean

Cette présélection permet d'identifier plusieurs solutions d'hébergement possibles, notamment des fournisseurs internationaux et européens.

Pour respecter le périmètre et le temps disponible pour l'étude, trois fournisseurs ont été retenus pour une analyse approfondie : **AWS, Microsoft Azure et Google Cloud**.

Cette sélection repose sur les considérations suivantes :

- La disponibilité de services managés couvrant les principaux besoins du MVP : exécution applicative, PostgreSQL, stockage, supervision et gestion des secrets.
- La possibilité d'envisager une architecture intégrant la recherche vectorielle et les composants RAG.
- L'existence de régions d'hébergement européennes.
- La disponibilité de calculateurs de prix permettant de documenter les hypothèses financières.
- La possibilité d'étudier des services fonctionnellement comparables entre fournisseurs.

OVHcloud, Scaleway et DigitalOcean restent des alternatives pertinentes, mais ne font pas l'objet d'une analyse tarifaire détaillée dans cette étude.

Cette présélection ne constitue pas un classement des fournisseurs. Le choix final parmi les trois candidats sera établi à partir de l'analyse multicritère AHP, des estimations financières et des contraintes techniques et réglementaires du MVP Puls-Events.

## 2. Contraintes et hypothèses

Le POC existant repose sur Python, LangChain, Mistral AI, FAISS et Streamlit.

La solution cloud devra permettre :

- L'exécution des composants applicatifs Python.
- La gestion du contexte conversationnel.
- Le stockage et la recherche des données événementielles.
- L'intégration de services externes, notamment OpenAgenda et les API d'IA.
- La journalisation, la supervision et le suivi des coûts.
- La protection des données et la gestion sécurisée des secrets.
- Une montée en charge progressive.

L'hébergement dans une région européenne sera privilégié. La conformité RGPD devra également prendre en compte les contrats, les transferts de données, les durées de conservation et les contrôles d'accès.

Les volumes d'utilisation, les objectifs de performance et les budgets détaillés restent à définir.

## 3. Méthode de comparaison multicritère AHP

### 3.1. Principe méthodologique

La sélection du fournisseur cloud repose sur la méthode AHP (Analytic Hierarchy Process), développée par Thomas Saaty.

Cette méthode permet de déterminer les pondérations des critères à partir de comparaisons deux à deux, plutôt que de fixer directement des pourcentages arbitraires.

Les exigences minimales de sécurité, de conformité réglementaire et de compatibilité technique sont considérées comme des contraintes éliminatoires. La notation multicritère porte uniquement sur les fournisseurs satisfaisant ces exigences.

### 3.2. Critères retenus

Six critères sont évalués :

- C1 : Coûts d'exploitation
- C2 : Compatibilité RAG et recherche vectorielle
- C3 : Scalabilité et disponibilité
- C4 : Sécurité et conformité RGPD, au-delà des exigences obligatoires
- C5 : Simplicité de déploiement et de maintenance
- C6 : Monitoring et observabilité

### 3.3. Comparaisons deux à deux

Pour six critères, le nombre de comparaisons indépendantes est :

n(n − 1) / 2 = 6 × 5 / 2 = 15.

Les jugements utilisent l'échelle de Saaty, notamment les valeurs 1, 3, 5, 7 et 9, ainsi que leurs inverses.

Après analyse de cohérence, deux jugements initiaux ont été réexaminés et modifiés :

- Comparaison C1/C2 : passage de 3 à 1.
- Comparaison C1/C5 : passage de 1/3 à 1.

Ces révisions correspondent à une réévaluation des priorités métier de Puls-Events.

### 3.4. Matrice de comparaison retenue

L'ordre des lignes et des colonnes est : C1, C2, C3, C4, C5, C6.

| Critère | C1 | C2 | C3 | C4 | C5 | C6 |
|---|---:|---:|---:|---:|---:|---:|
| C1 | 1 | 1 | 1 | 1 | 1 | 1 |
| C2 | 1 | 1 | 3 | 3 | 1 | 1 |
| C3 | 1 | 1/3 | 1 | 1 | 3 | 1 |
| C4 | 1 | 1/3 | 1 | 1 | 3 | 1 |
| C5 | 1 | 1 | 1/3 | 1/3 | 1 | 1 |
| C6 | 1 | 1 | 1 | 1 | 1 | 1 |

La matrice est réciproque : a(j,i) = 1/a(i,j).

### 3.5. Calcul des pondérations

Les poids sont obtenus par normalisation du vecteur propre principal de la matrice AHP.

| Critère | Pondération AHP |
|---|---:|
| C1 — Coûts d'exploitation | 15,21 % |
| C2 — Compatibilité RAG | 25,11 % |
| C3 — Scalabilité et disponibilité | 16,28 % |
| C4 — Sécurité et RGPD | 16,28 % |
| C5 — Simplicité de déploiement | 11,91 % |
| C6 — Monitoring et observabilité | 15,21 % |
| **Total** | **100,00 %** |

La compatibilité RAG obtient la pondération la plus élevée. Cette priorité reflète l'objectif principal de Puls-Events : transformer un POC de recherche sémantique en MVP exploitable.

### 3.6. Vérification de la cohérence

Pour une matrice de dimension 6 :

- Valeur propre principale : λmax ≈ 6,5756
- Indice de cohérence : CI = (λmax − 6) / 5 ≈ 0,1151
- Indice aléatoire de Saaty : RI = 1,24
- Ratio de cohérence : CR = CI / RI ≈ 0,09284

**CR ≈ 9,28 % < 10 %.**

Le ratio respecte le seuil indicatif usuellement retenu pour l'AHP.

Les pondérations sont donc acceptées pour la suite de l'étude, tout en restant fondées sur des jugements métier.

### 3.7. Méthode de notation des fournisseurs

Chaque fournisseur admissible recevra une note de 1 à 5 pour chaque critère, sur la base d'éléments techniques et financiers vérifiables.

Le score global sur 100 sera calculé par :

Score global = Σ [(note du critère / 5) × poids du critère en pourcentage].

Les notes devront être justifiées par des sources documentées et des hypothèses de dimensionnement comparables.

Une analyse de sensibilité sera réalisée pour déterminer si le classement reste stable lorsque les pondérations varient.

La conformité aux contraintes éliminatoires sera vérifiée séparément, avant le classement multicritère.

## 4. Services cloud candidats

| Besoin | AWS | Microsoft Azure | Google Cloud |
|---|---|---|---|
| Exécution de conteneurs | ECS Fargate | Azure Container Apps | Cloud Run |
| Base de données relationnelle | RDS PostgreSQL | Azure Database for PostgreSQL | Cloud SQL PostgreSQL |
| Stockage objet | Amazon S3 | Azure Blob Storage | Cloud Storage |
| Monitoring | CloudWatch | Azure Monitor | Cloud Monitoring |
| Gestion des secrets | AWS Secrets Manager | Azure Key Vault | Secret Manager |
| Recherche vectorielle | PostgreSQL avec pgvector, sous réserve de compatibilité | PostgreSQL avec pgvector, sous réserve de compatibilité | PostgreSQL avec pgvector, sous réserve de compatibilité |

Ces services sont des candidats techniques. Leur sélection définitive dépendra de la comparaison, des contraintes de dimensionnement et des estimations financières.

## 5. Analyse comparative détaillée

### 5.1. Objectif et périmètre

Cette analyse compare les services PostgreSQL managés proposés par AWS, Microsoft Azure et Google Cloud pour le futur MVP de Puls-Events.

L'objectif est d'estimer le coût d'une base de données relationnelle susceptible de prendre en charge les données événementielles, les informations applicatives et, sous réserve de validation technique, certaines fonctionnalités de recherche vectorielle.

Les estimations ont été établies à l'aide des calculateurs officiels des fournisseurs, avec des configurations aussi proches que possible.

La comparaison porte uniquement sur la composante PostgreSQL. Elle ne représente pas le coût total d'exploitation du MVP.

### 5.2. Hypothèses de dimensionnement

Les hypothèses communes retenues sont les suivantes :

| Paramètre | Hypothèse |
|---|---|
| Moteur de base de données | PostgreSQL managé |
| Région d'hébergement | France |
| Nombre d'instances | 1 |
| Processeur | 2 vCPU ou vCores |
| Mémoire cible | Environ 4 Gio |
| Stockage | 32 Go ou Gio selon le fournisseur |
| Durée d'utilisation | 730 heures par mois |
| Haute disponibilité | Non activée |
| Engagement tarifaire | Aucun |
| Devise | Dollar américain (USD) |

Ces hypothèses correspondent à un scénario initial de dimensionnement du MVP et non à une prévision définitive de sa consommation.

Les performances réelles peuvent varier selon les familles de machines, les technologies de stockage et les mécanismes de gestion des ressources.

### 5.3. Configurations retenues

| Caractéristique | AWS | Microsoft Azure | Google Cloud |
|---|---|---|---|
| Service | Amazon RDS PostgreSQL | Azure Database for PostgreSQL Flexible Server | Cloud SQL PostgreSQL |
| Région | Europe (Paris) | France Central | Paris (europe-west9) |
| Instance | db.t4g.medium | B2s | N4 Custom |
| Niveau / édition | RDS Single-AZ | Burstable | Enterprise |
| Processeur | 2 vCPU | 2 vCores | 2 vCPU |
| Mémoire | 4 Gio | À confirmer | 4 Gio |
| Stockage | 32 Go | 32 Gio | 32 Gio |
| Type de stockage | SSD gp3 | Premium SSD | Hyperdisk Balanced |
| Haute disponibilité | Single-AZ | Non incluse dans le scénario retenu | Désactivée |
| Tarification | On-Demand | Estimation sans engagement identifié | Sans engagement |

Pour Google Cloud, le stockage Hyperdisk Balanced est configuré avec une capacité de 32 Gio, 3 000 IOPS et un débit de 140 Mio/s.

Les configurations sont proches en matière de capacité CPU et de stockage, mais elles ne garantissent pas des performances équivalentes.

### 5.4. Comparaison des coûts

Les estimations ont été actualisées et vérifiées le 6 novembre 2026.

| Fournisseur | Coût mensuel estimé | Coût annuel estimé |
|---|---:|---:|
| AWS | 56,82 USD | 681,84 USD |
| Microsoft Azure | 59,74 USD | 716,88 USD |
| Google Cloud | 97,92 USD | 1 175,10 USD |

Les montants annuels sont obtenus par extrapolation sur douze mois. Pour Google Cloud, le calcul annuel utilise le montant mensuel non arrondi de 97,92488 USD.

Dans les configurations étudiées, AWS présente le coût mensuel estimé le plus faible, suivi d'Azure puis de Google Cloud.

L'écart mensuel entre AWS et Azure est d'environ 2,92 USD, tandis que l'écart entre AWS et Google Cloud est d'environ 41,10 USD.

Ces résultats constituent une comparaison financière indicative et ne suffisent pas, à eux seuls, à déterminer le meilleur fournisseur.

### 5.5. Analyse des différences techniques

**AWS — Amazon RDS PostgreSQL**

L'estimation repose sur une instance db.t4g.medium disposant de 2 vCPU et de 4 Gio de mémoire, avec 32 Go de stockage SSD gp3.

Le déploiement est prévu dans une seule zone de disponibilité, avec une tarification à la demande.

Cette configuration présente le coût estimé le plus faible des trois scénarios.

**Microsoft Azure — PostgreSQL Flexible Server**

L'estimation repose sur une instance B2s de niveau Burstable, disposant de 2 vCores et de 32 Gio de stockage Premium SSD.

Le caractère Burstable de cette instance doit être pris en compte dans l'analyse des performances, notamment pour les charges prolongées.

La mémoire exacte de l'instance et la mention « Extended Support » figurant dans l'export devront être vérifiées avant la validation définitive de l'architecture.

**Google Cloud — Cloud SQL PostgreSQL**

L'estimation repose sur une instance N4 personnalisée, disposant de 2 vCPU et de 4 Gio de mémoire.

Le stockage utilise Hyperdisk Balanced, avec une capacité de 32 Gio.

Le montant estimé est supérieur à ceux des deux autres fournisseurs. Toutefois, les différences de technologies, de performances et de services inclus empêchent d'assimiler directement cet écart à une différence de rapport qualité-prix.

### 5.6. Compatibilité RAG et recherche vectorielle (C2)

Le POC de Puls-Events repose sur Python, LangChain, Mistral AI, FAISS et Streamlit.

Pour le MVP, PostgreSQL avec l'extension `pgvector` constitue une solution envisageable pour stocker les données événementielles et leurs représentations vectorielles dans une infrastructure centralisée.

Les documentations techniques consultées confirment les possibilités suivantes :

| Fournisseur | Service PostgreSQL | Compatibilité pgvector | Service d'exécution applicative |
|---|---|---|---|
| AWS | Amazon RDS for PostgreSQL | Prise en charge documentée | Amazon ECS avec AWS Fargate |
| Microsoft Azure | Azure Database for PostgreSQL Flexible Server | Prise en charge documentée | Azure Container Apps |
| Google Cloud | Cloud SQL for PostgreSQL | Prise en charge documentée | Google Cloud Run |

La documentation officielle de LangChain présente également l'intégration `langchain-postgres`, permettant d'utiliser PostgreSQL avec `pgvector` comme stockage vectoriel.

Les trois fournisseurs permettent donc d'envisager une architecture RAG fondée sur Python, LangChain et PostgreSQL avec `pgvector`, sous réserve de vérifier les versions compatibles et de réaliser des tests d'intégration.

**Conclusion pour le critère C2 :** aucun fournisseur ne présente, à ce stade, d'avantage décisif sur la seule prise en charge de `pgvector`. Les différences devront être examinées au regard de la facilité d'intégration, des performances, de la maintenance et des coûts.

Cette conclusion repose sur une analyse documentaire et non sur des tests de performance réalisés dans le cadre du projet.

### 5.7. Sécurité et conformité RGPD (C4)

La sécurité des données et la conformité au Règlement général sur la protection des données (RGPD) constituent des exigences importantes pour le MVP Puls-Events.

L'analyse documentaire porte sur le chiffrement des données, la sécurisation des communications, la gestion des identités et des accès, les engagements contractuels et les possibilités d'hébergement en France.

| Élément étudié | AWS | Microsoft Azure | Google Cloud |
|---|---|---|---|
| Base de données managée | Amazon RDS PostgreSQL | Azure PostgreSQL Flexible Server | Cloud SQL PostgreSQL |
| Chiffrement des données au repos | Pris en charge | Pris en charge | Pris en charge |
| Chiffrement des communications | SSL/TLS | TLS 1.2 et 1.3 documentés | SSL/TLS configurable |
| Gestion des accès | AWS IAM et contrôles PostgreSQL | Microsoft Entra ID et contrôles PostgreSQL | Google Cloud IAM et contrôles PostgreSQL |
| Gestion des clés | AWS KMS | Clés gérées par le service ou par le client | Cloud KMS et CMEK |
| Engagements contractuels relatifs aux données | AWS DPA et engagements complémentaires | Microsoft Products and Services DPA | Google Cloud Data Processing Addendum |
| Région française retenue | Paris | France Central | Paris (europe-west9) |

**AWS — Amazon RDS PostgreSQL**

AWS propose des mécanismes de chiffrement, de gestion des accès et de protection des données pour ses services cloud.

La documentation officielle présente également des engagements contractuels relatifs au traitement des données personnelles, notamment un avenant complémentaire concernant les demandes d'accès aux données des clients par des autorités publiques.

La région AWS Europe (Paris) permet d'envisager un hébergement de la base de données en France.

**Microsoft Azure — PostgreSQL Flexible Server**

Azure Database for PostgreSQL Flexible Server propose le chiffrement des données au repos, avec des clés gérées par le service ou des clés gérées par le client selon la configuration retenue.

La documentation consultée confirme la prise en charge des connexions chiffrées avec TLS 1.2 et TLS 1.3.

Microsoft publie également un Data Protection Addendum (DPA), qui précise les engagements contractuels relatifs au traitement et à la protection des données.

La région France Central constitue une option d'hébergement en France.

**Google Cloud — Cloud SQL PostgreSQL**

Cloud SQL pour PostgreSQL chiffre les données au repos par défaut. Il est également possible d'utiliser des clés de chiffrement gérées par le client (CMEK) avec Cloud KMS.

Les communications peuvent être sécurisées avec SSL/TLS, et Google Cloud IAM permet de contrôler les autorisations d'accès aux ressources.

Google publie un avenant relatif au traitement des données dans le cloud (DPA).

La documentation officielle des produits par région confirme la disponibilité de Cloud SQL à Paris (`europe-west9`).

**Analyse comparative**

Les trois fournisseurs disposent de mécanismes documentés de protection des données et proposent des régions françaises pour les services PostgreSQL étudiés.

À ce stade, les éléments consultés ne permettent pas d'établir une supériorité générale d'un fournisseur en matière de conformité RGPD.

La conformité effective du MVP dépendra notamment :

- de la nature des données personnelles collectées ;
- de la configuration des accès et du chiffrement ;
- des durées de conservation et des procédures de suppression ;
- des sous-traitants et des éventuels transferts internationaux ;
- des traitements effectués par les API externes, notamment Mistral AI ;
- des mesures organisationnelles et techniques mises en œuvre.

**Conclusion pour le critère C4 :** AWS, Azure et Google Cloud présentent des capacités documentées compatibles avec les exigences de sécurité envisagées pour le MVP Puls-Events. La notation comparative devra tenir compte des preuves disponibles, de la facilité de mise en œuvre et des exigences spécifiques du projet. La présence d'une région française ou d'un DPA ne suffit pas, à elle seule, à démontrer la conformité RGPD.

### 5.8. Limites des estimations

Plusieurs limites doivent être prises en compte :

- Les configurations ne sont pas strictement équivalentes en matière de performances CPU, de stockage et de gestion des ressources.
- Les coûts de sauvegarde, de transfert réseau et d'opérations supplémentaires ne sont pas nécessairement couverts de manière identique.
- Les estimations ne comprennent pas l'ensemble des services nécessaires au MVP.
- Les coûts liés aux modèles d'intelligence artificielle et aux API externes restent à évaluer.
- Les besoins réels en capacité et en disponibilité devront être précisés à partir de scénarios d'utilisation.
- Les prix peuvent évoluer et les factures réelles dépendront de la consommation effective.

Une estimation complète du coût d'exploitation du MVP devra également considérer les composants applicatifs, le stockage objet, la supervision, la gestion des secrets, le trafic réseau et les services d'IA.

### 5.9. Conclusion intermédiaire

La comparaison financière fait apparaître AWS comme la solution la moins coûteuse parmi les trois configurations PostgreSQL étudiées.

Cependant, le coût ne constitue qu'un des six critères de décision retenus dans la méthode AHP.

Le choix du fournisseur devra également intégrer la compatibilité avec l'architecture RAG, la scalabilité, la sécurité, la simplicité d'exploitation et les capacités de monitoring.

Aucune recommandation définitive n'est formulée à ce stade. Elle sera établie après l'analyse technique et la notation multicritère.

### 5.10. Justificatifs des estimations

Les fichiers suivants sont conservés dans le répertoire `docs/estimations_cloud/` :

- `aws_rds_postgresql_paris.pdf` : estimation Amazon RDS PostgreSQL.
- `azure_postgresql_france_central.xlsx` : estimation Azure Database for PostgreSQL.
- `gcp_cloud_sql_postgresql_paris.csv` : estimation Google Cloud SQL PostgreSQL.

Ces documents constituent les justificatifs financiers des scénarios étudiés.

## 6. Grille de notation pondérée

### 6.1. Méthode de notation

La comparaison des fournisseurs cloud repose sur les six critères et les pondérations déterminés par la méthode AHP dans la section 3.

Chaque fournisseur admissible reçoit une note comprise entre 1 et 5 pour chaque critère :

- 1 : très insuffisant ;
- 2 : insuffisant ;
- 3 : satisfaisant ;
- 4 : bon ;
- 5 : très bon.

Les notes sont attribuées à partir des caractéristiques techniques, des estimations financières et des sources officielles disponibles.

La conformité aux exigences éliminatoires, notamment réglementaires et techniques, doit être vérifiée avant le classement.

### 6.2. Grille de comparaison

| Critère | Poids AHP | AWS | Azure | Google Cloud |
|---|---:|---:|---:|---:|
| C1 — Coûts d'exploitation | 15,21 % | 5,00 | 4,76 | 2,90 |
| C2 — Compatibilité RAG | 25,11 % | 4,00 | 4,00 | 4,00 |
| C3 — Scalabilité et disponibilité | 16,28 % | 4,00 | 4,00 | 4,00 |
| C4 — Sécurité et RGPD | 16,28 % | 4,00 | 4,00 | 4,00 |
| C5 — Déploiement et maintenance | 11,91 % | 3,50 | 4,50 | 4,50 |
| C6 — Monitoring et observabilité | 15,21 % | 4,00 | 4,00 | 4,00 |

### 6.2.1. Justification des notes du critère C1 — Coûts d'exploitation

La notation du critère C1 repose sur les estimations mensuelles des services PostgreSQL managés, obtenues à partir des calculateurs officiels AWS, Microsoft Azure et Google Cloud le 6 novembre 2026.

Afin d'éviter une attribution arbitraire des notes, une normalisation proportionnelle inverse au coût est appliquée :

**Note C1 = 5 × (coût mensuel minimal / coût mensuel du fournisseur)**

Le coût mensuel minimal observé est celui d'AWS, soit 56,82 USD.

| Fournisseur | Coût mensuel | Note C1 / 5 | Contribution pondérée / 100 |
|---|---:|---:|---:|
| AWS | 56,82 USD | 5,00 | 15,21 |
| Microsoft Azure | 59,74 USD | 4,76 | 14,47 |
| Google Cloud | 97,92488 USD | 2,90 | 8,83 |

La contribution pondérée est calculée en multipliant la note non arrondie, divisée par 5, par le poids AHP du critère C1 (15,21 %).

Cette méthode privilégie les fournisseurs présentant le coût estimé le plus faible, tout en conservant une progression proportionnelle entre les notes.

**Limites :** cette notation repose uniquement sur le coût de PostgreSQL. Les configurations présentent encore des différences de performances et de services inclus. Les coûts applicatifs, réseau, IA et supervision ne sont pas intégrés.

Les notes C1 sont donc provisoires et devront être réexaminées lors de l'estimation globale des coûts d'exploitation du MVP.

La normalisation proportionnelle est une règle de notation complémentaire à l'AHP ; elle ne constitue pas une pondération AHP supplémentaire.

### 6.2.2. Justification des notes du critère C2 — Compatibilité RAG

L'évaluation du critère C2 repose sur les besoins techniques du MVP Puls-Events et sur l'analyse des documentations officielles des trois fournisseurs cloud.

Les éléments vérifiés comprennent :

- La prise en charge de PostgreSQL avec l'extension `pgvector`.
- La possibilité d'exécuter des applications Python conteneurisées.
- La disponibilité de services applicatifs managés.
- La possibilité d'intégrer LangChain à PostgreSQL grâce au package `langchain-postgres`.

Les services identifiés sont Amazon RDS et ECS Fargate pour AWS, Azure Database for PostgreSQL et Azure Container Apps pour Microsoft Azure, ainsi que Cloud SQL et Cloud Run pour Google Cloud.

Les trois fournisseurs répondent aux principales exigences de compatibilité documentées.

Aucune différence technique suffisamment démontrée ne justifie, à ce stade, une notation distincte.

Une note provisoire de **4/5** est donc attribuée à chaque fournisseur.

| Fournisseur | Note C2 / 5 | Contribution pondérée / 100 |
|---|---:|---:|
| AWS | 4,00 | 20,09 |
| Microsoft Azure | 4,00 | 20,09 |
| Google Cloud | 4,00 | 20,09 |

Cette notation traduit une compatibilité technique documentée, mais non encore validée par des essais d'intégration.

Elle ne constitue pas une mesure comparative de performance.

Les tests futurs devront notamment vérifier la connexion à PostgreSQL, l'utilisation de `pgvector`, l'intégration avec LangChain, les appels à Mistral AI et les performances du moteur de recherche sémantique.

Les notes pourront être révisées à partir des résultats de ces tests.

### 6.2.3. Justification des notes du critère C3 — Scalabilité et disponibilité

L'évaluation du critère C3 repose sur deux dimensions : la capacité des services applicatifs à s'adapter à une variation de charge et les mécanismes de haute disponibilité proposés pour PostgreSQL.

Les documentations officielles confirment les fonctionnalités suivantes :

| Capacité | AWS | Microsoft Azure | Google Cloud |
|---|---|---|---|
| Haute disponibilité PostgreSQL multizone | Amazon RDS Multi-AZ | PostgreSQL Flexible Server HA | Cloud SQL HA régionale |
| Basculement vers une instance de secours | Documenté | Documenté | Documenté |
| Scalabilité horizontale des applications | Amazon ECS Service Auto Scaling | Azure Container Apps avec KEDA | Cloud Run Autoscaling |
| Adaptation automatique selon la charge | Documentée | Documentée | Documentée |

Les trois fournisseurs proposent des mécanismes de résilience et de mise à l'échelle applicative compatibles avec les besoins envisagés pour Puls-Events.

Une note provisoire identique de **4/5** est attribuée aux trois fournisseurs, faute de différences suffisamment démontrées dans le périmètre étudié.

| Fournisseur | Note C3 / 5 | Contribution pondérée / 100 |
|---|---:|---:|
| AWS | 4,00 | 13,02 |
| Microsoft Azure | 4,00 | 13,02 |
| Google Cloud | 4,00 | 13,02 |

**Limites de l'évaluation :**

- Les estimations PostgreSQL utilisées dans le critère C1 ne comprennent pas la haute disponibilité.
- Les capacités de scalabilité applicative ne démontrent pas la scalabilité de PostgreSQL.
- Aucun test de charge ni de basculement n'a été réalisé.
- Les coûts additionnels de la haute disponibilité et de la mise à l'échelle restent à estimer.
- Les objectifs de disponibilité, de temps de reprise et de perte maximale de données admissible devront être définis pour le MVP.

Cette notation reflète les fonctionnalités documentées et ne constitue pas une mesure des performances ou de la disponibilité réelles.

### 6.2.4. Justification des notes du critère C4 — Sécurité et conformité RGPD

L'évaluation du critère C4 repose sur les exigences de sécurité et de protection des données applicables au MVP Puls-Events.

L'analyse documentaire porte sur cinq dimensions :

- Le chiffrement des données au repos.
- La sécurisation des communications.
- La gestion des identités et des autorisations.
- Les engagements contractuels relatifs au traitement des données.
- La disponibilité d'une région d'hébergement en France.

Les documentations officielles consultées confirment que les trois fournisseurs proposent des mécanismes répondant à ces cinq dimensions.

| Dimension | AWS | Microsoft Azure | Google Cloud |
|---|---|---|---|
| Chiffrement au repos | Documenté | Documenté | Documenté |
| Connexions chiffrées | Documentées | Documentées | Documentées |
| Gestion des accès | AWS IAM | Microsoft Entra ID et contrôles PostgreSQL | Google Cloud IAM |
| Engagements de traitement des données | AWS DPA | Microsoft DPA | Google Cloud DPA |
| Région française | Paris | France Central | Paris |

Les trois fournisseurs présentent donc des capacités de sécurité documentées adaptées au périmètre technique étudié.

Aucune différence suffisamment démontrée ne permet, à ce stade, d'attribuer une note supérieure à l'un des fournisseurs.

Une note provisoire identique de **4/5** est attribuée à chacun.

| Fournisseur | Note C4 / 5 | Contribution pondérée / 100 |
|---|---:|---:|
| AWS | 4,00 | 13,02 |
| Microsoft Azure | 4,00 | 13,02 |
| Google Cloud | 4,00 | 13,02 |

La contribution pondérée est calculée avec le poids AHP du critère C4, fixé à 16,28 %.

**Limites de l'évaluation :**

- La conformité RGPD ne découle pas automatiquement de l'utilisation d'un fournisseur cloud.
- Les paramètres de sécurité devront être configurés et vérifiés lors du déploiement.
- Les engagements contractuels devront être examinés en fonction des données réellement traitées.
- Les éventuels transferts internationaux, notamment via les API externes, devront être analysés.
- Aucun audit de sécurité ni test de configuration n'a encore été réalisé.

Cette notation traduit la disponibilité de mécanismes de sécurité documentés et non une certification de conformité du MVP.

La vérification des exigences réglementaires éliminatoires demeure une condition préalable au classement définitif.


### 6.2.5. Justification des notes du critère C5 — Déploiement et maintenance

Le critère C5 évalue la simplicité de déploiement et d'exploitation d'une application Python/RAG conteneurisée, dans le contexte d'un MVP disposant de ressources techniques limitées.

L'analyse repose sur quatre dimensions :

- La prise en charge des conteneurs Docker.
- La quantité de configuration nécessaire au déploiement.
- La gestion des versions et des mises à jour.
- La maintenance de l'infrastructure sous-jacente.

| Dimension | AWS | Microsoft Azure | Google Cloud |
|---|---|---|---|
| Service applicatif | ECS avec Fargate | Azure Container Apps | Cloud Run |
| Exécution sans administration de serveurs | Oui | Oui | Oui |
| Déploiement de conteneurs | Oui | Oui | Oui |
| Gestion des versions | Définitions de tâches et déploiements ECS | Révisions applicatives | Révisions Cloud Run |
| Configuration opérationnelle | ECS, tâches, réseau et IAM | Environnement Container Apps, application et accès | Service Cloud Run, ressources et accès |

Les trois fournisseurs proposent des services managés adaptés au déploiement d'une application conteneurisée.

AWS ECS avec Fargate permet une configuration détaillée de l'exécution des tâches, mais implique plusieurs composants à coordonner.

Azure Container Apps et Google Cloud Run proposent des modèles de déploiement plus intégrés, potentiellement plus simples pour une petite équipe développant un MVP.

Une notation provisoire est proposée :

| Fournisseur | Note C5 / 5 | Contribution pondérée / 100 |
|---|---:|---:|
| AWS | 3,50 | 8,34 |
| Microsoft Azure | 4,50 | 10,72 |
| Google Cloud | 4,50 | 10,72 |

Ces notes représentent une appréciation qualitative de la simplicité opérationnelle. Elles ne résultent pas d'un chronométrage des déploiements ni d'un benchmark.

**Limites :**

- La simplicité réelle dépend des compétences de l'équipe.
- Les configurations de sécurité et de réseau peuvent modifier la complexité.
- Aucun déploiement comparatif n'a été effectué sur les trois plateformes.

### 6.2.6. Justification des notes du critère C6 — Monitoring et observabilité

Le critère C6 évalue les capacités de supervision nécessaires au suivi du MVP Puls-Events.

Les besoins identifiés concernent notamment :

- La disponibilité de l'application et du service PostgreSQL.
- Les temps de réponse des requêtes.
- Les erreurs applicatives et les échecs des appels aux API externes.
- La consommation des ressources.
- Le suivi des coûts et les mécanismes d'alerte.

| Dimension | AWS | Microsoft Azure | Google Cloud |
|---|---|---|---|
| Supervision native | Amazon CloudWatch | Azure Monitor | Cloud Monitoring |
| Centralisation des journaux | CloudWatch Logs | Azure Monitor Logs / Log Analytics | Cloud Logging |
| Métriques et tableaux de bord | Disponibles | Disponibles | Disponibles |
| Alertes | Disponibles | Disponibles | Disponibles |

Les trois fournisseurs proposent des services natifs permettant d'envisager une supervision adaptée aux besoins du MVP.

Aucune différence suffisamment établie dans le périmètre documentaire étudié ne permet de privilégier un fournisseur sur ce critère.

Une note provisoire identique de **4/5** est retenue.

| Fournisseur | Note C6 / 5 | Contribution pondérée / 100 |
|---|---:|---:|
| AWS | 4,00 | 12,17 |
| Microsoft Azure | 4,00 | 12,17 |
| Google Cloud | 4,00 | 12,17 |

**Limites :**

- Les métriques métier du chatbot devront être instrumentées dans l'application.
- La pertinence des réponses RAG ne peut pas être déduite des seules métriques d'infrastructure.
- Aucun dispositif complet de supervision n'a encore été testé.
- Les coûts de collecte et de conservation des journaux restent à estimer.

Cette notation évalue les fonctionnalités disponibles et non un niveau d'observabilité déjà atteint.

### 6.3. Calcul du score global

Le score pondéré de chaque fournisseur est calculé selon la formule :

**Score global = Σ [(note du critère / 5) × poids AHP en pourcentage]**

Le score final est exprimé sur 100.

Le classement ne sera établi qu'après justification des notes et vérification des exigences éliminatoires.


### 6.3.1. Résultats du classement multicritère

Les scores globaux sont calculés à partir des six critères, des notes provisoires attribuées aux fournisseurs et des pondérations AHP.

| Rang | Fournisseur | Score global / 100 |
|---|---|---:|
| 1 | Microsoft Azure | 83,49 |
| 2 | AWS | 81,85 |
| 3 | Google Cloud | 77,84 |

Les résultats sont calculés à partir des valeurs arrondies de la grille de notation.

Microsoft Azure obtient le meilleur score, principalement grâce à sa note favorable sur la simplicité de déploiement et de maintenance (C5), tout en conservant un coût PostgreSQL estimé proche de celui d'AWS.

AWS se classe deuxième. Il présente le coût PostgreSQL estimé le plus faible et un score global très proche de celui d'Azure.

Google Cloud se classe troisième, principalement en raison du coût supérieur de la configuration PostgreSQL étudiée.

L'écart entre Azure et AWS est d'environ 1,65 point sur 100. Ce résultat ne démontre pas une supériorité technique générale d'Azure.

Le classement reste provisoire, car il dépend de notes documentaires, d'estimations financières partielles et d'hypothèses de dimensionnement.

Il devra être confronté à une analyse de sensibilité, à la vérification des exigences éliminatoires et aux coûts globaux du MVP avant toute décision définitive.



### 6.4. Analyse de sensibilité

L'analyse de sensibilité vise à vérifier la robustesse du classement obtenu par la méthode AHP.

Le classement initial, calculé à partir des notes et poids arrondis, est le suivant :

| Fournisseur | Score initial / 100 |
|---|---:|
| Microsoft Azure | 83,49 |
| AWS | 81,85 |
| Google Cloud | 77,84 |

#### Scénario 1 — Révision de la simplicité de déploiement

La note C5 d'Azure est abaissée de 4,50 à 4,00, afin de représenter une complexité opérationnelle plus importante que prévu.

Les autres notes et pondérations restent inchangées.

| Fournisseur | Score recalculé / 100 |
|---|---:|
| Microsoft Azure | 82,30 |
| AWS | 81,85 |
| Google Cloud | 77,84 |

Azure conserve la première place, mais son avance sur AWS diminue.

#### Scénario 2 — Révision plus importante du critère C5

La note C5 d'Azure est abaissée à 3,50, soit la même note que celle attribuée à AWS.

| Fournisseur | Score recalculé / 100 |
|---|---:|
| AWS | 81,85 |
| Microsoft Azure | 81,11 |
| Google Cloud | 77,84 |

AWS passe alors en première position.

#### Interprétation

Ces scénarios montrent que le classement est sensible à l'évaluation de la simplicité de déploiement et de maintenance.

L'avantage initial d'Azure sur AWS est limité et ne constitue pas une preuve de supériorité générale.

Les pondérations AHP sont maintenues constantes dans ces deux scénarios : il s'agit d'une analyse de sensibilité des notes, et non des poids.

Une analyse complémentaire faisant varier les pondérations AHP pourra être réalisée si nécessaire.

Le choix final devra également tenir compte des coûts globaux du MVP, des compétences de l'équipe et de la vérification des exigences éliminatoires.


## 7. Recommandation du fournisseur cloud

### 7.1. Synthèse de la décision

L'analyse multicritère fondée sur la méthode AHP place Microsoft Azure en première position avec un score de 83,49/100, devant AWS (81,85/100) et Google Cloud (77,84/100).

Microsoft Azure est donc retenu comme **fournisseur recommandé à titre provisoire** pour l'architecture cible du MVP Puls-Events.

Cette recommandation repose principalement sur :

- La compatibilité documentée d'Azure Database for PostgreSQL Flexible Server avec l'extension pgvector.
- La possibilité de déployer une application Python conteneurisée avec Azure Container Apps.
- Les fonctionnalités de sécurité, de gestion des accès et de supervision proposées par Azure.
- La disponibilité de services dans la région France Central.
- Une estimation PostgreSQL mensuelle de 59,74 USD, proche de celle d'AWS (56,82 USD).

### 7.2. Architecture cible envisagée

L'architecture proposée comprend :

- Azure Container Apps pour l'exécution de l'application Python/RAG.
- Azure Database for PostgreSQL Flexible Server avec pgvector pour les données relationnelles et les représentations vectorielles.
- Azure Key Vault pour la gestion des secrets.
- Azure Monitor et Log Analytics pour la supervision et les journaux.
- L'API Mistral AI pour les fonctionnalités de génération de réponses.
- Une ingestion des événements issus notamment d'OpenAgenda, avec validation, transformation et mise à jour des données.

Le recours à PostgreSQL avec pgvector constitue une évolution envisagée du POC utilisant FAISS. Cette migration devra être validée techniquement.

### 7.3. Limites et conditions de validation

Le classement reste sensible à la note attribuée à la simplicité de déploiement et de maintenance.

AWS demeure une alternative crédible, particulièrement en raison de son coût PostgreSQL estimé plus faible.

Avant toute décision définitive, il conviendra de :

- Vérifier les exigences techniques et réglementaires éliminatoires.
- Confirmer les caractéristiques exactes et les conditions tarifaires de l'instance Azure.
- Compléter l'estimation du coût total d'exploitation du MVP.
- Tester l'intégration Python, LangChain, PostgreSQL et pgvector.
- Définir les objectifs de disponibilité, de performance et de supervision.
- Vérifier les conditions de traitement des données par les services et API externes.

### 7.4. Conclusion

Microsoft Azure constitue le choix recommandé pour la poursuite de la conception du MVP Puls-Events, selon les hypothèses et les critères retenus.

Cette décision représente une orientation d'architecture et non la preuve d'un déploiement déjà réalisé.

Elle pourra être révisée en fonction des résultats des tests techniques, de l'estimation globale des coûts et des contraintes opérationnelles.


## 8. Sources et références

### 8.1. Estimations financières

Les estimations ont été réalisées à l'aide des calculateurs officiels des fournisseurs et vérifiées le 6 novembre 2026.

- AWS Pricing Calculator : https://calculator.aws/
- Microsoft Azure Pricing Calculator : https://azure.microsoft.com/pricing/calculator/
- Google Cloud Pricing Calculator : https://cloud.google.com/products/calculator

Les exports sont conservés dans `docs/estimations_cloud/` :

- `aws_rds_postgresql_paris.pdf`
- `azure_postgresql_france_central.xlsx`
- `gcp_cloud_sql_postgresql_paris.csv`

### 8.2. Compatibilité RAG et services applicatifs

- AWS — Amazon ECS avec Fargate :
  https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html

- Microsoft Azure — Azure Container Apps :
  https://learn.microsoft.com/fr-fr/azure/container-apps/overview

- Google Cloud — Cloud Run :
  https://docs.cloud.google.com/run/docs/overview/what-is-cloud-run?hl=fr

- LangChain — Intégration PostgreSQL / pgvector :
  https://docs.langchain.com/oss/python/integrations/vectorstores/pgvector

- Google Cloud — Extensions PostgreSQL :
  https://cloud.google.com/sql/docs/postgres/extensions

- Microsoft Azure — Utilisation de pgvector :
  https://learn.microsoft.com/fr-fr/azure/postgresql/flexible-server/how-to-use-pgvector

### 8.3. Sécurité et protection des données

Les documentations officielles consultées portent notamment sur :

- AWS : chiffrement Amazon RDS, AWS IAM, AWS KMS et engagements de protection des données.
- Microsoft Azure : sécurité PostgreSQL Flexible Server, Microsoft Entra ID, TLS et Data Protection Addendum.
- Google Cloud : sécurité Cloud SQL, Cloud IAM, Cloud KMS et Cloud Data Processing Addendum.

Référence réglementaire :

- Règlement (UE) 2016/679 — RGPD :
  https://eur-lex.europa.eu/eli/reg/2016/679/oj

### 8.4. Limites documentaires

Les informations présentées reposent principalement sur les documentations officielles des fournisseurs et sur les estimations financières conservées dans le projet.

Les notes techniques constituent des appréciations provisoires. Elles ne remplacent pas des tests de déploiement, de performance, de sécurité ou de disponibilité.

Les caractéristiques des services, les conditions tarifaires et les exigences réglementaires devront être revérifiées avant une mise en production.