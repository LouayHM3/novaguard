# 🛡️ NovaGuard AI - Web Application Firewall Intelligent

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.109-green.svg)](https://fastapi.tiangolo.com/)

**NovaGuard AI** est un pare-feu applicatif web de nouvelle génération qui utilise l'intelligence artificielle pour détecter et bloquer les menaces en temps réel.

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
-  Création de règles personnalisées
-  Logs détaillés
-  Intégration Splunk UF
-  Métriques de performance

---

##  Architecture

```
┌─────────────────────────────────────┐
│         OKD / Kubernetes            │
├─────────────────────────────────────┤
│                                     │
│  Apache  →  FastAPI  →  PostgreSQL │
│     ↓           ↓                   │
│  WAF AI  →  ML Engine               │
│     ↓                               │
│  Splunk  ←  Logs                    │
│                                     │
└─────────────────────────────────────┘
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

##  Contribution

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



## Remerciements

- Sopra Steria Group pour le sponsoring
- Communauté open-source
- Contributeurs et testeurs

---

**Développé avec ❤️ par l'équipe NovaGuard**


