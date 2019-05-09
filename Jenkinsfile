pipeline {
  // Using docker image with lite version linux with php.
  agent { docker { image 'php:7.3.5-alpine' } }
  // Will execute everything at tmp folder.
  environment {HOME = '/tmp'} 
  stages {
    // Get files from your GitHub repository.
    stage('Git'){
        steps{
            checkout scm
        }
    }
    // Install Composer
    // Composer is a tool for dependency management in PHP. 
    // It allows you to declare the libraries your project depends on and it will manage (install/update) them for you.
    stage('Get Composer'){
        steps{
            sh """
            php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/tmp --filename=composer  
            """
        }
    }
    // Will use composer.json file to install dependencies
    stage('Install Requirements With Composer'){
        steps{
            sh "php /tmp/composer install"
        }
    }
    //Will run phpunit on all test files in tests folder
    stage('Phpunit'){
        steps{
            sh 'vendor/bin/phpunit tests'
        }
    }
  }
}
