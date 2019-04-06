pipeline {
    agent any
    //  Change number for quick testing: 012
    
    options{
        retry(3)   
    }
    stages { 
        stage('Angular'){
            options { 
                timestamps() 
            }
            when { 
                anyOf { 
                    branch 'master'; 
                    branch 'develop' 
                } 
            }
            parallel{
                stage('1_Install') {
                    steps {
                        echo 'Installing Angular Packages ...'
                        echo 'Building Angular ...'                       
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Service | Where-Object Status -eq "Stopped" | Sort-Object Name | Format-table -autosize

                            Write-Host("GIT_AUTHOR_NAME : $ENV:GIT_AUTHOR_NAME")
                            Write-Host("GIT_AUTHOR_EMAIL : $ENV:GIT_AUTHOR_EMAIL")
                            Write-Host("GIT_COMMITTER_NAME : $ENV:GIT_COMMITTER_NAME") 
                            Write-Host("GIT_COMMITTER_EMAIL : $ENV:GIT_COMMITTER_EMAIL") 
               
                            Write-Host("BUILD_NUMBER : $ENV:BUILD_NUMBER")
                            Write-Host("BUILD_ID : $ENV:BUILD_ID")
                            Write-Host("BUILD_URL : $ENV:BUILD_URL")
                            Write-Host("NODE_NAME : $ENV:NODE_NAME")
                            Write-Host("JOB_NAME : $ENV:JOB_NAME")
                            Write-Host("BUILD_TAG : $ENV:BUILD_TAG")
                            Write-Host("JENKINS_URL : $ENV:JENKINS_URL")
                            Write-Host("EXECUTOR_NUMBER : $ENV:EXECUTOR_NUMBER")
                            Write-Host("WORKSPACE : $ENV:WORKSPACE")
                            Write-Host("GIT_BRANCH : $ENV:GIT_BRANCH")
                            Write-Host("GIT_COMMIT : $ENV:GIT_COMMIT")
                            
                            $List = Get-ChildItem -Path $ENV:WORKSPACE -Recurse
                            $List | Where-object Mode -Like "d*" | Select-Object Name, Parent, CreationTime, CreationTimeUtc, Attributes
                            
                        ''')
                    }                 
                    
                }
                stage('2_Verification') {
                    steps {
                        echo 'Verifying folders/files creation ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Service | Where-Object Status -eq "running" | Sort-Object Name | Format-table -autosize
                        ''')
                    }
                }
            }
        }
        stage('Build C#') {
            options { 
                timestamps() 
            }
            when { 
                anyOf { 
                    branch 'master'; 
                    branch 'develop' 
                } 
            }
            steps {
                echo 'Calling dotnet to build solution'
                powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Service | Where-Object Status -eq "Stopped" | Sort-Object Name | Format-table -autosize
                        ''')
            }
        }
        
        stage('Unit Test'){
          options { 
                timestamps() 
            }
            when { 
                anyOf { 
                    branch 'master'; 
                    branch 'develop' 
                } 
            }
            parallel{            
                stage('1_Angular') {
                    steps {
                        echo 'Running Angular UnitTest ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Process | Sort-Object | Select-Object -First 20 | Format-table -autosize
                        ''')
                    }
                }
                stage('2_C#') {
                    steps {
                        echo 'Running C# UnitTest ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Process | Sort-Object | Select-Object -Last 30 | Format-table -autosize
                        ''')
                    }
                }
                
                stage('Email') {
                    steps {
                        echo 'Sending out Unit Test results ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Process | Sort-Object | Select-Object -First 20 | Format-table -autosize
                        ''')
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            parallel{            
                stage('1_Verification') {
                    steps {
                        echo 'Running Angular UnitTest ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Process | Sort-Object | Format-table -autosize
                        ''')
                    }
                }
                stage('2_GetResult') {
                    steps {
                        echo 'Running C# UnitTest ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Process | Sort-Object | Select-Object -Last 20 | Format-table -autosize
                        ''')
                    }
                }
                
                stage('Email') {
                    steps {
                        echo 'Sending out email of code analysis availability ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                        ''')
                    }
                }
            }
        }
        
        stage('Acceptance Test') {
            parallel{
                stage('1_Provisioning'){
                    steps {
                        echo 'Creating resources for acceptance test ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Service | Sort-Object Name | Select-Object -First 5 | Format-table -autosize
                        ''')
                    }
                }
                
                 stage('2_Executing'){
                    steps {
                        echo 'Running the acceptance test ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Service | Sort-Object Name | Format-table -autosize
                        ''')
                    }
                }
                
                 stage('3_Evaluating'){
                    steps {
                        echo 'Verifying the result of the acceptance test ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                        ''')
                    }
                }
                
                stage('Email'){
                    steps {
                        echo 'Sending out email of Acceptance test results ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                        ''')
                    }
                }
            }
        }
        
        stage('Octopus') {
            parallel{
                stage('1_Packaging'){
                    steps {
                        echo 'Creating Nuget packages for Octopus ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Process | Sort-Object | Select-Object -First 20 | Format-table -autosize
                        ''')
                    }
                }
                
                 stage('2_Uploading'){
                    steps {
                        echo 'Uploading Nuget packages to Octopus ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Service | Sort-Object Name | Select-Object -First 50 | Format-table -autosize
                        ''')
                    }
                }
                
                 stage('3_Releasing'){
                    steps {
                        echo 'Creating Release in Octopus ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                            Get-Process | Sort-Object | Select-Object -First 5 | Format-table -autosize
                        ''')
                    }
                }
                
                stage('Email'){
                    steps {
                        echo 'Sending out email release is available in Octopus ...'
                        powershell(returnStatus: true, script: '''
                            $(Get-Date)
                        ''')
                    }
                }
            }
        }
        
        stage('Dance') {
            steps {
                echo 'Everything went well, so let`s celebrate by dancing ...'
            }
        }         
    }
}
