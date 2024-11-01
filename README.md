pipeline {
    agent any
    stages {
        stage('Create HTML') {
            steps {
                script {
                    def country = 'USA' 
                    sh """
                    echo "<html><body><h1>Hello, World!</h1><p>Country: ${country}</p></body></html>" > /tmp/index.html
                    """
                    echo "HTML file created at /tmp/index.html"
                }
            }
        }
    }
}
