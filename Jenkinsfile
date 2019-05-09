pipeline {
  agent { docker { image 'php:7.3.5-alpine' } }
  environment {HOME = '/tmp'} 
  stages {
    // First stage , get files from your GitHub repository.
    stage('Git'){
        steps{
            checkout scm
        }
    }
    stage('Get Composer'){
        steps{
            sh """
            php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/tmp --filename=composer  
            """
        }
    }
    stage('Install Requirements With Composer'){
        steps{
            sh "php /tmp/composer install"
        }
    }
    stage('Phpunit'){
        steps{
            sh 'vendor/bin/phpunit tests'
        }
    }
  }
}
