pipeline {
    agent any
    //  Change number for quick testing: 001
    stages { 
        stage('Angular'){
            parallel{
                stage('1_Install') {
                    steps {
                        echo 'Installing Angular Packages ...'
                    }
                    
                    steps {
                        echo 'Building Angular ...'
                    }
                }
                stage('2_Verification') {
                    steps {
                        echo 'Verifying folders/files creation ...'
                    }
                }
            }
        }
        stage('Build C#') {
            steps {
                echo 'Building..'
            }
        }
        
        stage('Unit Test'){
            parallel{            
                stage('1_Angular') {
                    steps {
                        echo 'Running Angular UnitTest ...'
                    }
                }
                stage('2_C#') {
                    steps {
                        echo 'Running C# UnitTest ...'
                    }
                }
            }
        }
        stage('ShipToOctopus') {
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
