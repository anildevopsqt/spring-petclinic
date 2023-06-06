pipeline{
    agent{label 'JDK_17'}
    triggers{cron ('H/15 * * * *')}
    parameters{
        string (name:'MAVEN_GOAL', defaultValue:'package', description:'maven goal')
    }

stages{
        stage('vcs'){
            steps {
            git branch: 'main', url: 'https://github.com/anildevopsqt/spring-petclinic.git'
            }
        }
        stage('build'){
            tools{jdk 'JDK_17'}
            steps {
            sh "mvn ${params.MAVEN_GOAL}"
          }
        }
                
        
        stage('post build'){
            steps{
                archiveArtifacts artifacts: '**/*.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/*.xml',
                  allowEmptyResults: true
           }
       
        }
    }
}


