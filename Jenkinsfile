node {
   def mvnHome
   stage('Pre-req-display') { 
      sh """
      echo "Running this on Openshift Platform" 
      echo "Expecting you to have surjagta001-dev project in OCP" 
      echo "Jenkins Service-account should have privilages to do change on surjagta001-dev project" 
      """
      
   }
   stage('checkout') { 
      git 'https://github.com/jagtapsuresh/ubi_utils.git'
      
   }
   
   stage('Start container build'){
        sh """
                
                oc project surjagta001-dev
                echo "Creating BuildConfig/IS."
        		oc new-build --name=fuse-karafbase-image --binary=true --strategy=docker --to-docker=true -n surjagta001-dev
                tar -cvf a.tar jolokia/ run-java/ s2i/ Dockerfile
                oc start-build fuse-karafbase-image -n surjagta001-dev --from-archive=a.tar --follow
                
           """


    }
   
}
