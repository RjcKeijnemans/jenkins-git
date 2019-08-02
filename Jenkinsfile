pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                    echo "Importing values"
                    echo This is wrong > app.sh
                    echo but also not >> app.sh
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                    grep This app.sh >> ${BUILD_ID}.cov
                    grep but app.sh >> ${BUILD_ID}.cov
                ''' 
            }
        }
        stage('Coverage') {
            steps {
                sh '''
                    app_lines=`cat app.sh | wc -l`
                    cov_lines=`cat ${BUILD_ID}.cov | wc -l`
                    echo The app hass `expr $app_lines - $cov_lines' lines uncovered > ${BUILD_ID}.rpt
                
                    cat "${BUILD_IP}.rpt"
                '''
                archiveArtifacts "${env.BUILD_ID}.rpt"
            }
        }
    }
}
