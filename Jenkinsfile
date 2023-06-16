pipeline{
    agent{label 'node_1'}
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
                
        
          stage('sonar analysis') {
            steps {
                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                withSonarQubeEnv('SONAR_TOKEN') {
                    sh 'mvn clean package sonar:sonar -Dsonar.organization=springpetclinic00 -Dsonar.projectname=springpetclinic -Dsonar.projectkey=springpetclinic'
                }
       }        
  }
 }
}


