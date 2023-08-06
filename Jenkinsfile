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
    steps {
        script {
            sh 'npm install && npm run build'
            sh "npm install -g --silent gh-pages@2.1.1"
            sh "git clone https://github.com/WahyuriN/WahyuriN.github.io.git deploy"
            sh 'cp -R build/* deploy/'
            dir('deploy') {
                sh "git config --global user.email 'ci@jenkins.com' && git config --global user.name 'ci-auto'"
                sh "gh-pages --dotfiles --message '[skip ci] Updates' --dist ."
                sh 'git add .'
                sh 'git commit -m "Deploy to GitHub Pages"'
                sh 'git push origin main'
            }
            sh 'sleep 60'
            sh './jenkins/scripts/kill.sh'
        }
    }
}
    }   
}

 


