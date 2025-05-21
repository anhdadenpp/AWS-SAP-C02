# Access S3 from Private EC2 instance using VPC Endpoint
## Architecture
![1_52_34](https://github.com/user-attachments/assets/0a70779d-592d-466f-bb4a-cec322ac817c)

## Project Details
### Task Details 
1. Sign in to AWS Management Console 
2. SSH into the EC2 instance 
3. Check Docker Version and add user to the Docker Group 
4. Download Eclipse Mosquitto Docker Image 
5. Create a Configuration File for Mosquitto 
6. Run the MQTT Broker 
7. Verify the MQTT Broker 
8. Test the MQTT Broker

### Step
1. Create EC2 Instance :
- t2.micro
- Linux 2
- Security group : SSH, HTTP, HTTPS, SSH 1883
2. SSH to EC2 Instance
3. Check Docker Version and add user to the Docker Group
- Run the below command to Update your package index:
```
sudo yum update -y
```
- Add your user to the Docker group:
```
sudo usermod -aG docker $USER
```
- Run the below command to verify and check docker version:
```
docker --version
```
4. Download Eclipse Mosquitto Docker Image
- Pull the Eclipse Mosquitto Docker image: 
```
sudo docker pull eclipse-mosquitto:latest
```
5. Create a Configuration File for Mosquitto
- Pull the Eclipse Mosquitto Docker image:
```
mkdir –p /home/ec2-user/mosquitto
```

- Create a file named mosquitto.conf file in the directory:
```
sudo nano /home/ec2-user/mosquitto/mosquitto.conf
```
- Copy and paste the following content inside the file, and close and save the file by pressing Ctrl+X followed by Y and Enter:
```
listener 1883
allow_anonymous true
```
6. Run the MQTT Broker
- Run the docker container with the configuration file mounted:
```
sudo docker run -d --name mqtt-broker -p 1883:1883 -v /home/ec2-user/mosquitto/mosquitto.conf:/mosquitto/config/mosquitto.conf eclipse-mosquitto:latest
```
7. Verify the MQTT Broker
- Check the running containers:
```
sudo docker container ps
```
- Verify the logs of the MQTT broker container:
```
sudo docker container logs mqtt-broker
```
8. Test the MQTT Broker
- Execute the below command in the shell to subscribe to a topic:
```
sudo docker container exec mqtt-broker mosquitto_sub -i mosq_sub1 -t "#"
```
- Open a new terminal of the EC2 instance and execute the below command to Publish a message:
```
sudo docker container exec mqtt-broker mosquitto_pub -t bedroom/temperature -m "bedroom_temperature celsius=20"
```
