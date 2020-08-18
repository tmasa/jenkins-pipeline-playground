properties([
    parameters([
        [$class: 'CascadeChoiceParameter',
            choiceType: 'PT_SINGLE_SELECT',
            name: 'Subproject',
            referencedParameters: 'Project',
            script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: 'return ["error"]'],
                script: [classpath: [], sandbox: false, script: """if(Project.equals("project2")){ return ["both","rfqpub","rfqDetailsPub"] } else { return ["Not Applicable"] }"""]]]
    ])
])

pipeline {
    agent any

    environment {
        MyVar = 'my variable value'
    }

    parameters {
         choice(name: 'Project', choices: ['project1', 'project2'], description: 'Project to be deployed')
     }

    stages {
         stage('Stage0') {
            steps {
                echo "${params.Project}"
                echo "${params.Subproject}"
            }
         }
         stage('Stage1') {
            when {
                expression {
                    params.Project == "project2"
                }
            }
            steps {
                //bat 'set'
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL} with value ${env.MyVar}"
                echo "Deploying ${params.Project}"
                echo "Deploying ${params.Subproject}"
            }
        }
    }
}