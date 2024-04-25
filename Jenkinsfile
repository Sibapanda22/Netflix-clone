pipeline    {
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'Node16'
    }
    environment{
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages{
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('check out from git'){
            steps{
                git branch: 'siba_dev', url: 'https://github.com/Sibapanda22/Netflix-clone.git'
            }
        }
        stage('Sonarqube Analysis'){
            steps{
                withSonarQubeEnv('sonar-server'){
            //         sonar-scanner \
            //          -Dsonar.projectKey=Netflix_clone \
            //          -Dsonar.sources=. \
            //          -Dsonar.host.url=http://52.66.196.136:9000 \
            //          -Dsonar.login=squ_57234af16f909a1ab883ecddaccabb3a0e35e944
            //  }
            sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Netflix_clone \
                    -Dsonar.projectKey=Netflix_clone '''
            }
          }
        }
        stage('Quality Gate'){
            steps{
                scripts{
                waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
             }
            }
          }
        stage('install Dependencies'){
            steps{
                sh 'npm install'
              }
            }
        
        }
    }