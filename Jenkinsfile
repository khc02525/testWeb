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
                    // Tomcat webapps 경로
                    def tomcatWebapps = "/usr/local/tomcat/webapps"

                    // 기존 ROOT.war 삭제 (있을 경우)
                    sh """
                        rm -f ${tomcatWebapps}/ROOT.war
                    """

                    // GitHub에서 받은 root.war 복사
                    sh """
                        cp ROOT.war ${tomcatWebapps}/ROOT.war
                    """
                }
            }
        }

        stage('Restart Tomcat') {
            steps {
                script {
                    sh """
                        # Tomcat 재시작 (예시, 환경에 맞게 수정 필요)
                        /usr/local/tomcat/bin/shutdown.sh || true
                        sleep 5
                        /usr/local/tomcat/bin/startup.sh
                    """
                }
            }
        }
    }
}
