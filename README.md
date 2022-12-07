# To create the Repo in ECR and push/pull the image to the same

## Step1 : Creating the Repository
Go to the console -> ECR -> create a Repository 

<img width="960" alt="image" src="https://user-images.githubusercontent.com/67600604/206119468-64f3a3bb-e461-407e-8741-1cf23c4227ef.png">

Now, create a private repository, name your repository and click on create.

<img width="960" alt="image" src="https://user-images.githubusercontent.com/67600604/206112008-e6c33f00-8c77-4772-8f39-5366f60579e9.png">

Our Private Repository has been created. 

<img width="958" alt="image" src="https://user-images.githubusercontent.com/67600604/206112343-42d7bcba-5653-41b5-bfb1-0c9f87a2b6e1.png">

## Step2 : Creating our own Image.

Launch an EC2 instance and SSH into it and install Docker in the instance.
```
sudo yum update
sudo yum search docker
sudo yum info docker
sudo yum install docker
sudo systemctl enable docker 
```

Now, docker is installed , we will create the image now 
```
mkdir shruti
cd shruti
vim Dockerfile
```

<img width="503" alt="image" src="https://user-images.githubusercontent.com/67600604/206116147-4430dd46-b930-4e88-8115-f05fcbbbba48.png">

write this content in the Dockerfile 

Now to run and build the images , use the following commands 

```
docker build -t awsimage1:v1 .
docker run -dit awsimage1:v1

check the image and the running containers by these commands, respectively
docker images
docker ps
```

Our Image is now created

## Step3 : Push the Image to the ECR Repo 

Go to the Repo that we have created in step1 and click on the "view push commands".

<img width="752" alt="image" src="https://user-images.githubusercontent.com/67600604/206117582-07a66c3e-6a73-41a0-b20f-c9ed5c814bf9.png">

Now configure aws-cli to get the password for login into the repository.

```
aws configure
Access Key ID [None]: Access Key 
AWS Secret Access Key [None]: Secret Key 
Default region name [None]: 
Default output format [None]: 
```

It will ask for username and password
configure your aws-cli and type this command to get the password 

<img width="410" alt="image" src="https://user-images.githubusercontent.com/67600604/206118158-525578e9-5be7-462b-8dd1-fd15203f469d.png">

Take the repo ID and Login using the command with username and password

<img width="476" alt="image" src="https://user-images.githubusercontent.com/67600604/206117824-6aaa05d8-4fe8-40f2-ac70-f92055256204.png">

Rename your image to the repo name 
```
docker tag awsimage1:latest 655645242246.dkr.ecr.ap-south-1.amazonaws.com/shruti-test1:latest
```
And, push into the Repository
```
docker push 655645242246.dkr.ecr.ap-south-1.amazonaws.com/shruti-test1:latest
```

Now, our image has been pushed into the repository 

Go to the ECR -> Repositories -> <Your Repository name>

<img width="743" alt="image" src="https://user-images.githubusercontent.com/67600604/206119177-e7842b7b-29b4-4956-85da-ef9c85de32d4.png">






