# DSpace-Docker-Installation

Steps for installation of DSpace with Docker

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
      Also modify the "local.cfg" file in db.url with correct port for postgres
      
Step-11) Launch Docker-Compose

        $ docker-compose up -d
Step-12) 

      
Once launched, you should be able to attach to the container's bash process. This will get you into a 'developer' account
      
      
      
      
      

         
