pipeline{
    agent{label 'JDK_17'}
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
                withSonarQubeEnv('SONAR_token') {
                    sh 'mvn clean package sonar:sonar -Dsonar.organization=springpetclinic1'
                }
       }        
  }
 }
}


