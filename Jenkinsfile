pipeline {

    environment {
        docker_image_name = "angular6-build"
    }

    agent {
        dockerfile {
            filename 'Dockerfile.build'
            dir '.'
            label env.docker_image_name
        }
    }

    stages {

        stage('Pre-Build') {
            steps {
                script{
                    dir('.'){
                        sh 'npm --version'
                        sh 'sudo npm i-g  @angular/cli'
                        sh 'npm install'
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    dir('.') {
                        sh 'ng build'
                    }
                }
                script {
                    dir('dist') {
                        sh 'tar -cvzf voting-client.tar.gz *'
                    }
                }
                archiveArtifacts 'dist/voting-client.tar.gz'
            }
        }

    }
    // post {
    //     always {
    //         script {
    //             sh "docker rmi ${env.docker_image_name}"
    //         }
    //     }
    // }
}
