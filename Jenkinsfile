stages {
    stage('Checkout Code') {
        steps {
            checkout([
                $class: 'GitSCM',
                branches: [[name: 'main']],
                extensions: [],
                userRemoteConfigs: [[
                    credentialsId: 'github-cred',
                    url: 'https://github.com/ravish142000/Basichtml.git'
                ]]
            ])
        }
    }
    // ... (rest of the stages)
}
