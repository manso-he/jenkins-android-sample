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
                        keyStoreId: "android-test",
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
