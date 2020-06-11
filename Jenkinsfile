pipeline {
    agent any

    stages {
        stage("SCM Checkout") {
        	script { 
        		if (env.BRANCH_NAME == "master") {
        			echo "Cloning the Master Branch"

        			git branch: "${env.BRANCH_NAME}", credentialsId: "fa098c49-fb71-47fe-856a-5900b6551508", url: "https://dakshrajgoyal@github.com/dakshrajgoyal/scala-project.git"

        		} else if (env.BRANCH_NAME == "feature") {
        			echo "Cloning the release branch"

        			git branch: "${env.BRANCH_NAME}", credentialsId: "fa098c49-fb71-47fe-856a-5900b6551508", url: "https://dakshrajgoyal@github.com/dakshrajgoyal/scala-project.git"

        		} else if (env.BRANCH_NAME == "devint") {
        			echo "Cloning the dev_int branch"

        			git branch: "${env.BRANCH_NAME}", credentialsId: "fa098c49-fb71-47fe-856a-5900b6551508", url: "https://dakshrajgoyal@github.com/dakshrajgoyal/scala-project.git"
        		} else {

        			echo "Checkout done in respective branch"
        		}
        	}
        }



        stage('sbt build'){
            steps {
                //sh " ls ui/ "
                //sh " ls && cd ui/ && npm install -g grunt-cli bower yo generator-karma generator-angular && npm install npm -g && npm install grunt-contrib-compass --save-dev && npm audit fix && npm install && grunt build --force "
                //&& cat project/plugins.sbt "
                sh "${tool name: 'Sbt_Home', type:'org.jvnet.hudson.plugins.SbtPluginBuilder$SbtInstallation'}/bin/sbt package "
                sh " pwd " 
            }
        }
    }
}
