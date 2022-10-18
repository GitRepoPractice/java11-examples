node('jdk11-mvn3.8.6') {
    stage('git') {
        git 'https://github.com/GitRepoPractice/java11-examples.git'
    }
    stage('build') {
        sh '''
            echo "PATH={$PATH}"
            echo "M2_HOME=${M2_HOME}"
        '''
        sh '/usr/local/apache-maven-3.8.6/bin/mvn clean package'
    }
}