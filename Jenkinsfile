pipeline {
    agent any

    stages {
        stage('Obtener el repositorio') {
            steps {
                git branch: 'main', url: 'https://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@github.com/girovic/taller-openwebinars.git'
            }
        }
        stage('Construir la documetación') {
            steps {
                sh "doxygen"
            }
            
        }

        stage('Archivar la documentación') {
            steps {
                sh "zip documentation.zip -r html/*"
            }
        }
        stage('Análisis estático') {
            steps {
                sh 'make cppcheck-xml'
               // recordIssues(tools: [cppCheck(pattern: 'reports/cppcheck/*.xml')])
               recordIssues qualityGates: [[threshold: 1, type: 'TOTAL', unstable: false]], tools: [cppCheck(pattern: 'reports/cppcheck/*.xml')]
            }
        }
        stage('Tests unitarios') {
            steps {
                sh 'make tests-xml'
                junit 'reports/cmocka/*.xml'
            }
        }

    }
    post {
        success {
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'html/', reportFiles: 'files.html', reportName: 'Documentación', reportTitles: ''])
            archive "documentation.zip"
        }
    }
}

