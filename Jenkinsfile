pipeline {
    agent { label 'my-project' }
    stages {
        stage('build') {
            steps {
                echo 'build'
                script{
                    
                        withCredentials([usernamePassword(credentialsId: 'my-dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                            sh '''
                                docker login -u ${USERNAME} -p ${PASSWORD}
                                docker build -t msami74/bakehouseiti:v${BUILD_NUMBER} .
                                docker push msami74/bakehouseiti:v${BUILD_NUMBER}
                                echo ${BUILD_NUMBER} > ../build.txt
                            '''
                       
                    }

                }
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
                script {
                    
                        withCredentials([file(credentialsId: 'my-kubeconfig', variable: 'KUBECONFIG')]) {
                            sh '''
                              
                                mv Deployment/deploy.yaml Deployment/deploy.yaml.tmp
                                cat Deployment/deploy.yaml.tmp | envsubst > Deployment/deploy.yaml
                                rm -f Deployment/deploy.yaml.tmp
                                kubectl apply -f Deployment --kubeconfig ${KUBECONFIG}
                            '''
                        }
                  
                }
            }
        }
    }
}
