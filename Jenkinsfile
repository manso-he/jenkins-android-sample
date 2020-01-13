pipeline {
    agent {
        docker {
            image 'allbears/jenkins-android:1.0.1'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh './gradlew clean && rm -rf ./app/build/'
                sh './gradlew assembleRelease' 
            }
        }
        stage("Sign APK"){
            steps {
                echo 'Sign APK'
                signAndroidApks(
                        keyStoreId: "a20a9c66-1744-4b8f-b1a5-72e8073c0539",
                        keyAlias: "android.keystore",
                        apksToSign: "app/build/**/*.apk",
                        archiveSignedApks: false,
                        archiveUnsignedApks: false,
                        skipZipalign: true
                )
            }
        }
        stage('Archive') {  
            steps {
                archiveArtifacts artifacts: 'app/build/outputs/**/*.apk', fingerprint: true 
            }
        }
    }

}
