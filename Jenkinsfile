#!groovy

def repo_name = 'samplemod'
def git_url = 'https://github.com/t-hsgw/${repo_name}.git'



pipeline {
    agent {
        docker {
            image 'python:3.5.1'
            args '-u root -v /var/lib/jenkins/.pypirc:/var/lib/jenkins/workspace/sample_pipeline/.pypirc'
        }
    }
    stages {
        stage('id'){
            steps {
                sh 'id'
                sh 'hostname'
                sh 'pwd'
                sh 'ls -al'
                sh 'cat .pypirc'
                sh 'cd /'
                sh 'ls'
            }
        }
        stage('docker setup') {
            steps {
                sh 'pip install --upgrade pip'
                sh 'pip install twine'
                sh 'pip install -r requirements.txt'
                sh 'python -V'
            }
        }
        stage('test'){
            steps {
                sh 'python setup.py test'
                sh 'python setup.py upload --help'
                sh 'python setup.py sdist'
                sh 'twine upload --config-file .pypirc --repository internal --skip-existing dist/*'
            }
        }
    }
}

