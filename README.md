# Blynk-server-for-raspberrypi
## Blynk local server running on raspberry pi without port-forwarding .... 

### 1) first you need to install blynk local server by following :

## Quick local server setup on Raspberry PI

+ Login to Raspberry Pi via ssh;
+ Install java 8: 
        
        sudo apt install openjdk-8-jdk openjdk-8-jre
        
+ Make sure you are using Java 8

        java -version
        Output: java version "1.8"
        
+ now enter the following command:

      
       mkdir Blynk
       cd Blynk
      
        
+ Download Blynk server jar file (or manually copy it to Raspberry Pi via ssh and scp command): 
   
      wget "https://github.com/blynkkk/blynk-server/releases/download/v0.41.13/server-0.41.13-java8.jar"

+ Run the server on default 'hardware port 8080' and default 'application port 9443' (SSL port)

      java -jar server-0.41.13-java8.jar -dataFolder /home/pi/Blynk
        
   That's it! 

+ As output you will see something like that:

        Blynk Server successfully started.
        All server output is stored in current folder in 'logs/blynk.log' file.






## 2) now goto for ngrok setup:

+ Go to:
             
      https://ngrok.com/ 

+ and signup for a account;

+ after that goto 
                    
      https://ngrok.com/download 
     
  and download linux(arm) on your raspberry pi;

+ after that move the downloaded file in your /home/pi directory 

+ and simply enter the following command:

      unzip ngrok-stable-linux-arm.zip

      
      ./ngrok <authtoken>  
+
   #### here you need to copy the auth token from ngrok website you signup and simply replace it ####

+ now enter the following command:

      sudo nano /home/pi/.ngrok2/ngrok.yml

+ and enter tne following:
 
       authtoken: <your_auth_token>
       region: in

       tunnels:
         blynk:
            proto: tcp
            addr: 9443
         websocket:
            proto: tcp
            addr: 8080
    

+ after that hit : 
        
  control + X and then y ( to save the setup)

+ run:
    ```./ngrok start -all```

to start the ngrok service 

now you will see three line of ip address

>>>the line ending with 9443 is our ip and port for blynk app

>>>the line ending with 8080 is our ip and port for esp8266/32 code

simply replace the ip and ports in your code and blynk app:

now you are done;
you can access the blynk local server anywhere fron internet
"if you want more security you can generate ssl certificate by following 
https://github.com/blynkkk/blynk-server.git
