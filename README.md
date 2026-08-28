# 🚀 Tech Stack Advisor

Une application Machine Learning qui recommande une stack technique adaptée à ton projet, en fonction de son type, de la taille de l'équipe, du besoin de performance et du niveau d'expérience.

**🔗 Démo en ligne :** [gildas2001-tech-stack-advisor.hf.space](https://gildas2001-tech-stack-advisor.hf.space)
**🐳 Image Docker :** [edenakpo/tech-stack-advisor](https://hub.docker.com/r/edenakpo/tech-stack-advisor)

---

## 📋 À propos

Renseigne quatre informations sur ton projet :
- **Project Type** — Web App, API, ML App, ou Real-time App
- **Team Size** — la taille de ton équipe
- **Performance Need** — Low, Medium, ou High
- **Experience Level** — Beginner, Intermediate, ou Expert

L'application encode ces choix, les passe à un modèle de classification entraîné avec `scikit-learn`, puis retourne une recommandation de stack technique adaptée à ce profil.

## 🛠️ Stack technique

| Composant | Technologie |
|---|---|
| Modèle ML | scikit-learn |
| Interface | Gradio |
| Conteneurisation | Docker |
| Hébergement | Hugging Face Spaces |
| Langage | Python 3.11 |

## ⚙️ Comment ça marche

1. `train.py` entraîne le modèle et génère `model.pkl` (le modèle) et `encoders.pkl` (les encodeurs qui traduisent chaque champ catégoriel en valeur numérique)
2. `app.py` charge ces deux fichiers, construit l'interface avec **Gradio**, et sert les prédictions en temps réel
3. L'application est packagée dans une image **Docker** via un `Dockerfile` multi-étapes (image de base `python:3.11-slim`, dépendances installées séparément du code pour profiter du cache des layers)
4. L'image est déployée sur **Hugging Face Spaces**, avec le port 7860 exposé

## 📁 Structure du projet

```
tech-stack-advisor/
├── app.py              # Interface Gradio + logique de prédiction
├── train.py             # Entraînement du modèle et génération des encodeurs
├── model.pkl             # Modèle scikit-learn entraîné
├── encoders.pkl           # Encodeurs pour les variables catégorielles
├── requirements.txt        # Dépendances Python (versions figées)
├── Dockerfile             # Définition de l'image de conteneur
├── .dockerignore           # Fichiers exclus du build Docker
└── README.md
```

## 🚀 Lancer le projet en local

```bash
git clone https://github.com/Gildas-EDEN/tech-stack-advisor.git
cd tech-stack-advisor

python -m venv .venv
.venv\Scripts\Activate.ps1     # Windows
# source .venv/bin/activate    # macOS / Linux

pip install -r requirements.txt
python app.py
```
L'application est ensuite accessible sur `http://localhost:7860`.

## 🐳 Lancer avec Docker

**Option 1 — Construire l'image toi-même**
```bash
docker build -t tech-stack-advisor .
docker run -p 7860:7860 tech-stack-advisor
```

**Option 2 — Utiliser l'image déjà publiée sur Docker Hub**
```bash
docker pull edenakpo/tech-stack-advisor:v2
docker run -p 7860:7860 edenakpo/tech-stack-advisor:v2
```

## 📄 Licence

Ce projet est sous licence **Apache 2.0**. Voir le fichier [LICENSE](./LICENSE) pour plus de détails.

## 🙏 Remerciements

Application développée à partir d'un projet initial de [Gourav Shah](https://www.linkedin.com/in/gouravshah/) (School of DevOps), containerisée, déboguée et déployée par mes soins.
