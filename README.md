# sonar_docker
Docker Compose File for SonarQube Server and Scanner Setup

1. Install Docker on your machine
2. Copy docker-compose.yml and properties folder to your project.
3. Execute docker-compose up on your terminal.

You can check results on http://localhost:9000 sonarqube server

There are 4 services in the compose file running on sonar_net network
1. golang
2. postgres
3. sonarqube
4. newtmitch/sonar-scanner

1. golang service will copy source code into its working directory and execute go test to generate coverage report.
2. postgres service will setup database with named volumes so as to switch from internal h2 database used by sonar.
3. sonarqube will start the sonarqube service that will listen at 9000 port. It will be connected to postgres database and has a healthcheck attached to it that checks the health on the basis of /system/health API from sonar.
4. newtmitch/sonar-scanner will start sonar scanner service once sonarqube server is healthy. This will pick coverage report from go test and after scanning post result to sonarqube server.