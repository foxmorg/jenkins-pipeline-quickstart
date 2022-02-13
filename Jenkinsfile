pipeline {
    agent none
    stages {
        stage('docker agent test') {
	          agent { docker { image 'maven:3.8.4-openjdk-11-slim' } }
            steps {
                sh 'mvn --version'
            }
        }
	      stage('work with remote git repo - move branch to specified commit id') {
		        agent any

    		    parameters {
        		    string(name: 'commitId', defaultValue: 'HEAD', description: 'Enter a commit id')
    		    }
		        stages {
                stage('Starting') {
                    steps {
                        echo 'Start...'
                        echo "moving prod branch to: ${params.commitId}"
                    }
                }
                stage('git pull/clone') {
                    steps {
                        git url: 'git@github.com:foxmorg/git-init.git', branch: 'master'
                    }
                }
                stage('moving prod branch to specified commit') {
                    steps {
                        sh "git branch -f prod ${params.commitId}"
                    }
                }
                stage('push prod branch to remote repo') {
                    steps {
                        sh 'git push -f origin prod'
                    }
                }
                stage('Finish') {
                    steps {
                        echo '...Finished'
                    }
                }
            }
        }
    }
}
