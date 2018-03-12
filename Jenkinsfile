pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('env init') {
      steps {
        sh '''if [ -n "`docker ps -a |grep promise-bulter-dev-ci`" ]; then (docker stop promise-bulter-dev-ci)&&(docker rm promise-bulter-dev-ci); fi
docker run -it -d --name=promise-bulter-dev-ci --hostname=promise-bulter-dev-ci -v /etc/localtime:/etc/localtime:ro -e "PYTHONPATH=/apps/svr/promise-bulter" promise-base:v1.0 /usr/sbin/init'''
        sh '''docker exec promise-bulter-dev-ci git clone http://192.168.182.51/promise/promise-bulter.git /apps/svr/promise-bulter
'''
        sh '''docker exec promise-bulter-dev-ci cp /apps/svr/promise-bulter/env.conf/my.cnf /etc/
'''
        sh '''docker exec promise-bulter-dev-ci chmod 0644 /etc/my.cnf
'''
        sh '''#docker exec cp /apps/data/tomcat_8080/jenkins_file/promise-back/promise-bulter-dev-ci/dev-ci-instance promise-bulter-dev-ci:/apps/svr/promise-bulter/
docker exec promise-bulter-dev-ci pip install -r /apps/svr/promise-bulter/requirements.txt'''
      }
    }
  }
}