pipeline {
    agent { label 'my-project' }
//     parameters {
//         choice(name: 'ENV', choices: ['dev', 'test', 'prod',"release"])
//     } 
    stages {
        stage('build') {
            steps {
                echo 'build'
                script{
//                     if (params.ENV == "release") {
                        withCredentials([usernamePassword(credentialsId: 'my-dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                            sh '''
                                docker login -u ${USERNAME} -p ${PASSWORD}
                                docker build -t msami74/bakehouseitismart:v${BUILD_NUMBER} .
                                docker push msami74/bakehouseiti:v${BUILD_NUMBER}
                                echo ${BUILD_NUMBER} > ../build.txt
                            '''
                        }
//                     }
//                     else {
//                         echo "user choosed ${params.ENV}"
//                     }
                }
            }
        }
        stage('deploy') {
            steps {
                echo 'deploy'
//                 script {
//                     if (params.ENV == "dev" || params.ENV == "test" || params.ENV == "prod") {
//                         withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
//                             sh '''
//                                 export BUILD_NUMBER=$(cat ../build.txt)
//                                 mv Deployment/deploy.yaml Deployment/deploy.yaml.tmp
//                                 cat Deployment/deploy.yaml.tmp | envsubst > Deployment/deploy.yaml
//                                 rm -f Deployment/deploy.yaml.tmp
//                                 kubectl apply -f Deployment --kubeconfig ${KUBECONFIG} -n ${ENV}
//                             '''
//                         }
//                     }
//                 }
            }
        }
    }
}
