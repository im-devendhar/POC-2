pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/im-devendhar/POC-2.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy with Ansible') {
    steps {
        sh '''
        export ANSIBLE_HOST_KEY_CHECKING=False
        ansible-playbook -i inventory deploy.yml
        '''
    }
}

    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo " Pipeline failed!"
        }
    }
}
