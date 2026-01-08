pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/USERNAME/REPO_NAME.git'
            }
        }

        stage('Build') {
            steps {
                echo 'HTML project - no build required'
            }
        }

        stage('Test') {
            steps {
                sh '''
                echo "Testing HTML file"
                test -f index.html
                grep -i "<html" index.html
                '''
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(['ec2-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ec2-user@13.204.68.242 << EOF
                      sudo cp index.html /var/www/html/
                      sudo systemctl restart httpd
                    EOF
                    '''
                }
            }
        }
    }
}
