node {

    stage('Checkout') {
        checkout scm
    }

    stage('Build') {
        docker.image('shippingdocker/php-composer:7.4').inside('-u root') {
            sh 'composer install'
        }
    }

    stage('Testing') {
        docker.image('ubuntu').inside('-u root') {
            sh 'echo "Ini adalah test"'
        }
    }

}