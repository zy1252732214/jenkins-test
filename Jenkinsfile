pipeline {
    agent {
        kubernetes {
            // 定义构建环境，这里用一个包含 git 和 maven/node 的镜像
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: build-tool
    image: alpine/git  # 仅仅演示，实际项目可能需要 maven 或 node 镜像
    command:
    - cat
    tty: true
'''
        }
    }
    stages {
        stage('Checkout') {
            steps {
                // 拉取代码
                checkout scm
                sh 'ls -al'
            }
        }
        stage('Test') {
            steps {
                container('build-tool') {
                    sh 'echo "Running tests..."'
                    sh 'git --version'
                }
            }
        }
        stage('Build') {
            steps {
                container('build-tool') {
                    sh 'echo "Building artifact..."'
                }
            }
        }
    }
}