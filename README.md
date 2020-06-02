pipeline {    
        agent any
                stages {
                        stage('One') {
                                steps { 
                                        echo 'hi, this is Lloyd from Leeds' 
                                 }
                          }
                          
                          stage('Two') {
                                  steps { 
                                          input('dDo you want to proceed?')
                                   }
                           }
                           
                           stage('Three') {
                                    when {
                                              not {
                                                      branch "master"
                                              }
                                      }
                                      steps {
                                              echo "Hello"
                                       }
                           }
                           
                           stage('Four') {
                                            parallel {
                                                   stage('Unit Test') {
                                                                      steps {
                                                                             echo "Running the unit test..."
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
                                                                                echo 'Running the integration test..'
                                                                         }
                                                       }
  }
  }
  }
  }
