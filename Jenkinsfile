pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/khc02525/testWeb.git'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Tomcat 컨테이너 이름 (실제 이름 확인 필요)
                    def tomcatContainer = "tomcat"
                    def warFile = "${env.WORKSPACE}/ROOT.war"

                    // 기존 ROOT.war 삭제 및 새 파일 복사
                    sh """
                        docker exec ${tomcatContainer} rm -f /usr/local/tomcat/webapps/ROOT.war
                        docker cp ${warFile} ${tomcatContainer}:/usr/local/tomcat/webapps/ROOT.war
                    """
                }
            }
        }

        stage('Restart Tomcat') {
            steps {
                script {
                    def tomcatContainer = "tomcat"
                    sh """
                        docker exec ${tomcatContainer} /usr/local/tomcat/bin/shutdown.sh || true
                        sleep 5
                        docker exec ${tomcatContainer} /usr/local/tomcat/bin/startup.sh
                    """
                }
            }
        }
    }
}
