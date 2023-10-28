pipeline {
    agent {
        node {
            label 'slave-node'
        }
    }

tools {
    mvn 'maven3'
}

options{
    buildDiscarder(logRotator(numToKeepStr:'3'))
    retry(3)
    timestamps()
}

parameters{
    string(name: "branch", defaultValue: "main", description: "select the branch")
    choice(name: "Environment", choice:'dev/ntest/nprod', description: "select the environment")
}

stages {
    stage("pull code"){
        steps {
            git branch: ${branch_name} credntialsId: 67ca7455-3a0f-4a29-86a8-ee74abc7dc72 url: https://github.com/sand9989/Maven.git 
        }
    }
}
    stage("maven deploy"){
        when { ${Environment} == "dev"}
        steps{
            sh "mvn clean deploy -Dmaven.test.skip=true"
        }
    }

    stage("maven test report"){
        steps{
            sh "mvn surefire-report:report"
        }
    }
}

