node {
    stage('Preparation') {
        //git credentialsId: 'ubuntukey', url: 'git@github.com:JonasKs/gildedrose.git'
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'ubuntukey', url: 'git@github.com:JonasKs/gildedrose.git']]])
    }
    stage('Build'){
        sh 'docker run -i --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn install'
    }
    stage('Results'){
        junit '**/target/surefire-reports/TEST-*.xml'
        archive 'target/*.jar'
    }
    stage('javadoc'){
        sh 'docker run -i --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn site'
        archive 'target/gildedrose-*.jar'
    }
}
