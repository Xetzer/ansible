node("${env.SLAVE}") {

  stage("Build"){

    git branch: 'master', url: 'https://github.com/Xetzer/ansible.git'
    sh "mvn clean package -DbuildNumber=$BUILD_NUMBER"
    sh "echo build artefact"

  }

  stage("Package"){
    sh "tar czf mnt-exam-${BUILD_NUMBER}.tar.gz target/mnt-exam.war"
    sh "tar xzf mnt-exam-${BUILD_NUMBER}.tar.gz --strip-components 1"
    sh "echo package artefact"

  }

  stage("Roll out Dev VM"){
    sh "ansible-playbook createvm.yml -i inventory"
    sh "echo ansible-playbook createvm.yml"

  }

  stage("Provision VM"){
    sh "ansible-playbook provisionvm.yml"
    sh "echo ansible-playbook provisionvm.yml"

  }

  stage("Deploy Artefact"){
    sh "ansible-playbook deploy.yml"
    sh "echo ansible-playbook deploy.yml"

  }

  stage("Test Artefact is deployed successfully"){
    sh "ansible-playbook application_tests.yml"
    sh "echo ansible-playbook application_tests.yml"

  }

}

