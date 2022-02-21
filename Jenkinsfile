pipeline {
    agent any
    tools {
    maven 'maven-instance'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout changelog: true, poll: true, scm: [
                        $class                           : 'GitSCM',
                        branches                         : [[name: "cicd"]],
                        doGenerateSubmoduleConfigurations: false,
                        extensions                       : [[$class: 'UserIdentity', email: 'caolv@biplus.com.vn', name: 'caolv']],
                        submoduleCfg                     : [],
                        userRemoteConfigs                : [[credentialsId: 'b1872cd7-b22b-4360-a59f-347e20feca68',
                                                            name         : 'origin',
                                                            url          : "${env.gitlabSourceRepoHomepage}" + ".git"]]
                ]
            }
        }
        stage('Build microservice') {
            steps {
                script {
                    jenkinsfile_bootstrap = load 'jenkinsfile_bootstrap.groovy'
                    jenkinsfile_bootstrap.bootstrap_build()
                    sh 'printenv'
                    sh 'echo test'
                }
            }
        }
    }
}

