# GMC_CI

* Prerequisite : 
  * run the command : sudo docker-compose -f tools.yml up
  * add JDK installations in Jenkins : jdk 11 and jdk 8

# 1. Docker images : 
* backend : https://hub.docker.com/repository/docker/khouloud123456/backend 
* frontend  : https://hub.docker.com/repository/docker/khouloud123456/frontend

# 2. Stage('Unit tests') : using Jest and Enzyme 
Two basic unit tests were created in Movies_App/frontend/src/__tests__

# 3. Stage('Code quality inspection')
* a Jenkins freestyle job named Sonarqube must be created using the plugin SonarQube Scanner for Jenkins.
* Configuration : 
  * Source code Management : https://github.com/khouloudRb/Movies_App.git
  * JDK : jdk11
  * *Analysis properties* : 
  - sonar.host.url=http://localhost:9000
  - sonar.projectKey=React_APP
  - sonar.login=admin
  - sonar.password=admin
  - sonar.sources=/var/lib/jenkins/workspace/Sonarqube

# 4. Stage('Katalon tests') : 
* a jenkins freestyle job named Katalon2 must be created using the plugin Katalon TestOps Plugin.
* Configuration :
  * Source code Management : https://github.com/khouloudRb/katalon2.git 
  * *Build section* : 
  - Download Katalon Studio version : 8.0.5
  - Command arguments : 
-retry=0 -apiKey="*****" -testSuitePath="Test Suites/Simple test suite" -executionProfile="default" -browserType="Chrome (headless)" --config -webui.autoUpdateDrivers=true 
