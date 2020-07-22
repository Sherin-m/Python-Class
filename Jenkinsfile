//def awsCredentials = [[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-test']]

pipeline {
    agent any
    options {
        parallelsAlwaysFailFast()
       // timestamps()
        //withCredentials(awsCredentials)
    }
    stages {
        stage("Maven Build") {
            
            steps {
                git url: 'https://github.com/Sherin-m/maven-project.git'
                sh '''
                mvn clean package
                '''
            }
        }
        stage("Code Testing") {
            steps {
                echo "Cecking file existed or not "
                sh "cd $WORKSPACE/webapp/target/"
                sh "ls -lrt"
            }
        }
        stage("S3  upload") {
            when {
                beforeAgent true
                branch 'master'
            }
            steps {
                sh '''
                echo "aws s3 cp" $WORKSPACE/webapp/target/*.?ar "s3://testing.com/building/"
                echo "somthing is changed"
                '''
           }
        }
        stage("Lmabda Function") {
          steps {
                echo "Lmabda function running "
                echo "nothing is running"
                echo "change something"
                
           }
        }
    }
}
