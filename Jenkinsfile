pipeline
{
    agent any
    stages
    {
        stage('continuous-Download')
        {
            steps
            {
               script
                {
                  try
                 {
                  git 'https://github.com/IntelliqDevops/maven1.git' 
                 }
                  catch (Exception e1)
                 {
                    mail bcc: '', body: 'Download_Stage_Failed', cc: '', from: '', replyTo: '', subject: 'jenkins_download', to: 'mr.vmanoj3@gmail.com'
                    exit(1)
                     
                 }
                } 
            }
            
        }
        stage('Continuous-Build')
        {
            steps
            {
              script
               {
                 try
                {
                   sh 'mvn package' 
                }
                catch(Exception e2)
                {
                    mail bcc: '', body: 'build_Stage_Failed', cc: '', from: '', replyTo: '', subject: 'Jenkins_Build_stage', to: 'middleware_engi@gmail.com'
                    exit(1)
                    
                }
               }
               
            }
        }
        stage('continuous-Deployment')
        {
            steps
              {
                  script
                  {
                       try
                       {
                           deploy adapters: [tomcat9(credentialsId: 'f93c1a56-c58d-460c-a340-5e1bbbdb010f', path: '', url: 'http://172.31.6.181:8080')], contextPath: 'newapp', war: '**/*.war' 

                       }
                       catch(Exception e3)
                       {
                           mail bcc: '', body: 'jekins_Deployment-Failed', cc: '', from: '', replyTo: '', subject: 'deployment', to: 'deploy@gmail.com'
                       }
                  }
               
            }
        }
        stage('continuous_testing')
        {
            steps
            {
                script
                 {
                    try
                    {
                        git 'https://github.com/IntelliqDevops/FunctionalTesting.git'
                        sh 'java -jar /var/lib/jenkins/workspace/Declarative_pipeline-1/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Testing_Stage_Failed', cc: '', from: '', replyTo: '', subject: 'Testing', to: 'testers@gmail.com'
                    }
                    
                }
            }
        }
        stage('Continuous_Delivery')
        {
            steps
            {
                script
                {
                   try  
                   {
                        deploy adapters: [tomcat9(credentialsId: 'f93c1a56-c58d-460c-a340-5e1bbbdb010f', path: '', url: 'http://172.31.5.89:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                   catch(Exception e5)
                   {
                       mail bcc: '', body: 'Jenkins_Delivery_stage_Failed', cc: '', from: '', replyTo: '', subject: 'Delivery_Stage', to: 'delivery@gmail.com'
                   }
                }
            }
        }
    }
}
