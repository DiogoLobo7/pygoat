pipeline {
    agent any
    environment {
        SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
        SEMGREP_PR_ID = "${env.CHANGE_ID}"
    }
    stages {
        stage('Semgrep-Scan') {
            steps {
                // Instala o Semgrep
                sh 'pip3 install semgrep'
                // Executa o scan e salva os resultados em um arquivo JSON
                sh 'semgrep ci --json > semgrep_results.json'
            }
        }
        stage('Upload Results to Semgrep Cloud') {
            steps {
                // Envia os resultados do scan para a nuvem do Semgrep
                sh 'curl -X POST -H "Authorization: Bearer $SEMGREP_APP_TOKEN" -F "results=@semgrep_results.json" https://semgrep.dev/api/reports'
            }
        }
    }
}
