pipeline {
    agent any

    tools {
        maven "Maven-3.8.7"
    }

    stages {
        stage('clean and get latest build') {
            steps {
                sh 'mvn clean -f backend'
                echo 'downloading GitHub project...'
                git branch: 'main', credentialsId: 'PUBLIC_KEY', url: 'https://github.com/lukhasz/ProjectAssignment2-Group.git'
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
        
        stage ('deploy'){
            steps {
               dir('./backend') {
               sh 'cp ./target/ROOT.war /artifacts'
			   }
            }
        }
	}
	
	post {
        always {
            echo 'generating test report....'
            junit '**/*reports/**/*.xml'
            echo 'test report generated'
        }
    }
}