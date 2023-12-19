# JAVA KUBERNETE'S DEPLOYMENT


# STEP 1:

  1.MINIKUBE AND DOCKER INSTALLATION ON AMAZON LINUX

    - Launch an instance from an Amazon Linux 2 or Amazon Linux AMI

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

    - /usr/local/bin/minikubestart--force--driver=docker

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

    - 


  
