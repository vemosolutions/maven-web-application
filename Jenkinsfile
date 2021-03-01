node {
    
    def mvnHome = tool "maven 3.6.3"
    def javaHome = tool 'Java 1.8'
    
    stage('codeCheckOut'){
        git branch: 'development', credentialsId: '8da5d983-9e36-45c8-9cd7-a45455cca6b3', url: 'https://github.com/vemosolutions/maven-web-application.git'
    }
    
    stage('mavenBuild'){
        //sh "${mavenHome}/bin/mvn clean package"
        sh "JAVA_HOME=$javaHome $mvnHome/bin/mvn clean package"
    }
    
    stage('executeSonar'){
        sh "JAVA_HOME=$javaHome $mvnHome/bin/mvn sonar:sonar"
    } 
    
    stage('uploadToNexus'){
        sh "JAVA_HOME=$javaHome $mvnHome/bin/mvn deploy"
    }
    
    stage('deployToAppServer'){
        //cp  "
        //Files.copy("/Users/apple/.jenkins/workspace/vemo-pipeline-dev/target/maven-web-application.war","/Library/tomcat/webapps/")
        sh "cp /Users/apple/.jenkins/workspace/vemo-pipeline-dev/target/maven-web-application.war /Library/tomcat/webapps/"
        
    }
    
    stage('sendEmail'){
        emailext body: '''From
            Vemo Solutions.
            Guntur''', subject: 'Build Satus', to: 'pstjayakar@gmail.com,gurumadala@gmail.com'
    }
    
}
