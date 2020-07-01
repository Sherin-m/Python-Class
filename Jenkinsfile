//def awsCredentials = [[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-test']]

pipeline {
    agent any
    options {
        parallelsAlwaysFailFast()
        timestamps()
        //withCredentials(awsCredentials)
    }
    stages {
        stage("Maven Build") {
            
            steps {
                sh '''
                //cd $WORKSPACE
                //pwd
               // echo "/opt/maven/apache-maven-3.6.3/bin/mvn clean install"
               echo "nothing is changeed"
                '''
            }
        }
        stage("Code Testing") {
            steps {
                echo "Here we are running code test"
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
