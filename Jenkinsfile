stages {
    stage('Checkout Code') {
        steps {
            checkout([
                $class: 'GitSCM',
                branches: [[name: 'main']],
                extensions: [],
                userRemoteConfigs: [[
                    credentialsId: 'github-cred',
                    url: 'https://github.com/your-username/your-repo.git'
                ]]
            ])
        }
    }
    // ... (rest of the stages)
}
