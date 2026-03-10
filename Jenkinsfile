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
            sh 'echo "Testing stage berjalan"'
        }
    }

}