def jobName = JOB_NAME
def projectName = jobName.split('/')[0]
pipeline{
    agent any
     parameters { 
        choice(name: 'deploy_environment', choices: "DEV\nQA\nSIT\nPROD", description: 'Application deployment environment') 
    }
    stages{
        stage('Checkout'){
        steps{
			bat 'git clean -f'		
			bat 'git reset --hard'  
			bat 'git checkout .'              
            }
           }
        stage('Build'){
            steps{
                 echo "echo Building ${BRANCH_NAME}..."
                 bat "mvn clean install -DskipTests=true"
            }
        }
        stage('Test'){
            steps{
                 echo "echo Testing ${BRANCH_NAME}..."
                 bat "mvn clean test"
            }
        }
        stage('Deploy'){
         steps{
             echo "echo Deploying to ${BRANCH_NAME}..."
             bat "mvn clean deploy -Denvironment=${params.deploy_environment} -DmuleDeploy"
           }   
        }
    }
}

     
 