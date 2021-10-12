# NOTES 12-Oct-2021
# SOURCE: https://docs.microsoft.com/en-gb/azure/spring-cloud/quickstart?tabs=Azure-CLI&pivots=programming-language-java

# spring.io
https://start.spring.io/#!type=maven-project&language=java&platformVersion=2.5.3&packaging=jar&jvmVersion=1.8&groupId=com.example&artifactId=hellospring&name=hellospring&description=Demo%20project%20for%20Spring%20Boot&packageName=com.example.hellospring&dependencies=web,cloud-eureka,actuator,cloud-starter-sleuth,cloud-starter-zipkin,cloud-config-client

# Repository
https://github.com/pietronromano/springopsmanifests 
# Git repo for app configuration
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/pietronromano/springopsmanifests.git
git push -u origin main

# PAT
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

# Create Spring cloud instance in the portal
# Build locally
az login
az account list -o table

mvn clean package -DskipTests

# Env variables
APP_NAME=hellospring
SERVICE_INSTANCE=pnrspringopsmanifests
RG=jrg-asclab

# Create the app
az spring-cloud app create -n $APP_NAME -s $SERVICE_INSTANCE -g $RG --assign-endpoint true --runtime-version Java_11

# Deploy the jar file: note the double \\ in the folder path
az spring-cloud app deploy -n $APP_NAME -s $SERVICE_INSTANCE -g $RG --artifact-path target\\hellospring-0.0.1-SNAPSHOT.jar

# Stream logs
az spring-cloud app logs -n $APP_NAME -s $SERVICE_INSTANCE -g $RG --lines 100 -f
