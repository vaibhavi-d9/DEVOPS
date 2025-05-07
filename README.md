# DEVOPS

pipeline{
 agent any
 tools{
 maven 'Maven'
 
 }
 stages{
 stage('clone the repository'){
 steps{
 git url: 'https://github.com/devisar/Exp2.5.git'
 }
 }
 stage('Build the code'){
 steps{
 bat 'mvn clean install'
 }
 }
 stage('deploy to tomcat'){
 steps{
 deploy adapters: [tomcat9(credentialsId: 'Deploy', path: '', url: 'http://localhost:8080')], 
contextPath: null, war: '**/*.war' 
 }
 }
