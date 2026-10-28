pipeline {
    agent any

    environment {
        KUBECTL = 'D:\\Docker\\resources\\bin\\kubectl.exe'
        KUBECONFIG = 'C:\\Users\\prave.LAPTOP-R0HN6EQN\\.kube\\config'
    }

    stages {
        stage('Check Kubernetes') {
            steps {
                bat '''
                    "%KUBECTL%" config current-context
                    "%KUBECTL%" get nodes
                '''
            }
        }

        stage('Create PVC') {
            steps {
                bat '"%KUBECTL%" apply -f C:\\Kubernetes-PVC\\pvc.yaml'
            }
        }

        stage('Create Pod') {
            steps {
                bat '"%KUBECTL%" apply -f C:\\Kubernetes-PVC\\pod.yaml'
            }
        }

        stage('Verify PVC and Pod') {
            steps {
                bat '"%KUBECTL%" get pvc jenkins-pvc'
                bat '"%KUBECTL%" get pod jenkins-pvc-pod'
            }
        }

        stage('Verify Stored File') {
            steps {
                bat '"%KUBECTL%" exec jenkins-pvc-pod -- cat /data/result.txt'
            }
        }
    }

    post {
        success {
            echo 'PVC, Pod, and persistent file verified successfully.'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}