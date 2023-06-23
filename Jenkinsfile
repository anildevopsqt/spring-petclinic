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
        }stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "ARTIFACTORY_SERVER",
                    url: 'https://devopsqtasu.jfrog.io/artifactory/',
                    credentialsId: 'jfrog_id'
                )

                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "ARTIFACTORY_SERVER",
                    releaseRepo: 'libs-release',
                    snapshotRepo: 'libs-snapshot'
                )

                rtMavenResolver (
                    id: "MAVEN_RESOLVER",
                    serverId: "ARTIFACTORY_SERVER",
                    releaseRepo: 'libs-release',
                    snapshotRepo: 'libs-snapshot'
        stage('build'){
            tools{jdk 'JDK_17'}
        }
            steps{
                rtMavenRun (
                    tool: 'MAVEN_DEFAULT',
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER"
                )
                
                rtPublishBuildInfo (
                    serverId: "ARTIFACTORY_SERVER"
                )
            }
                
        
            
               }   //sh "mvn ${params.MAVEN_GOAL}"      
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

