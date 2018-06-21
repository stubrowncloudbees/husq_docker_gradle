pipeline {
    agent {
        node {
            label 'gradle'
            }
        }
    stages {
        stage('build') {
            steps {
                container('gradle') {
                    sh 'id'
                    sh 'ls && pwd'
                    sh './gradlew build'
                    
                    
                }
            }
        }
        
    }
}
