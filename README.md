# Jenkins + Docker CI pipeline

Declarative pipeline that clones the repo, builds a Docker image, verifies it,
and sends an email if any stage fails.

## Stages
1. Clone: `checkout scm`
2. Build Docker image: `docker build -t jenkins-ci-demo:$BUILD_NUMBER .`
3. Verify image: runs the image and imports Flask
4. Post: `mail` step on failure

## Notification
Email through Gmail SMTP (`smtp.gmail.com:465`, SSL, app password stored in
Jenkins system settings, never in this repo).
