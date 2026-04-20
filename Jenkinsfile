pipeline { 
    agent { 
        docker { 
            // Image contenant Maven et Git 
            image 'gitimage' 
            // Pour réutiliser le cache Maven local entre builds 
            args '-v $HOME/.m2:/root/.m2' 
        } 
    } 
 
    stages { 
        stage('Checkout') { 
            steps { 
                // Nettoie proprement le workspace courant (mieux que rm -rf)
                deleteDir() 
                
                // Étape native Jenkins pour cloner (permet à Jenkins de suivre les commits)
                // Assurez-vous de préciser la bonne branche (ex: 'main' ou 'master')
                git branch: 'main', url: 'https://github.com/simoks/java-maven.git' 
            } 
        } 
        stage('Build') { 
            steps { 
                // Affiche le répertoire courant (sans avoir besoin du bloc "script" ou "def")
                echo "Current directory: ${pwd()}" 
                 
                // Comme l'étape native "git" clone directement dans le workspace, 
                // le chemin n'a plus le préfixe "java-maven/". On va directement dans "maven/".
                dir('maven') { 
                    // Exécution des commandes Maven et Java
                    sh 'mvn clean test package' 
                    sh 'java -jar target/maven-0.0.1-SNAPSHOT.jar' 
                } 
            } 
        } 
    } 
}
