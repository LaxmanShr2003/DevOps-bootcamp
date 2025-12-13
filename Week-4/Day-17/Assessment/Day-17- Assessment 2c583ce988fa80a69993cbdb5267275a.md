# Day-17- Assessment

Install AWS CLI 

**Step 1: If you have not installed aws cli in your machine, run this below command**

curl "[https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip](https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip)" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

**Or if you want to update** 

curl "[https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip](https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip)" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update

**Step 2: Configuration of aws cli**

Required: Access key and aws secrect access key

As we are using the sandbox environment here, sandbox provides us these credentials after successful opening. 

Go to the right top where you can find “*aws details” . Click the button* then copy the credentials.


**Step 3: Open your terminal, and use this command to access aws console**

	aws configure

              Now lets create a bucket and list the bucket. Using below command we can create bucket . After successful creation of bucket, system will provide name of the bucket as output

![image.png](images/image%202.png)

lets list the bucket

![image.png](images/image%203.png)