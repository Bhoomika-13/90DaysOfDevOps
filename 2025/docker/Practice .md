# Practice on Docker containerization 

##  Created Docker file for docker image build it and run

## Two applications Python and Java 

### steps 

1. Connect you EC2 instance

![image](https://github.com/user-attachments/assets/9a9c11ba-f393-4a60-ad70-390cabc186b5)

2. install Docker on your instance `sudo apt-get install docker.io`

![image](https://github.com/user-attachments/assets/dac798d4-b94a-4b28-abfb-af8666c13c94)

3. Clone your repository

![image](https://github.com/user-attachments/assets/c3ca0d50-40f7-462e-9754-50b3f88ed124)

4. Go to docker file
![image](https://github.com/user-attachments/assets/23b853b3-862a-4917-b7d3-bf81dc28360a)

5. remove existing `rm -v Dockerfile`
   
![image](https://github.com/user-attachments/assets/102ee154-8a34-47af-a037-7aa44f713b9f)

6. create Dockerfile with the help of vim `vim Dockerfile`
   
![image](https://github.com/user-attachments/assets/4c6b3389-e96a-4cdd-89a6-f825acc54359)

7. To create image will run command `docker build -t python-app:latest .`

![image](https://github.com/user-attachments/assets/ed58a856-f16f-451c-892d-acc0ba6340a5)

8. Chcek the status with command `docker ps`

![image](https://github.com/user-attachments/assets/bb77055b-1894-41fe-af37-733dc980ca85)

9. Run into port

![image](https://github.com/user-attachments/assets/9767bf22-aaad-42af-abca-12a797d89242)

# Created 2-tier Flask app connected with MSQL app with the help of docker networking 

1. connect your server with with your ec2 instance
   
![image](https://github.com/user-attachments/assets/f45d9bea-08e9-4fde-b209-60cca337000a)

3. Clone your repo

![image](https://github.com/user-attachments/assets/f9b41a29-3eb0-4e8d-8090-068e1cacac68)

4. Go to docker project directory to check disk/storage Run the command `df -h` and for Ram `free -h`
   
![image](https://github.com/user-attachments/assets/15c792eb-75c6-4b3a-bc1b-c118eb1b4632)

5. Free up the Ram with command `sudo sysctl -w vm.drop_caches=3`

![image](https://github.com/user-attachments/assets/341a3339-11ae-41d1-8a53-ecd73f5636fe)

6. Go to two-tier flask app & `cat Docker file`
   
![image](https://github.com/user-attachments/assets/9d667668-435e-4378-bd57-cc5ee5d64390)

7. Create file `touch .env` , open the .env file `vim .env` add confg. MSQL & `cat .env`

![image](https://github.com/user-attachments/assets/6bedd2f9-14be-4d2a-9033-51f787680b18)

8. Run this two-tier application using without docker-compose `docker build -t flask-app .`

![image](https://github.com/user-attachments/assets/427b3c30-9746-4651-a7f2-2b17e484a93a)

9. Need to run MSQL container before that need to create user bridge with command `docker network create twotier` check the network status 

![image](https://github.com/user-attachments/assets/acb991e5-144d-4180-9198-b465d04b7e74)
![image](https://github.com/user-attachments/assets/61882def-ea4f-43b8-82fa-0968173bb62d)

10. To check inside Network id details `docker inspect "network id"`
![image](https://github.com/user-attachments/assets/3e57fc09-4413-4920-82fe-ee98ba687994)

11. Creating MYSQL container Run MSQL with detach mode `-d`, name for identification `--name` network creation `--network`, given environment variable `-e` volume attachment `-v` port maping `p`

![image](https://github.com/user-attachments/assets/0ab3b9d6-e0ae-44fc-b626-368247c54e1b)

12. Check twotier app has container attached `docker inspection "id"`

![image](https://github.com/user-attachments/assets/23253de2-6d99-472c-8511-8300293095d2)

13. Run the two-tier flask app/ Backend container with the command `docker run -d --name flaskapp --network=twotier -e MYSQL_HOST=mysql -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_DB=tws_db -p 5000:5000 flask-app:latest`

![image](https://github.com/user-attachments/assets/18a57025-6cad-41b9-9c1e-01437830391b)

14. Run on browser with the port 5000

![image](https://github.com/user-attachments/assets/4381a548-55d9-440e-a0de-4a2eafb4c0c8)
 








 



   








   









