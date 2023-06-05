pipeline {
    agent any 
    tools {
        example 'example'
    }
    environment {
        SCANNER_NAME= tool "sonar-scanner"
        registry= "211223789150.dkr.ecr.us-east-1.amazonaws.com/my-docker-repo"
    }
    stages {
        stage( 'Git CheckOut' ) {
            steps {
                git changelog: false, poll: false, url: 'https://github.com/sahat/hackathon-starter.git'
            }
        }
        stage( 'CodeQuality Analysis with SonarQube' ) {
            steps {
                sh '''' $SCANNER_HOME/bin/sonar-scanner \
                        -Dsonar.url=http://54.232.200.77:9000/ \
                        -Dsonar.login=$sqp_5a03f4395033c714f44cddfabb60fe2a65fcb4bd \
                        -Dsonar.projectName=hackathon-starter \
                        -Dsonar.projectKey=hackathon-starter \
                        -Dsonar.sources=. '''
            }
        }
        stage ('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: ' --scan ./ ', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage ('Docker Image Build') {
            steps {
                script {
                    withDockerRegistry(crednetialsId: 'mydockerhub-credentials') {
                        sh "docker build -t hackathon-starter:latest -f /Dockerfile ."
                        sh "docker tag hackathon-starter:latest nkdh2050/hackathon-starter:latest"
                        sh "docker push nkdh2050/hackathon-starter:latest"
                    }
                }
            }
        }
        stage ('Trivy Security Scan') {
            steps {
                sh "trivy image nkdh2050/hackathon-starter:latest"
            }
        }
        stage ('Helm package') {
            steps {
                sh "helm package nodejs"
            }
        }
        stage ('Helm Install') {
            steps {
                sh "helm upgrade my-release-06 nodejs-0.0.1-tgz"
            }
        }
    }

}
