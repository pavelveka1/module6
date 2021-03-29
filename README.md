# MJC-shcool-module 2. Restfull application
## web service for Gift Certificates
### List of requests:
- 1) Read gift certificate by id, "method": "GET", header: Content-Type: application/json, url: http://localhost:8080/controller/api/giftCertificates/1
- 2) Read all gift certificates, "method": "GET", header: Content-Type: application/json, url: http://localhost:8080/controller/api/gift_certificates
- 3) Read all gift certificates with sort, "method": "GET", header: Content-Type: application/json, url: http://localhost:8080/controller/api/giftCertificates?sortType=id&orderType=desc
- 4) Read gift certificates by tag's name, "method": "GET", header: Content-Type: application/json, url: http://localhost:8080/controller/api/giftCertificates?search=tag&value=спорт&sortType=name&orderType=asc
- 5) Read gift certificates by part of name or description, "method": "GET", header: Content-Type: application/json, url: http://localhost:8080/controller/api/giftCertificates?search=name&value=дел&sortType=id&orderType=asc
- 6) Delete gift certificate by id, "method": "DELETE", header: Content-Type: application/json, url: http://localhost:8080/controller/api/giftCertificates/10
- 7) Update gift certificate , "method": "PUT", header: Content-Type: application/json, url: http://localhost:8080/controller/api/giftCertificates
- 8) Create gift certificate , "method": "POST", header: Content-Type: application/json, url: http://localhost:8080/controller/api/giftCertificates
- 9) Read tag by id, "method": "GET", header: Content-Type: application/json, url: http://localhost:8080/controller/api/tags
- 10) Read all tags, "method": "GET", header: Content-Type: application/json, url: http://localhost:8080/controller/api/tags/1
- 11) Delete tag by id, "method": "DELETE", header: Content-Type: application/json, url: http://localhost:8080/controller/api/tags/10
- 12) Create tag , "method": "POST", header: Content-Type: application/json, url: http://localhost:8080/controller/api/tags

# Task 6 CI-CD
- 0) SonarQube is installed ( version: 8.7.1.42226; port: 9000), jenkins (port: 8081), tomcat (version: 9.0.38; port: 8080) 
- - everything works fine, but test coverage: 0%
- 1) Deploy to container, Role-based Authorization Strategy, SonarQube Scanner for Jenkins plugins are installed
- 2) In the Global config tool:
- - JDK is configured (13.0.2)
- - git is configured
- - SonarQube Scanner is added( name: SonarScanner; install automatically (version 4.6.0.2311))
- - Maven is configured (version 3.6.3)
- 3) System Config:
- - SonarQube (name: SQ, server url: http://localhost:9000; Server authentication token is added)
- 4) Job configuratuin:
- - git (repositiry: https://github.com/pavelveka1/module6.git; branch to  build: */master)
- - build (maven, goals: clean package )
- - Execute SonarQube Scanner ( jdk-13.0.2; Analysis properties: sonar.projectKey=certificates-sonarqube
                                                                 sonar.java.binaries=C:\\Users\\localuser\\AppData\\Local\\Jenkins\\.jenkins\\workspace\\certificateJob)
- - Deploy war/ear to a container (war/ear files: **/*.war; context path: controller; credentials: user from tomcat-users.xml with role "manager-script"; tomcat url: http://localhost:8080/)
- 5) Configuration Jacoco is located in pom.xml file in service module
- - after command: mvn clean package I had a note: [INFO] --- jacoco-maven-plugin:0.8.3:report (jacoco-site) @ service ---
                                                   [INFO] Loading execution data file C:\Users\HP\tempory\MJC-Module2\giftcertificate\service\target\coverage-reports\jacoco-unit.exec
                                                   [INFO] Analyzed bundle 'service' with 11 classes
