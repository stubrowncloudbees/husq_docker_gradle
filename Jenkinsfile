podTemplate(label: "kubernetes", yaml: """
apiVersion: v1
kind: Pod
metadata:
  name: docker
spec:
  containers:
  - name: gradle
    image: stuartcbrown/gradlehusq
    command: ["sleep"]
    args: ["100000"]
  - name: docker
    image: docker:18.03-git
    command: ["sleep"]
    args: ["100000"]
    volumeMounts:
    - mountPath: /var/run/docker.sock
      name: docker-socket
  volumes:
  - name: docker-socket
    hostPath:
      path: /var/run/docker.sock
      type: Socket
"""
) {
    
    stage("gradle") {
    node("kubernetes") {
        container("gradle") {
            checkout scm
           
                sh 'df -k'
                sh 'ls /home/jenkins/workspace'
                sh 'id'
                sh 'ls && pwd'
                sh './gradlew build'
                sh 'cp Dockerfile /'
                
                
                
            }
        }
    }
    stage("docker") {
    node("kubernetes") {
        container("docker") {
           //checkout scm
                sh 'df -k'
                sh 'ls /home/jenkins/workspace'
                sh "docker version"
                sh 'id'
                sh 'ls'
                sh 'pwd' 
                //sh 'docker build .'
                sh 'ls /'
                docker.withRegistry('https://324005994172.dkr.ecr.us-east-1.amazonaws.com/cloudbeeps', 'ecr:us-east-1:demo-ecr-credentials') {
                  docker.image('demo').push('latest')
                }
               

            }
        }
    }
}
