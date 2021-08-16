pipeline {
    agent any
    parameters{
             string( defaultValue: '', name: 'repo', description: 'Repo')
	     string( defaultValue: 'master', name: 'branch', description: 'Branch')
	     choice( choices: ['pass', 'run,not pass'], description: 'Please choice action', name: 'actions')
    }
	    
    stages {
        stage('Ls') {
		when {
			expression {return 'run' in env.actions.split(',')}
		}
            steps {
		dir('repo') {
		    checkout scm: [$class: 'GitSCM', userRemoteConfigs: [[url: "${params.repo}", credentialsId: 'atolkachev']], branches: [[name: "${env.branch}"]]], poll: false
		}
            }
        }
	stage('git') {
		when {
			expression {return 'run' in env.actions.split(',')}
		}
            steps {
                sh 'git status'
		dir('repo') {
			sh 'git status'
		}
            }
        }
    }
}
