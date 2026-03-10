node {

    stage('Checkout') {
        checkout scm
    }

    stage('Build') {
        docker.image('composer:2').inside('-u root') {
            sh '''
            cd devops_lav
            composer install
            '''
        }
    }

    stage('Testing') {
        docker.image('php:8.2-cli').inside('-u root') {
            sh 'echo "Ini adalah test"'
        }
    }

    stage('Deploy') {
        docker.image('agung3wi/alpine-rsync:1.1').inside('-u root') {

            sshagent (credentials: ['ssh-prod']) {

                sh 'mkdir -p ~/.ssh'
                sh 'ssh-keyscan -H "$PROD_HOST" > ~/.ssh/known_hosts'

                sh '''
                rsync -rav --delete devops_lav/ ubuntu@$PROD_HOST:/home/ubuntu/prod.kelasdevops.xyz/ \
                --exclude=.env \
                --exclude=storage \
                --exclude=.git
                '''
            }

        }
    }

}