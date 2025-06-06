pipeline {
    agent any
    parameters {
        choice(
            name: 'ENV',
            choices: ['dev', 'prod'],
            description: 'Выберите окружение'
        )
    }
    stages {
        stage('Deploy') {
            steps {
                echo "Deploying to ${params.ENV}"
                cleanWs()  // Очистка рабочей директории
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'your-ssh-server',  // Название SSH-сервера в Jenkins
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/*',
                                    removePrefix: '',
                                    remoteDirectory: "${params.ENV}",
                                    execCommand: 'echo "Файлы скопированы"'
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }
}
