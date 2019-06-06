pipeline{
				 agent any
				 environment {
        								EMAIL_RECIPIENTS = 'shivu483@gmail.com'
        								DEV='services-int.dev.keeboot.com'
        								QE='services-int.qe.keeboot.com'
        								STAGING='services-int.staging.keeboot.com'
        								AWS='services-int.staging.keeboot.com'
    			}
    			parameters {
  									string defaultValue: 'master', description: '''enter branch name master is taking as default''', name: 'branch', trim: false
  									choice choices: ['DEV', 'QE', 'STAGING', 'AWS'], description: 'choose the option aws,dev,qe,staging', name: 'environment'
  									credentials credentialType: 'com.cloudbees.jenkins.plugins.sshcredentials.impl.BasicSSHUserPrivateKey', defaultValue: 'privatekey', description: 'ssh login credentials', name: 'ssh', required: true
				}
    			stages {
    						stage('checkout branch'){
    						          input {
  												  message 'Shall i deploy ?'
  												  id 'deploy'
  												  ok 'continue'
 												  submitter 'devops'
  												  submitterParameter 'approverOfdeploy'
										}
    						          steps {
    						          			script{
                                                             echo "hi how are you"
                                                             echo "enterd branch name ${params.branch}"

    						          			}
    						          }
    						}
    						stage('upload ') {
             											steps {
                												script {
                												            def pom = readMavenPom file: 'pom.xml'
                												            echo  "groupId ${pom.groupId}"
                												            echo  "artifactId ${pom.artifactId}"
                												            echo  "verstion ${pom.version}"
                        													sh "mvn deploy"
                        													echo " uploaded successfully"
                       
            													}
        												}
    						}
    						stage('push to remote and deploy for dev'){
                                        when{
                                                equals expected: 'DEV', actual: "${params.environment}"
                                        }
                                        steps{
                                                  script{
                                                   			   def pom = readMavenPom file: 'pom.xml'
                											   echo  "groupId ${pom.groupId}"
                											   echo  "artifactId ${pom.artifactId}"
                											   echo  "verstion ${pom.version}"
                                                               def workspace = "/var/lib/jenkins"
                                                               echo "Deploying to ${params.environment}"
                                                               sh "ssh -o StrictHostKeyChecking=no -i ${workspace}/prod_login_key.txt -p 2779 deploy@139.162.46.185 'bash -s ' < ${workspace}/deploy.sh java ${pom.groupId} ${pom.artifactId} ${pom.version}"
                                                  }
                                        }
    						}
    						stage('push to remote and deploy for qe'){
                                        when{
                                                equals expected: 'QE', actual: "${params.environment}"
                                        }
                                        steps{
                                                  script{
                                                               echo "Deploying to ${params.environment}"
                                                  }
                                        }
    						}   						
    						stage('push to remote and deploy for staging'){
                                        when{
                                                equals expected: 'STAGING', actual: "${params.environment}"
                                        }
                                        steps{
                                                  script{
                                                               echo "Deploying to ${params.environment}"
                                                  }
                                        }
    						}
    			}

}
