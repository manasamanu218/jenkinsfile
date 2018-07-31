pipeline {
        agent any
               stages {
                       stage('one') {
                                  steps {
                                         echo 'HI,this is manasa'
                                  }
                         }
                         stage('two') {
                                    steps {          
                                           input('DO you want to proceed?')
                                     }
                           }
                           stage('three') {
                                      when {
                                             not {
                                                     branch "master"
                                                  }
                                      }
                                      steps {
                                              echo "Hello"
                                              }
                            }
                            stage('four') {
                                           parallel {
                                                     stage('unit test') {
                                                                        steps{
                                                                              echo "Running the unit test......"
                                                                         }
                                                      }
                                                      stage('Integration test') {
                                                                            agent {
                                                                                  docker {
                                                                                          reuseNode false
                                                                                          image 'ubuntu'
                                                                                   }
                                                                              }
                                                                              steps {
                                                                                     echo 'Running the integration test'
                                                                               }
                                                         }
                                                  }
}
}
}
}
