node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000'){
        stage('Build'){
            checkout scm
            sh 'npm install'
        }
        stage('Test'){
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval'){
            input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan, "Abort" untuk membatalkan)'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            sh 'sleep 60'
            sh './jenkins/scripts/kill.sh'
        }
    }
}

 


