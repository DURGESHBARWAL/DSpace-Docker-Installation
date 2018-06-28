# DSpace-Docker-Installation


                              Steps for installation of DSpace with Docker
                              
          Basic Requirements is that, we need a user account with "dspace" name. Otherwise, we have to change the all configration files of dspace-src folder.                  
                              

Step-1
      Update your system
      
      $ sudo apt-get update
Step-2
      Basic requirement for this installation process:
        Git, Docker, Docker-Compose
        
      $ sudo apt-get install git
  
   Docker - https://docs.docker.com/install/linux/docker-ce/ubuntu/#set-up-the-repository

   Docker Compose -- https://docs.docker.com/compose/install/

Step-3) Clone the Repository "Dspace-Labs/dspace-dev-docker"
       
       $ git clone https://github.com/DSpace-Labs/dspace-dev-docker.git
       $ cd dspace-dev-docker

Step-4) Clone the DSpace Repository in dspace-src folder 
      
      $ git clone -b dspace-6.0 https://github.com/DSpace/DSpace.git dspace-src

Step-5) Also, add m2-repo and dspace-build folders.
          
      $ mkdir m2-repo dspace-build
            
Step-6) (Optional)  If you already have a working copy of DSpace checked out on your computer:
       
      $ ln -s /path/to/your/dspace/working/copy dspace-src

Step-7) Changing Ownership of Folders to your Users.Replace "youruser" with your username of the machine.
      
      $ sudo chown -R youruser:youruser dspace-src dspace-build m2-repo

               
               
               ----------------------Edit the DSpace configuration---------------------------------
               
               

Step -8) Find the "local.cfg.EXAMPLE" file inside the dspace-src/dspace/config directories
           
           $ cd dspace-src/dspace/config

Step-9) Open the "local.cfg.EXAMPLE" file and copy its content and paste its content into new file "local.cfg"

Step-10) Edit the "local.cfg" file with the reference bellow.

      ##########################
      # SERVER CONFIGURATION   #
      ##########################
      dspace.dir=/srv/dspace

      dspace.hostname = localhost

      dspace.baseUrl = http://localhost:8080

      dspace.ui = jspui

      # Name of the site
      dspace.name = DSpace Using Docker of My University
      
      solr.server = http://localhost/solr

      ##########################
      # DATABASE CONFIGURATION #
      ##########################
      # DSpace only supports two database types: PostgreSQL or Oracle
      
      db.url = jdbc:postgresql://postgres:5432/dspace
     
Basic Requirements:     
      
      NOTE: 
      
      Have ports 8080 (tomcat), 5432 (postgresql), 1043 and 8000 (remote debugging) open.
      Otherwise, you can modify the mappings in docker-compose.yml file to use whichever ports you prefer.
      Also modify the "local.cfg" file in db.url with correct port for postgres.
      
      
      NOTE: 
      
      ******************To Activate APIs of DSpace, Disable the SSL******************************
                To disable DSpace REST's requirement to require security/ssl, [dspace-source]/dspace-rest/src/main/webapp/WEB-INF/web.xml and comment out the <security-constraint> block.
      
Step-11) Launch Docker-Compose

        $ docker-compose up -d
Step-12) Once lanched, to get into developer account, first find the container id of "dspace-dev-docker_dspace-dev" using,
      
        $ docker ps
        
   Take the container id of "docker-dev-docker_dspace-dev" from above and use the same id in the next step.
        
        $ docker attach <container-id>
                  
                  Example: docker attach 9be4y7se3
              
Step-13) Compilation of DSpace inside the container

       $ mvn -Dmirage2.on=true -Dmirage2.deps.included=false package
    
Step-14) Once compiled the task' alias is available.Install the java webapps inside the container.

        
        $ task fresh_install
       
Step-15) Now create a user for the DSpace

        $ dspace create-administrator
        
Step -16) Staring the server

       $ tomcat start && catalina.out
 
 -----------------------------------------------------------------------------------------------------------------------
 
             Now open http://localhost:8080/xmlui/ , you can access the DSpace xml UI.
      
      
References:

    [1] https://wiki.duraspace.org/display/~terrywbrady/Building+and+Running+DSpace+in+Docker
    [2] http://wiki.lib.sun.ac.za/index.php?title=SUNScholar/Install_DSpace/S04/5.X
    [3] https://github.com/DSpace-Labs/dspace-dev-docker
    [4] https://wiki.duraspace.org/display/DSDOC6x/REST+API#RESTAPI-DisablingSSL  
                 
