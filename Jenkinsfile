pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID     = credentials('access-key')
        AWS_SECRET_ACCESS_KEY = credentials('secret-access-key')
        AWS_DEFAULT_REGION    = 'us-east-1'
    }
    stages {
        stage('Clone') {
            steps {
                // Checkout your source code from version control
                git 'https://github.com/nishusingh26/kafka-ansible-pipeline.git'
            }
        }

        stage('Run Ansible Roles') {
            parallel {
                stage('Kafka Role') {
                    steps {
                        // Run your first Ansible role
                        sh 'ansible-playbook -i aws_ec2.yml kafka.yml'
                    }
                }
                stage('Zookeeper Role') {
                    steps {
                        // Run your second Ansible role
                        sh 'ansible-playbook -i aws_ec2.yml zookeeper.yml'
                    }
                }
            }
        }
    }
}
