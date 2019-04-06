pipeline {
    agent any
    //  Change number for quick testing: 001
    
    options{
     retry(3)   
    }
    stages { 
        stage('Angular'){
            options { 
                timestamps() 
            }
            parallel{
                stage('1_Install') {
                    steps {
                        echo 'Installing Angular Packages ...'
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
             when { branch 'develop' }
            
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
        
        stage('Code Analysis') {
            steps {
                echo 'Running SonarQube for static code analysis ...'
            }
        }
        
        stage('Acceptance Test') {
            parallel{
                stage('1_Provisioning'){
                    steps {
                        echo 'Creating resources for acceptance test ...'
                    }
                }
                
                 stage('2_Executing'){
                    steps {
                        echo 'Running the acceptance test ...'
                    }
                }
                
                 stage('3_Evaluating'){
                    steps {
                        echo 'Verifying the result of the acceptance test ...'
                    }
                }
                
                stage('Email Result'){
                    steps {
                        echo 'Emailing test results ...'
                    }
                }
            }
        }
        
        stage('Octopus') {
            parallel{
                stage('Packaging'){
                    steps {
                        echo 'Creating Nuget packages for Octopus....'
                    }
                }
                
                 stage('Uploading'){
                    steps {
                        echo 'Uploading Nuget packages to Octopus....'
                    }
                }
                
                 stage('Releasing'){
                    steps {
                        echo 'Creating Release in Octopus....'
                    }
                }
            }
        }
        
        stage('Dance') {
            steps {
                echo 'Everything went well, so let`s celebrate by dancing ...'
            }
        }
        
         stage('Sequential') {
            environment {
                FOR_SEQUENTIAL = "some-value"
            }
            stages {
                stage('In Sequential 1') {
                    steps {
                        echo "In Sequential 1"
                    }
                }
                stage('In Sequential 2') {
                    steps {
                        echo "In Sequential 2"
                    }
                }
                stage('Parallel In Sequential') {
                    parallel {
                        stage('In Parallel 1') {
                            steps {
                                echo "In Parallel 1"
                            }
                        }
                        stage('In Parallel 2') {
                            steps {
                                echo "In Parallel 2"
                            }
                        }
                    }
                }
            }
        }
    }
}
