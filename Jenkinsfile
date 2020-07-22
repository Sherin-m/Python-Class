//def awsCredentials = [[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-test']]

pipeline {
    agent { node { label 'Master' }}
    options {
         parallelsAlwaysFailFast()
        //timestamps()
        //withCredentials(awsCredentials)
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'Env', choices: ['Dev', 'Staging', 'Prod'], description: 'Choice your ENV')

        string(name: 'BranchName', defaultValue: 'dev-ui', description: 'branch name')
    }
    
    stages {
        stage("Maven Build") {
            when { branch "${params.BranchName}"}
            
            steps {
                
                git url: 'https://github.com/Sherin-m/maven-project.git'
                sh '''
                mvn clean package
                '''
            }
        }
        stage("Code Testing") {
            options {
                timeout(time: 1, unit: 'MINUTES') 
            }
            steps {
                
                echo "Cecking file existed or not "
                echo "$WORKSPACE"
                sh "cd $WORKSPACE/webapp/target/"
                sh "pwd"
                sh "ls -lrt"
            }
        }
        stage("S3  upload") {
            steps {
                sh '''
                echo "aws s3 cp" $WORKSPACE/webapp/target/*.?ar "s3://testing.com/building/"
                echo "somthing is changed"
                '''
           }
        }
        stage("Lmabda Function") {
             input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    choice(name: 'Approval', choices: ['Apprvoed', 'Rejected'], description: '?')
                }
            }
          steps {
                echo "Lmabda function running"
                echo "nothing is running"
                echo "change something"
                
           }
        }
    }
}
