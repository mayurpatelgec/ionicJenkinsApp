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
        
          // requires SonarQube Scanner 2.8+
          def scannerHome = tool 'sonarscanner';
          withSonarQubeEnv('sonarqubeserver') {
            sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ionicJenkins -Dsonar.sources=./src -Dsonar.language=ts"
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
