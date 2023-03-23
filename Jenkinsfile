    agent none
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'python:3.8-alpine3.16'
                }
            }
            steps {
                sh 'python3.8 -m py_compile sources/prog.py sources/calc.py'
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
        
        stage('Test') {
            agent {
                docker {
                    image 'grihabor/pytest'
                }
            }
            steps {
                sh 'pytest -v --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit "test-reports/results.xml"
                }
            }
        }
    }
}```

Ce script compile les fichiers `prog.py` et `calc.py` en utilisant une image Docker `python:3.8-alpine3.16`. Il stocke ensuite les résultats compilés dans une variable nommée `compiled-results`. 

La deuxième étape du script exécute les tests en utilisant une image Docker `grihabor/pytest`. Les résultats sont stockés dans un fichier XML nommé `results.xml`. Enfin, le script affiche les résultats des tests en utilisant la commande `junit`.
