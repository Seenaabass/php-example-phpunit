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
    stage('Get PhpUnit'){
        steps{
            sh """
            wget -O phpunit https://phar.phpunit.de/phpunit-8.phar
            chmod +x phpunit
            """
        }
    }
     stage('Run PhpUnit'){
        steps{
            sh "./phpunit tests/EmailTest"
        }
    }
  }
}
