# Publishing-Artifacts-on-Nexus

## Demo Project:

**Run Nexus on Droplet and Publish Artifact to Nexus**

Technologies used:
- Nexus
- DigitalOcean
- Linux
- Java
- Gradle
- Maven

### Project Description:

- Install and configure Nexus from scratch on a cloud server
- Create a new User on Nexus with relevant permissions

#### Java Gradle Project: Build Jar & Upload to Nexus

#### Java Maven Project: Build Jar & Upload to Nexus


## Notes:

### Installing Nexus:
- Create new droplet on DigitalOcean
- Installing Nexus
  - Step 1: Install openjdx and net-tools
  
    apt update
    
    apt install openjdk-8-jre-headless
    
    apt install net-tools
    
  - Step 2: Download and untar nexus files
  
    cd /opt
    
    wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
    
    tar -zxvf latest-unix.tar.gz
    
  - Step 3: Create specific user for Nexus and configure it to use nexus
  
    adduser nexus
    
    chown -R nexus:nexus nexus-3.28.1-01
    
    chown -R nexus:nexus sonatype-work
    
    vim nexus-3.28.1-01/bin/nexus.rc
    
    run_as_user="nexus"
    
  - Step 4: Start nexus and check if its working
  
    su - nexus
    
    /opt/nexus-3.28.1-01/bin/nexus start
    
    ps aux | grep nexus
    
    netstat -lnpt

  - Step 5: Access nexus through web browser
  
    Port to be open using firewall rule - 8081

  - Step 6: Login using default user "admin"
  
    default user admin, one time password is stored in:
    
    cat /opt/sonatype-work/nexus3/admin.password
    
  - Step 7: Create local user and role using Nexus UI
  
    create local user on nexus using UI i.e. rachana
    
    create roles for the above created user using UI i.e. nx-java
    
    assign the role nx-java to user rachana
    
   
#### Java Gradle Project: Build Jar & Upload to Nexus

 - Step 1: In ‘build.gradle’ file add following lines.

   version '1.0-SNAPSHOT’

   apply plugin:'maven-publish’

   publishing {
   
     publications{
     
     maven(MavenPublication){
     
       artifact("build/libs/my-app-$version"+".jar"){
       
       extension ="jar"
       
       }
       
      }
      
    }
    
   repositories {
   
    maven{
    
        name ="nexus"
        
				url= "http://64.227.152.141:8081/repository/maven-snapshots/   
        
				allowInsecureProtocol = true
        
        credentials {
        
            username = project.repoUser
            
            password = project.repoPassword
            
        }
     }
   }

}

 - Step 2: Add credentials in gradle.properties file

 - Step 3: Set project name in settings.gradle file.

 - Step 4: Build the project using command :  ./gradlew build

 - Step 5: Publish the artifacts to nexus using command : ./gradlew publish
 

#### Java Maven Project: Build Jar & Upload to Nexus
    
 

