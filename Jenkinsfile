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
                sh 'id'
                sh 'ls && pwd'
                sh './gradlew build'
                
                
            }
        }
    }
    stage("docker") {
    node("kubernetes") {
        container("docker") {
           checkout scm
                sh 'df -k'
                sh "docker version"
                sh 'id'
                sh 'ls'
                sh 'pwd' 
                sh 'docker build .'

            }
        }
    }
}