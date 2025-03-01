pipeline {
    agent any
    tools {
        maven 'maven-jenkins'  // Nom défini dans Global Tool Configuration
    }
    triggers {
        githubPush()  // Déclenche automatiquement le pipeline à chaque push sur GitHub
    }


    stages {
        stage('Checkout') {
            steps {
                echo '📥 Clonage du dépôt...'
                git branch: 'main', url: 'https://github.com/ZahirOuma/helloWorld.git'
            }
        }

        stage('Build') {
            steps {
                echo '🔧 Compilation du projet...'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Exécution des tests...'
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Déploiement de l\'application...'
                script {
                    def jarFile = sh(script: "ls target/*.jar", returnStdout: true).trim()
                    if (jarFile) {
                        sh "java -jar ${jarFile}"
                    } else {
                        error "🚨 Aucun fichier .jar trouvé dans le dossier target/"
                    }
                }
            }
        }
    }
}
