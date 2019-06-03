pipeline {
    agent any
    environment {
        EMAIL_RECIPIENTS = 'shivu483@gmail.com'
    }
    stages {
        stage('test and verify ') {
            steps {
                script {
                        git credentialsId: 'git', url: 'https://github.com/shivrajaras/jenkinsnexus.git'
                        echo 'Pulling...' + env.BRANCH_NAME
                        sh "mvn clean install package"
                        def pom = readMavenPom file: 'pom.xml'
                        echo  "groupId ${pom.groupId}"
                        echo  "artifactId ${pom.artifactId}"
                        echo  "verstion ${pom.version}"
            }
        }
    }
            stage('upload ') {
            steps {
                script {
                        sh "mvn deploy"
                        echo " uploaded successfully"
                       
            }
        }
    }
                stage('deploy ') {
            steps {
                script {
                        def pom = readMavenPom file: 'pom.xml'
                        sh "sudo ./home/shivaraja/deploy.sh java ${pom.groupId} ${pom.artifactId} ${pom.version}"
                        echo " uploaded successfully"
                       
            }
        }
    }
}
}
