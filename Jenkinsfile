pipeline {
    parameters {
        choice(name: 'PLATFORM_FILTER', choices: ['all', 'master', 'ubuntu18-digitalocean'], description: 'Run on specific platform')
    }
    agent none
    stages {
        stage('BuildAndTest') {
            matrix {
                agent {
                    label "${PLATFORM}-agent"
                }
                when { anyOf {
                    expression { params.PLATFORM_FILTER == 'all' }
                    expression { params.PLATFORM_FILTER == env.PLATFORM }
                } }
                axes {
                    axis {
                        name 'PLATFORM'
                        values 'master', 'ubuntu18-digitalocean'
                    }
                }
                excludes {
                    exclude {
                        axis {
                            name 'PLATFORM'
                            values 'master'
                        }
                    }
                    exclude {
                        axis {
                            name 'PLATFORM'
                            notValues 'ubuntu18-digitalocean'
                        }
                    }
                }
                stages {
                    stage('Build') {
                        steps {
                            echo "Do Build for ${PLATFORM}"
                        }
                    }
                    stage('Test') {
                        steps {
                            echo "Do Test for ${PLATFORM}"
                        }
                    }
                }
            }
        }
    }
}
