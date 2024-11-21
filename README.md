# CI/CD Pipeline Deployment with Jenkins and Monitoring using DataDog

This project demonstrates an end-to-end CI/CD pipeline for deploying a Flask application using Jenkins. The setup includes Docker containerization and integrates DataDog for observability and monitoring.

## Table of Contents
- Features
- Prerequisites
- Setup Instructions
  - Step 1: Clone Repository
  - Step 2: Setup Flask Application
  - Step 3: Configure Jenkins
  - Step 4: Containerization with Docker
  - Step 5: Monitor with DataDog
- Project Structure
- How to Run
- References

## Features
- CI/CD Pipeline using Jenkins.
- Dockerized deployment of a Flask application.
- Integrated monitoring and logging with DataDog.
- Scalability through containerization and automation.

## Prerequisites
- Python 3.9 or later
- Docker
- Jenkins
- DataDog account with an API key
- Basic knowledge of CI/CD pipelines, Docker, and observability tools.

## Setup Instructions

### Step 1: Clone Repository
Clone the repository to your local machine:

```bash
git clone https://github.com/davidkairu/ci_cd_flask_app.git
cd ci_cd_flask_app
```

### Step 2: Setup Flask Application
Install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Run the Flask application:

```bash
python app.py
```

Access the application at [http://localhost:5001](http://localhost:5001) (or the configured port).

### Step 3: Configure Jenkins
1. Install Jenkins and set up required plugins:
   - Git Plugin
   - Docker Plugin
2. Create a new pipeline job in Jenkins.
3. Use the provided Jenkinsfile in the repository.
4. Ensure Jenkins can run Docker commands by adding the appropriate permissions.

### Step 4: Containerization with Docker
Build the Docker image:

```bash
docker build -t flask-app .
```

Run the Docker container:

```bash
docker run -p 8080:5001 flask-app
```

### Step 5: Monitor with DataDog
Install the DataDog agent:

```bash
DD_AGENT_MAJOR_VERSION=7 DD_API_KEY=<your_api_key> DD_SITE="datadoghq.com" bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_mac_os.sh)"
```

Configure `datadog.yaml`:

```yaml
logs_enabled: true

logs_config:
  logs_enabled: true

logs:
  - type: file
    path: /path/to/your/flask_app.log
    service: flask-app
    source: python
```

Restart the DataDog agent:

```bash
sudo pkill -f datadog-agent
/opt/datadog-agent/bin/agent/agent run &
```

Verify logs in the DataDog dashboard.

## Project Structure
```bash
ci_cd_flask_app/
├── app.py                # Main Flask application
├── Dockerfile            # Docker build file
├── Jenkinsfile           # Jenkins pipeline configuration
├── requirements.txt      # Python dependencies
├── flask_app.log         # Application log file
└── README.md             # Project documentation
```

## How to Run
1. Clone the repository and set up the Flask application.
2. Build and run the Docker container.
3. Configure Jenkins for CI/CD pipeline automation.
4. Install and configure DataDog for monitoring.


## References
- [Flask Documentation](https://flask.palletsprojects.com/)
- [Jenkins Documentation](https://www.jenkins.io/doc/)
- [Docker Documentation](https://docs.docker.com/)
- [DataDog Documentation](https://docs.datadoghq.com/)

