## SonarQube Installation:
Step1->install java
````
sudo apt-get update && sudo apt-get install openjdk-11-jdk
````
step2->
````
apt install unzip
````
**switch to user root:**
````
adduser sonarqube
````
**switch to user sonarqube:**
````
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip
````
````unzip *
````
**switch to user root:**
````
chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424

chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424
````
**switch to user sonarqube:**
````
cd sonarqube-9.4.0.54424/bin/linux-x86-64/
````
````
./sonar.sh start
````
