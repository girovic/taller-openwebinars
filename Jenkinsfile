pipeline {
        agent any
        stages {
                stage('Obtener el repo') {
                      steps {
                             git branch: 'main', url: 'https://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@github.com/girovic/taller-openwebinars.git'
                            }
                     }
                stage('Generar la documentacion') {
                       steps {
                             sh "doxygen"
                            }

                     }       
                post {
                      publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'html/', reportFiles: 'files.html', reportName: 'Documentación', reportTitles: ''])

                    }                    

        }
}