pipeline {
   agent any
      environment {
         PATH='/usr/local/bin:/usr/bin:/bin'
      }
   stages {
      stage('NPM Setup') {
        steps {
          sh 'npm install'
        }
      }

      stage('SonarQube analysis') {
        steps {
          // requires SonarQube Scanner 2.8+
          def scannerHome = tool 'SonarQube Scanner 3.2.0.1227';
          withSonarQubeEnv('My SonarQube Server') {
            sh "${scannerHome}/bin/sonar-scanner"
          }
        }
      }

      stage('IOS Build') {
        steps {
            sh 'ionic cordova build ios --release'
        } 
      }

      stage('Android Build') {
        steps {
            sh 'ionic cordova build android --release'
        }
      }

      stage('APK Sign') {
        steps {
                echo 'APK Sign'
            // sh 'jarsigner -storepass your_password -keystore keys/yourkey.keystore platforms/android/app/build/outputs/apk/release/app-release-unsigned.apk nameApp'
          }
      }

      stage('Stage Web Build') {
          steps {
            sh 'npm run build --prod'
        }
      }

      stage('Publish iOS') {
        steps {
          echo "Publish iOS Action"
        }
      }

      stage('Publish Android') {
        steps {
          cho "Publish Android API Action"
        }
      }

  }
}
