pipeline {
    agent { label 'jdk11-mvn3.8.6' }
    triggers { 
        cron('45 23 * * 1-5')
        pollSCM ('*/5 * * * *') 
    }
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'This is maven goal')
        choice(name: 'BRANCH_TO_BUILD', choices: ['declarative', 'master', 'scripted'], description: 'Branch to build')
    }
    stages {
        stage ('scm') {
            steps {
                git url: 'https://github.com/GitRepoPractice/java11-examples.git', branch: "${params.BRANCH_TO_BUILD}"
            }
        }
        stage ('build') {
            steps {
                sh "/usr/local/apache-maven-3.8.6/bin/mvn ${params.MAVEN_GOAL}"
            }
        }
    }
    post {
        always {
            mail from: "devops@qt.com",
                  to : "team@qt.com",
                  subject: "Status of the pipeline ${currentBuild.fullDisplayName}",
                  body: "${env.BUILD_URL} has a result ${currentBuild.result}" 
        }
    }
}


