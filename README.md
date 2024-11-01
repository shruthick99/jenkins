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
        stage('Serve HTML') {
            steps {
                script {
                    // Start a simple HTTP server in the background
                    sh 'nohup python3 -m http.server 8080 --directory /tmp &'
                    echo "HTTP server started on port 8080"
                }
            }
        }
    }
    post {
        always {
            echo "Pipeline finished."
        }
    }
}
