node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email j.geof93@gmail.com"
                        sh "git config user.name jgeof"
                        //sh "git switch master"
                        sh "cat deployment.yml"
                        sh "sed -i 's+joeygeofrey/test.*+joeygeofrey/test:${DOCKERTAG}+g' deployment.yml"
                        sh "cat deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'Update: jenkins job update manifest: ${env.BUILD_NUMBER}'"
                        sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/flaskblog-CD.git HEAD:main'
      }
    }
  }
}
}
