pipeline{
    agent any
    tools{
        maven 'M2_HOME'
    }
    stages{
        stage('maven build'){
            steps{
                sh 'mvn clean install package'
            }

        }
         stage('upload artifact'){
             steps{
                 script{
                     def mavenPom = readMavenPom file: 'pom.xml'
                nexusArtifactUploader artifacts: 
                [[artifactId: "${mavenPom.artifactId}",
                classifier: '', 
                file: "target/${mavenPom.artifactId}-${mavenPom.version}.${mavenPom.packaging}", 
                type: "${mavenPom.packaging}"]], 
                credentialsId: 'nexusID', 
                groupId: "${mavenPom.groupId}", 
                 nexusUrl: '139.144.31.245:8081', 
                  nexusVersion: 'nexus3', 
                   protocol: 'http', 
                    repository: 'biom', 
                     version: "${mavenPom.version}"
                 }
            }


        }
         stage('list the dir'){
            steps{
                sh 'ls'
            }

        }
    }
}