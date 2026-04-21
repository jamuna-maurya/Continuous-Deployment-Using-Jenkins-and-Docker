# Continuous-Deployment-Using-Jenkins-and-Docker
# 🚀 DevOps Project: Continuous Deployment using Jenkins & Docker

## 📌 Project Title

**Automated CI/CD Pipeline using Jenkins and Docker on Ubuntu 24.04**

---

## 🧠 Objective

To design and implement a CI/CD pipeline that:

* Automatically builds a Docker image
* Deploys a containerized application
* Ensures continuous deployment with Jenkins

---

## 🏗️ Architecture Overview

```
GitHub → Jenkins → Docker Build → Docker Run → Live Application
```

---

## ⚙️ Tech Stack

* **OS:** Ubuntu 24.04
* **CI/CD Tool:** Jenkins
* **Containerization:** Docker
* **Version Control:** GitHub
* **Backend:** Python Flask

---

## 📂 Project Structure

```
myapp/
│── app.py
│── requirements.txt
│── Dockerfile
```

---

## 🧾 Application Code

### 📄 app.py

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Jenkins CI/CD 🚀"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

---

### 📄 requirements.txt

```
flask
```

---

### 📄 Dockerfile

```dockerfile
FROM python:3.10-slim

WORKDIR /app
COPY . .

RUN pip install -r requirements.txt

EXPOSE 5000
CMD ["python", "app.py"]
```

---

## 🔧 Setup Steps

### 1️⃣ Install Jenkins & Docker

* Install Java (OpenJDK 17)
* Install Jenkins
* Install Docker
* Add Jenkins user to Docker group

---

### 2️⃣ Configure Jenkins

* Access Jenkins via: `http://<server-ip>:8080`
* Unlock using admin password
* Install plugins:

  * Pipeline
  * Git
  * Docker Pipeline

---

### 3️⃣ Create Jenkins Pipeline

* Create a new **Pipeline Job**
* Add GitHub repo
* Use pipeline script to:

  * Clone repo
  * Build Docker image
  * Run container

---

## 🔄 Jenkins Pipeline Script

```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        CONTAINER_NAME = "myapp-container"
    }

    stages {

        stage('Clone Code') {
            steps {
                git '<your-github-repo-url>'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker rm -f $CONTAINER_NAME || true'
                sh 'docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }
}
```

---

## ▶️ Execution Steps

1. Push code to GitHub
2. Trigger Jenkins Build
3. Jenkins builds Docker image
4. Container runs automatically

---

## 📸 Screenshots 

### 🔹 1. Jenkins Dashboard

<img width="2066" height="1116" alt="image" src="https://github.com/user-attachments/assets/e2368c70-bf82-426d-b849-f8eb09067719" />



---

### 🔹 2. Build Success Console Output

<img width="2750" height="1304" alt="image" src="https://github.com/user-attachments/assets/2ac2417f-8f57-4dcf-a94a-76f9c9dec94c" />


---

### 🔹 3. Docker Running Container

👉 Command:

```
docker ps
```

<img width="2368" height="260" alt="image" src="https://github.com/user-attachments/assets/68e1ff36-e953-4b75-bb03-bf666c19190b" />


---

### 🔹 4. Application Output (Browser)

👉 URL:
---
http://<server-ip>:5000
---

<img width="2070" height="1128" alt="image" src="https://github.com/user-attachments/assets/25ccb738-4f4b-4e57-8223-8cee82215371" />

---

## ✅ Expected Output

* Jenkins automatically builds Docker image
* Container is deployed successfully
* Application accessible via browser

---

## 🎯 Key Learnings

* CI/CD Pipeline creation
* Jenkins automation
* Docker container lifecycle
* Real-world deployment workflow

---

## 🚀 Future Enhancements

* Integrate Docker Hub (push images)
* Add GitHub Webhooks (auto trigger)
* Deploy on Kubernetes
* Add monitoring (Prometheus + Grafana)

---



## 👨‍💻 Author

**jeny (Beginner to Intermediate Level)**

---
