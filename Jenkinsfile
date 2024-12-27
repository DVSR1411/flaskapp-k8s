pipeline {
    agent any
    tools {
        git 'Default'
    }
    stages {
        stage('Update manifest') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'git', passwordVariable: 'passwd', usernameVariable: 'user')]) {
                    git "https://github.com/$user/flaskapp-k8s.git" 
                    sh "git config user.name $user"
                    sh "git config user.email satwikreddy.danda@hotmail.com"
                    sh "sed -i 's+dvsr1411/flaskapp.*+dvsr1411/flaskapp:$params.dockertag+g' deployment.yml"
                    sh "git add ."
                    sh "git commit -m Commit-$params.dockertag"
                    sh "git push https://$user:$passwd@github.com/$user/flaskapp-k8s.git master"
                }
            }
        }
    }
}
