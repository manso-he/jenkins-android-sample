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
                sh './gradlew assembleProd' 
            }
        }
        stage("Sign APK"){
            steps {
                echo 'Sign APK'
                signAndroidApks(
                        keyStoreId: "android-test",
                        keyAlias: "android.keystore",
                        apksToSign: "**/*-prod-release-unsigned.apk",
                        archiveSignedApks: false,
                        archiveUnsignedApks: false
                )
            }
        }
    }

}
