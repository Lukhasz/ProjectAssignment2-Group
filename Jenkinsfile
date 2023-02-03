pipeline {
    agent any

    tools {
        maven "Maven-3.8.7"
        maven "MY_MAVEN"
    }

    stages {
        stage('clean and get latest build') {
            steps {
                sh 'mvn clean -f backend'
                echo 'downloading GitHub project...'
                git branch: 'main', credentialsId: 'dcf05bfd-e0bb-4627-b951-7eb1e10948ea', url: 'https://github.com/lukhasz/ProjectAssignment2-Group.git'
            }
        }

        stage('build') {
            steps {
                echo 'building...'
                sh 'mvn test-compile -f backend'
                echo 'finished building'
            }
        }

        stage ('test') {
            steps {
                echo 'starting test...'
                sh 'mvn surefire:test -f backend'
                echo 'finished test'
            }
        }

        stage('package') {
            steps {
                 echo 'packaging...'
                 sh 'mvn war:war -f backend'
                 echo 'packaged'
                    }
                }
               }

        post {
          always {
                echo 'generating test report....'
                junit 'target/*reports/**/*.xml'
                echo 'test report generated'
                }
            }

         stage ('deploy'){
               steps {
               dir('./backend'){
               sh 'cp ./target/ROOT.war /artifacts'
                 }
                  }
                  }