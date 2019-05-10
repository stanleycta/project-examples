pipeline {
    agent any

    stages {
        stage('Install Angular') {
            when{
                anyOf{
                    branch 'develop';
                    branch 'preprod';
                    branch 'master';
                    branch 'sonar'
                }
            }
            steps {
                echo 'Building..'
            }
        }
        stage('Build Angular') {
             when{
                anyOf{
                    branch 'develop';
                    branch 'preprod';
                    branch 'master';
                    branch 'sonar'
                }
            }
            steps {
                echo 'Building..'
            }
        }
        
        stage('Build C#') {
             when{
                anyOf{
                    branch 'develop';
                    branch 'preprod';
                    branch 'master'
                }
            }
            steps {
                echo 'Building..'
            }
        }
        
        stage('Code Analysis') {
             when{
                branch 'sonar'                
            }
            steps {
                echo 'Building..'
            }
        }
        
        stage('Angular UnitTest') {
             when{
                anyOf{
                    branch 'develop';
                    branch 'preprod';
                    branch 'master'
                }
            }
            steps {
                echo 'Building..'
            }
        }
        stage('C# UnitTest') {
             when{
                anyOf{
                    branch 'develop';
                    branch 'preprod';
                    branch 'master'
                }
            }
            steps {
                echo 'Testing..'
            }
        }
        stage('ShipToOctopus') {
            when{
                anyOf{
                    branch 'develop';
                    branch 'preprod';
                    branch 'master'
                }
            }
            steps {
                echo 'Deploying....'
            }
        }
        
        stage('HappyDance') {
            steps {
                echo 'Building..'
            }
        }
    }
}
