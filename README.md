# 🚀 Tech Stack Advisor

A Machine Learning application that recommends a suitable tech stack for your project, based on its type, team size, performance needs, and experience level.

**🔗 Live demo:** [gildas2001-tech-stack-advisor.hf.space](https://gildas2001-tech-stack-advisor.hf.space)
**🐳 Docker image:** [edenakpo/tech-stack-advisor](https://hub.docker.com/r/edenakpo/tech-stack-advisor)

---

## 📋 About

Provide four pieces of information about your project:

* Project Type : Web App, API, ML App, or Real-time App
* Team Size : the size of your team
* Performance Need : Low, Medium, or High
* Experience Level : Beginner, Intermediate, or Expert

The application encodes these inputs, feeds them into a classification model trained with `scikit-learn`, and returns a tech stack recommendation tailored to that profile.

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| ML model | scikit-learn |
| Interface | Gradio |
| Containerization | Docker |
| Hosting | Hugging Face Spaces |
| Language | Python 3.11 |

## ⚙️ How it works

1. `train.py` trains the model and generates `model.pkl` (the model) and `encoders.pkl` (the encoders that translate each categorical field into a numeric value)
2. `app.py` loads both files, builds the interface with **Gradio**, and serves predictions in real time
3. The application is packaged into a **Docker** image via a `Dockerfile` (base image `python:3.11-slim`, dependencies installed separately from the code to take advantage of Docker layer caching)
4. The image is deployed on **Hugging Face Spaces**, with port 7860 exposed

## 📁 Project structure

```
tech-stack-advisor/
├── app.py              # Gradio interface + prediction logic
├── train.py             # Model training and encoder generation
├── model.pkl             # Trained scikit-learn model
├── encoders.pkl           # Encoders for categorical variables
├── requirements.txt        # Python dependencies (pinned versions)
├── Dockerfile             # Container image definition
├── .dockerignore           # Files excluded from the Docker build
└── README.md
```

## 🚀 Run locally

```bash
git clone https://github.com/Gildas-EDEN/tech-stack-advisor.git
cd tech-stack-advisor

python -m venv .venv
.venv\Scripts\Activate.ps1     # Windows
# source .venv/bin/activate    # macOS / Linux

pip install -r requirements.txt
python app.py
```
The app is then available at `http://localhost:7860`.

## 🐳 Run with Docker

**Option 1 — Build the image yourself**
```bash
docker build -t tech-stack-advisor .
docker run -p 7860:7860 tech-stack-advisor
```

**Option 2 — Use the pre-built image from Docker Hub**
```bash
docker pull edenakpo/tech-stack-advisor:v2
docker run -p 7860:7860 edenakpo/tech-stack-advisor:v2
```

## 📄 License

This project is licensed under **Apache 2.0**. See the [LICENSE](./LICENSE) file for details.

## 🙏 Acknowledgments

Built on top of an original project by [Gourav Shah](https://www.linkedin.com/in/gouravshah/) (School of DevOps), containerized, debugged, and deployed by me.
