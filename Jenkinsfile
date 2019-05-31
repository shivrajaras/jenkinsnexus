pipeline {
    agent { label 'java8' }
    environment {
        EMAIL_RECIPIENTS = 'shivu483@gmail.com'
    }
    stages {
        stage('Build ') {
            steps {
                // Run the maven build
                script {
                        echo 'Pulling...' + env.BRANCH_NAME
                        sh "mvn clean install package"
                        def pom = readMavenPom file: 'pom.xml'

                        echo  "groupId ${pom.groupId}"
                        echo  "artifactId ${pom.groupId}"
                        echo  "verstion ${pom.version}"
            }
        }
    }
}
}
