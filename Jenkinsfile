pipeline{
    agent any
    stages{
        stage('Checkout'){
            steps{
            echo 'Checking out branch' + env.BRANCH_NAME
                checkout scm
                sh 'ls -lrt'
                
            }
        }
        stage('Deploy Mysql'){
            steps{
                sh """
                   gcloud auth list
                   gcloud container clusters get-credentials wordspres-gke-euwe2 --region europe-west2 --project flash-keel-412418
                   helm uninstall mysql || exit 0
 
                   helm install  mysql  helm-charts/mysql -f helm-overrides/mysql-bld-01.yaml 
                   sleep 60
                
                """
               
                
         
            }
        }
        
        stage('Deploy Wordpress'){
            steps{
                sh """
                    gcloud container clusters get-credentials wordspres-gke-euwe2 --region europe-west2 --project flash-keel-412418
                    helm uninstall wordspress || exit 0
                   
                    helm install  wordspress helm-charts/wordpress -f helm-overrides/wordpress-bld-01.yaml 
                     sleep 30
                    
                """
               
               
                
                sh 'kubectl get ns'
            }
        }
        

 
    }
}
