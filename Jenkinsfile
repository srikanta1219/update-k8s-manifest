node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    //withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
   
                    withCredentials([usernamePassword(credentialsId: 'GitHub', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email srikantanayak41@gmail.com"
                        sh "git config user.name srikanta1219"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+srikanta1219/shanvi.*+srikanta1219/shanvi:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push --force https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/update-k8s-manifest.git HEAD:master"
                        //sh "git push https://github.com/srikanta1219/update-k8s-manifest.git"
                        
      }
    }
  }
}
}
