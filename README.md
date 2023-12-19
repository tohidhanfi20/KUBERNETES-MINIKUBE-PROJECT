# JAVA KUBERNETE'S DEPLOYMENT


# STEP 1:

  1.MINIKUBE AND DOCKER INSTALLATION ON AMAZON LINUX

    - Launch an instance from an Amazon Linux 2 or Amazon Linux AMI
    - Instance Type - t2.medium
    - Proceed without a key-pair
    - Create a security group
    - Storage 15GB
    
  Edit security group wilh all traffic

  2. Connect to your instance

  3. Update the packages and package caches you have installed on your instance.

    - yum update -y   

  4. Install the latest Docker Engine packages.

    - amazon-linux-extrasinstalldocker
    - yuminstalldocker-y

  5. Start the Docker service.

    - systemctlstartdocker
    - systemctlenabledocker

  6. Install Conntrack and Minikube.

    - yum install conntrack -y
    - curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    - sudo install minikube-linux-amd64 /usr/local/bin/minikube 

  7. Start your MINIKUBE

    - sudo /usr/local/bin/minikubestart--force--driver=docker


# STEP 2 :  

  DOCKER

    - yum install docker -y 
    - systemctl start docker 
    - systemctl enable docker

  MAVEN

    - cd/opt/
    - wget http://mirrors.estointernet.in/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
    - tar xvzf apache-maven-3.6.3-bin.tar.gz
    - vi/etc/profile.d/maven.sh
    - export MAVEN_HOME=/opt/apache-maven-3.6.3
    - export PATH=$PATH:$MAVEN_HOME/bin

 GIT 

    - yum install git -y 
    
 JAVA

    - yum install java -y
    

 # STEP 3 : 

    - curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.20.4/2021-04-12/bin/linux/amd64/kubectl
    - chmod +x ./kubectl
    - mkdir -p $HOME/bin
    - cp ./kubectl $HOME/bin/kubectl
    - export PATH=$HOME/bin:$PATH
    - echo'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
    - source $HOME/.bashrc
    - kubectl version --short –client
    
    
 # STEP 4 :     

    - git clone https://github.com/tohidhanfi20/KUBERNETES-MINIKUBE-PROJECT
    

# STEP 5 : IMPORTANT STEP

  NOTE - Give your dockerhub ID in place of tohidaws
  
  SERVICE 1 - Shopfront
  
        - cd shopfront/
        - mvn clean install -DskipTests
        - docker build -t tohidaws/shopfront:latest .
        - docker push tohidaws/shopfront:latest

  SERVICE 2 - productcatalogue
  
        - cd productcatalogue/
        - mvn clean install -DskipTests
        - docker build -t tohidaws/productcatalogue:latest .
        - docker push tohidaws/productcatalogue:latest

  SERVICE 3 - stockmanager
  
        - cd stockmanager/
        - mvn clean install -DskipTests
        - docker build -t tohidaws/stockmanager:latest .
        - docker push tohidaws/stockmanager:latest


# STEP 6 : 

   GO TO KUBERNETES FOLDER IN SAME PROJECT

        - cd kubernetes
        - kubectl apply -f shopfront-service.yaml
        - kubectl apply -f productcatalogue-service.yaml
        - kubectl apply -f stockmanager-service.yaml



# STEP 7 : 

     - kubectl get pods



# STEP 8 :

  Hit the below command to start the kubernetes dashboard in EC2

    - /usr/local/bin/minikube dashboard
    

# STEP 9 : IN NEW EC2 WINDOW

  Open the EC2 in new window and set the PROXY

    - kubectl proxy --address='0.0.0.0' --accept-hosts='^*$' 
    

# STEP 10 : 

  Hit in browser to view the dashboard

    - http://<EC2-IP>:8001/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/pod?namespace=default
    

    
# STEP 11 :         

  Hit the below command for each service in different console of EC2

  EC2 LOGIN FOR SHOPFRONT
  
     - kubectl port-forward --address 0.0.0.0 svc/shopfront8080:8010

  EC2 LOGIN FOR productcatalogue
  
     - kubectlport-forward--address0.0.0.0svc/productcatalogue8090:8020

  EC2 LOGIN FOR stockmanager
  
     - kubectlport-forward--address0.0.0.0svc/stockmanager9008:8030


     
# STEP 12 :       

   For productcatalogue
   
      - http://<EC2IP>:8090/products

   For stockmanager

      - http://<EC2IP>:9008/stocks



 # STEP 13 :

   ANALYZE THE DASHBOARD



# We Have Successfully completed our Java Kubernete's deployement
