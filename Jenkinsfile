pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deploy') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'echo "shutting down"'
                sleep(time: 1, unit: 'MINUTES')
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}

// node {
//     docker.image('node:16-buster-slim').inside('-p 3000:3000') {
//         stage('Build') {
//             echo "Build with Scripted Pipeline"
//             sh 'npm install'
//             }
//         stage('Test') { 
//             echo "Testing with Scripted Pipeline"
//             sh './jenkins/scripts/test.sh' 
//             echo "Testing Finished"
//         }
//     }
// }
