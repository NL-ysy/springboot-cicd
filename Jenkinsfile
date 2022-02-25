pipeline {
  agent none
  stages {
    stage('build') {
      steps {
        echo 'build bone1'
        sh './gradlew clean build' }
      }
    }

    stage('upload') {
      steps {
        echo 'upload done2'
        sh 'aws s3 cp build/libs/application.war s3://springboot-cicd-nlyung/application.war --region us-west-1'
      }
    }

    stage('deploy') {
      steps {
        echo 'deploy done3'
        sh 'aws elasticbeanstalk create-application-version --region us-west-1 --application-name spring-cicd-nlyung 
        --version-label ${BUILD_TAG} --source-bundle S3Bucket="springboot-cicd-nlyung",S3Key="application.war"' 
        sh 'aws elasticbeanstalk update-environment --region us-west-1 --environment-name Springcicdnlyung-env 
        --version-label ${BUILD_TAG}' 
            
      }
    }

  }
