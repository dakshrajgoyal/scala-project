
pipeline {
    agent any

    stages {
        stage("SCM Checkout") {
            steps {
                script {
                    
                    echo "${STAGE_NAME}"
                    
                    if (env.BRANCH_NAME == "master") {
                        echo "Cloning the Master Branch"

                        git branch: "${env.BRANCH_NAME}", credentialsId: "f05a7061-a0bc-4954-b42b-1d8a3674141c", url: "https://dakshrajgoyal@github.com/dakshrajgoyal/scala-project.git"

                    } else if (env.BRANCH_NAME == "feature") {
                        echo "Cloning the release branch"

                        git branch: "${env.BRANCH_NAME}", credentialsId: "f05a7061-a0bc-4954-b42b-1d8a3674141c", url: "https://dakshrajgoyal@github.com/dakshrajgoyal/scala-project.git"

                    } else if (env.BRANCH_NAME == "devint") {
                        echo "Cloning the dev_int branch"

                        git branch: "${env.BRANCH_NAME}", credentialsId: "f05a7061-a0bc-4954-b42b-1d8a3674141c", url: "https://dakshrajgoyal@github.com/dakshrajgoyal/scala-project.git"
                    
                    } else {
                        
                        echo "Checkout done in respective branch"
                        
                    }
                }
            }
            post {
                success {
                    emailext (
                        GIT_EMAIL=$(git --no-pager show -s --format='%ae' $GIT_COMMIT)
                        to: '${GIT_EMAIL}',           
                        subject: "Status of pipeline: Success ${currentBuild.fullDisplayName}",
                        body: """FINISHED Successfully: "${STAGE_NAME}" Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]" (${env.BUILD_URL}console)"""
                    )

                }

                failure {
                    emailext (
                        to: '${foo}',           
                        subject: "Status of pipeline: Failure ${currentBuild.fullDisplayName}",
                        body: """Failed: "${STAGE_NAME}" Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]" (${env.BUILD_URL}console)"""            
                    )
                }
            }
        }

        stage('sbt build') {
            steps {
                sh "echo '${STAGE_NAME}' "
                //sh " ls ui/ "
                //sh " ls && cd ui/ && npm install -g grunt-cli bower yo generator-karma generator-angular && npm install npm -g && npm install grunt-contrib-compass --save-dev && npm audit fix && npm install && grunt build --force "
                //&& cat project/plugins.sbt "
                sh "${tool name: 'Sbt_Home', type:'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'}/bin/sbt package"
                sh "pwd"
            }
            
            post {
                success {
                    emailext (
                        to: '$DEFAULT_RECIPIENTS',           
                        subject: "Status of pipeline: Success ${currentBuild.fullDisplayName}",
                        body: """FINISHED Successfully: "${STAGE_NAME}" Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]" (${env.BUILD_URL}console)"""
                    )

                }

                failure {
                    emailext (
                        to: '$DEFAULT_RECIPIENTS',           
                        subject: "Status of pipeline: Failure ${currentBuild.fullDisplayName}",
                        body: """Failed: "${STAGE_NAME}" Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]" (${env.BUILD_URL}console)"""            
                    )
                }
            }
        }
    }
    
    post {
        success {
            emailext (
                to: '$DEFAULT_RECIPIENTS',           
                subject: "Status of Overall pipeline:  ${currentBuild.fullDisplayName}",
                body: """FINISHED Successfully: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]" (${env.BUILD_URL}console)"""
            )

        }

        failure {
            emailext (
                to: '$DEFAULT_RECIPIENTS',           
                subject: "Status of Overall pipeline: ${currentBuild.fullDisplayName}",
                body: """Failed: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]" (${env.BUILD_URL}console)"""            
            )
        }
    }
}
