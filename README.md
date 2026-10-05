# 🛡️ NovaGuard AI - Web Application Firewall Intelligent

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.109-green.svg)](https://fastapi.tiangolo.com/)

**NovaGuard AI** est un pare-feu applicatif web de nouvelle génération qui utilise l'intelligence artificielle pour détecter et bloquer les menaces en temps réel.


## Rapport détaillé

[Consulter le rapport NovaGuard AI (PDF, 79 pages)](docs/reports/WAF_Intelligent_NovaGuardAI.pdf)

Rapport de projet de fin d’année II à l’ENIT, année universitaire 2025/2026 : contexte, architecture, agent ModSecurity, API FastAPI, interface Angular, assistance IA/RAG, tests et limites de l’évaluation.


---

##  Table des Matières

- [Vue d'ensemble](#-vue-densemble)
- [Fonctionnalités](#-fonctionnalités)
- [Architecture](#-architecture)
- [Installation](#-installation)
- [Utilisation](#-utilisation)
- [Technologies](#-technologies)
- [Développement](#-développement)
- [Contribution](#-contribution)
- [Licence](#-licence)

---

##  Vue d'ensemble

NovaGuard AI remplace les solutions WAF traditionnelles comme ModSecurity en offrant :

- Détection intelligente des menaces via Machine Learning
- Réduction des faux positifs grâce à l'IA
- Réponses automatisées aux attaques
- Interface de monitoring moderne
- Intégration native avec Apache et Splunk

---

##  Fonctionnalités

### Protection en Temps Réel

- ✅ Détection d'injection SQL
- ✅ Protection contre XSS (Cross-Site Scripting)
- ✅ Prévention Path Traversal
- ✅ Rate Limiting et protection DDoS
- ✅ Détection d'anomalies par IA

### Intelligence Artificielle

- Détection d'anomalies (Isolation Forest, K-means)
-  Classification des attaques (Random Forest, XGBoost)
-  Scoring et priorisation des menaces
-  Analyse NLP des logs

### Gestion et Monitoring

-  Dashboard interactif (Angular)
- Création de règles personnalisées
-  Logs détaillés
- Intégration Splunk UF
- Métriques de performance

---

##  Architecture

### Vue d'Ensemble Simplifiée

```
Internet
   ↓
[Client Web/Mobile]
   ↓
┌─────────────────────────────────────────────────────┐
│                  NOVAGUARD WAF                      │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐     │
│  │  Apache  │ → │ Module   │ → │ FastAPI  │     │
│  │  Serveur │    │   WAF    │    │ Backend  │     │
│  └──────────┘    └──────────┘    └──────────┘     │
│                        ↓                            │
│                  ┌──────────┐                       │
│                  │ Moteur   │                       │
│                  │    IA    │                       │
│                  └──────────┘                       │
└─────────────────────────────────────────────────────┘
   ↓                    ↓                ↓
[Application]    [PostgreSQL]      [Splunk SOC]
 Protégée         Base de            Monitoring
                  Données
```

### Flux de Requête - Étape par Étape

```
1. CLIENT envoie une requête HTTP
   │
   ↓
2. APACHE reçoit la requête
   │  (Port 80/443)
   │
   ↓
3. MODULE WAF intercepte
   │  (mod_novaguard.so)
   │  • Extrait les données
   │  • Envoie à FastAPI
   │
   ↓
4. FASTAPI analyse
   │  (Port 8000)
   │  ┌─────────────────┐
   │  │ A. Règles Basic │
   │  │ B. ML Detection │
   │  │ C. Scoring      │
   │  └─────────────────┘
   │
   ↓
5. DÉCISION
   │
   ├─→ [BLOQUÉ] → Retour 403
   │              Log vers Splunk
   │
   └─→ [AUTORISÉ] → Passe à l'app
                     Log vers DB
```

### Composants Principaux

#### 1️⃣ Apache + Module WAF
- Intercepte toutes les requêtes HTTP
- Extrait : URL, Headers, Body, IP Client
- Premier niveau de filtrage

#### 2️⃣ Backend FastAPI
- API principale d'analyse
- Moteur de règles de sécurité
- Coordination avec le ML Engine

#### 3️⃣ Moteur d'Intelligence Artificielle
- **Détection d'anomalies** : Isolation Forest, K-means
- **Classification** : Random Forest, XGBoost
- **Scoring** : Évaluation de criticité (0-100)
- **NLP** : Analyse textuelle des logs

#### 4️⃣ Base de Données PostgreSQL
- Stockage des menaces détectées
- Règles de sécurité personnalisées
- Historique des attaques
- IPs bloquées

#### 5️⃣ Dashboard Angular
- Monitoring temps réel
- Gestion des règles
- Visualisation des alertes
- Rapports et analytics

#### 6️⃣ Intégration Splunk
- Collecte centralisée des logs
- Corrélation avec SOC
- Alertes avancées

### Exemple : Détection d'Injection SQL

```
┌─────────────────────────────────────────────────┐
│  1. REQUÊTE MALVEILLANTE                        │
│     GET /users?id=1' OR '1'='1                  │
└─────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────┐
│  2. APACHE + MODULE WAF                         │
│     Intercepte et extrait                       │
└─────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────┐
│  3. FASTAPI - RULES ENGINE                      │
│     Pattern SQL détecté → Score: 80/100         │
└─────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────┐
│  4. ML ENGINE - CLASSIFICATION                  │
│     Type: SQL_INJECTION                         │
│     Confiance: 95% → Score final: 95/100        │
└─────────────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────────────┐
│  5. DÉCISION: BLOQUER                           │
│     • Block IP pendant 15 min                   │
│     • Retourne 403 Forbidden                    │
│     • Log dans PostgreSQL + Splunk              │
└─────────────────────────────────────────────────┘
```

---

##  Installation

### Prérequis

- Python 3.10 ou supérieur
- Node.js 18 ou supérieur
- PostgreSQL 15 ou supérieur
- Docker et Docker Compose
- Git

### Installation Rapide

```bash
# 1. Cloner le repository
git clone https://github.com/yourusername/novaguard.git
cd novaguard

# 2. Lancer avec Docker Compose
docker-compose up -d

# 3. Accéder aux services
# Backend API: http://localhost:8000
# Frontend: http://localhost:4200
# API Docs: http://localhost:8000/docs
```

### Installation Manuelle

#### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

#### Frontend

```bash
cd frontend
npm install
ng serve
```

#### Base de données

```bash
createdb novaguard
cd backend
alembic upgrade head
```

---

##  Utilisation

### Démarrage Rapide

```bash
# Démarrer tous les services
docker-compose up -d

# Vérifier le statut
docker-compose ps

# Voir les logs
docker-compose logs -f backend
```

### Accès aux Services

| Service | URL | Description |
|---------|-----|-------------|
| Backend API | http://localhost:8000 | API principale |
| Documentation API | http://localhost:8000/docs | Swagger UI |
| Frontend | http://localhost:4200 | Dashboard Angular |
| Base de données | localhost:5432 | PostgreSQL |
| Redis | localhost:6379 | Cache |

### Tests

```bash
# Backend
cd backend
pytest

# Frontend
cd frontend
npm test
```

---

##  Technologies

### Backend

- **FastAPI** - Framework web Python
- **PostgreSQL** - Base de données
- **Redis** - Cache et rate limiting
- **SQLAlchemy** - ORM

### Frontend

- **Angular** - Framework JavaScript
- **TypeScript** - Langage typé
- **Chart.js** - Visualisations

### Intelligence Artificielle

- **scikit-learn** - Machine Learning
- **XGBoost** - Gradient Boosting
- **NLTK/spaCy** - Traitement du langage

### DevOps

- **Docker** - Conteneurisation
- **OKD/Kubernetes** - Orchestration
- **GitLab CI/CD** - Intégration continue

---

##  Développement

### Structure du Projet

```
novaguard/
├── backend/          # API FastAPI
├── frontend/         # Application Angular
├── ml-engine/        # Modèles ML
├── deployment/       # Configs Kubernetes
├── docs/             # Documentation
└── docker-compose.yml
```

### Roadmap

#### Phase 1 - Core WAF (6 semaines)
- [x] Setup infrastructure
- [ ] Module Apache
- [ ] Règles de sécurité basiques
- [ ] Dashboard initial

#### Phase 2 - Intelligence IA (6 semaines)
- [ ] Collecte de datasets
- [ ] Modèles de détection
- [ ] Classification d'attaques
- [ ] Intégration temps réel

#### Phase 3 - Automatisation (3 semaines)
- [ ] Moteur de règles dynamiques
- [ ] Réponses automatiques
- [ ] Analyse NLP

#### Phase 4 - Production (6 semaines)
- [ ] Tests de charge
- [ ] Intégration Splunk
- [ ] Documentation finale
- [ ] Déploiement

---

##  contribution

Les contributions sont les bienvenues ! Consultez [CONTRIBUTING.md](CONTRIBUTING.md) pour les directives.

### Comment Contribuer

1. Fork le projet
2. Créer une branche (`git checkout -b feature/AmazingFeature`)
3. Commit les changements (`git commit -m 'Add AmazingFeature'`)
4. Push vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

---

##  Métriques de Performance

Objectifs de performance :

- **Latence** : < 50ms par requête
- **Débit** : > 10 000 requêtes/seconde
- **Faux Positifs** : < 1%
- **Détection** : > 95%
- **Disponibilité** : 99.9%

---

## Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

##  Équipe

- **Chef de Projet** : PRODOPS-Pole Sécurité
- **Support Technique** : 459.Prodops-NSS.Operations

---

##  Remerciements

- Sopra Steria Group pour le sponsoring
- Communauté open-source
- Contributeurs et testeurs

---

**Développé avec ❤️ par l'équipe NovaGuard**


