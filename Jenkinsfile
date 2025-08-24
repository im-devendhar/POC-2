pipeline {
    agent any

    environment {
        // Disable SSH host key checking for Ansible
        ANSIBLE_HOST_KEY_CHECKING = "False"
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Pull the code from your GitHub repository
                git branch: 'main', url: 'https://github.com/im-devendhar/POC-2.git'
            }
        }

        stage('Build with Maven') {
            steps {
                // Clean and package the project to produce POC-2.war
                sh 'mvn clean package'
            }
        }

        stage('Run Unit Tests') {
            steps {
                // Execute unit tests
                sh 'mvn test'
            }
        }

        stage('Deploy with Ansible') {
            steps {
                // Run Ansible playbook to deploy the WAR to Tomcat
                sh 'ansible-playbook -i inventory deploy.yml'
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline executed successfully! WAR deployed as POC-2.war"
        }
        failure {
            echo "❌ Pipeline failed!"
        }
    }
}
