# WordPress-application-hosted-on-EC2-with-a-RDS
Create security group and allow MySQL/MariaDB: 3306 in 
inbound rule

![image](https://github.com/user-attachments/assets/247af0f0-2caf-4eb1-9ba3-13498a458e81)

![image](https://github.com/user-attachments/assets/9332a993-17c1-40aa-ba8d-3716d5d10567)

First create database Go to the Amazon RDS console. Click 
“Create database”.

![image](https://github.com/user-attachments/assets/9ba93aab-cdd0-409e-ada2-4b777cceda31)

Enter a unique name for the “DB instance identifier”.

![image](https://github.com/user-attachments/assets/49937a35-ac29-4e9d-a20c-782c330791a2)

Set the “Master username” and “Master password” for the database.

![image](https://github.com/user-attachments/assets/4aa48a9a-84c3-4a8a-a5da-83c8fa89ed79)

Select the security group created for the database.
![image](https://github.com/user-attachments/assets/20b36952-a870-41cc-91d8-daa0940def38)

Database is created.

![image](https://github.com/user-attachments/assets/9c4d3e8c-6a68-4888-8454-4cbe586fe83d)

Go to the Amazon EC2 console.
![image](https://github.com/user-attachments/assets/b9ecfa1d-9263-4ec6-829d-ac7e0d45787c)

#### Click “Launch Instance”, Choose a Ubuntu AMI. Choose an instance 
type, such as t2. micro, Choose a VPC and subnet.
Configure security group rules to allow inbound traffic on the 
appropriate port for the type of database you are using (e.g. port 3306 
for MySQL).

![image](https://github.com/user-attachments/assets/efaae09d-9769-4d5f-82e8-0a573f809585)

````
apt update -y
````

![image](https://github.com/user-attachments/assets/8d5e9a60-e955-4c2e-aa0d-d8ac584c91d5)

````
apt install mysql-server -y
````
![image](https://github.com/user-attachments/assets/a3178751-da7f-4d28-9fc7-d95d88d7a091)

Run the following command in your terminal to connect to your 
MySQL database. Replace “<user>” and “<password>” with the 
master username and password you configured when creating your 
Amazon RDS database. -h is host which is RDS database endpoint. 

````
mysql -h <rds-database-endpoint> -u <user> -p<password>
````
Finally, create a database user for your WordPress application and give 
the user permission to access the wordpress database.

#### Run the following commands in your terminal:
````
CREATE DATABASE wordpress;
````
````
CREATE USER 'wordpress' IDENTIFIED BY 'wordpress-pass';
````
````
GRANT ALL PRIVILEGES ON wordpress.* TO wordpress;
````
````
FLUSH PRIVILEGES;
````
````
Exit
````
![image](https://github.com/user-attachments/assets/e336d8ec-893e-4141-b4cc-6ff948b03b21)

````
apt-get install apache2 -y
````
![image](https://github.com/user-attachments/assets/4a250f7b-9fb2-4b4e-b1fb-6d31660f920e)

To start the Apache web server, run the following command in your 
terminal

````
systemctl restart apache2
````

Hit the public Ip of instance on new tab of browsers

![image](https://github.com/user-attachments/assets/b768c24c-d112-48aa-b5f2-8c43434297e1)

#### First, download and uncompressed the software by running the 
following commands in your terminal:

````
wget https://wordpress.org/latest.tar.gz
````
![image](https://github.com/user-attachments/assets/3d15464a-3cd1-47c6-8497-1eab34871c51)

````
tar -xvf latest.tar.gz
````

![image](https://github.com/user-attachments/assets/f390b25c-d8c0-415b-9472-3927cf663d51)

you will see a tar file and a directory called WordPress with the 
uncompressed contents using the ls command

![image](https://github.com/user-attachments/assets/8f1f6568-59d4-4504-bf38-1bfc4957fc00)

Change the directory to the WordPress directory and create a copy of 
the default config file using the following commands. Open the wpconfig.php file

![image](https://github.com/user-attachments/assets/e2187b8c-a07c-4aff-909d-ba7bc8fde4f7)

#### Edit the database configuration by changing the following lines:
- DB_NAME: your RDS database name
- DB_USER: The name of the user you created in the database in 
the previous steps
- DB_PASSWORD: The password for the user you created in the 
previous steps
- DB_HOST: The hostname of the database means your database 
endpoint
![image](https://github.com/user-attachments/assets/0facc047-fbe7-4610-aeda-5a4aed74eb02)

#### The second configuration section you need to configure is the 
Authentication Unique Keys and Salts.
You can replace the entire content in that section with the help of 
WordPress Secret Key Generator on google or GPT.

![image](https://github.com/user-attachments/assets/79a09e98-2dfc-46d2-841d-09a945c716fa)

#### First, install the application dependencies you need for WordPress. In 
your terminal, run the following command.
````
sudo apt install php libapache2-mod-php php-mysql -y
````

![image](https://github.com/user-attachments/assets/75383d71-c55e-4a7d-a52c-a6dcc1a11af4)

Copy your WordPress application files into the /var/www/html 
directory used by Apache.
````
 sudo cp -r wordpress/* /var/www/html/
````

Finally, restart the Apache web server
````
systemctl restart apache2
````
![image](https://github.com/user-attachments/assets/dc5ae203-1e14-45a9-8d72-7d449efd0c31)

#### In Browse “ec2-public-ip/wp-admin/” and you should see the 
WordPress welcome page.

![image](https://github.com/user-attachments/assets/d125f346-f1b5-4ce3-8c3f-7f73cc5c1a43)


![image](https://github.com/user-attachments/assets/61370311-0240-40f5-8ceb-2ca3fc6a336f)

Configure username and password
![image](https://github.com/user-attachments/assets/903bd7f6-5fc5-4610-a065-cdff0e32a6e3)

![image](https://github.com/user-attachments/assets/f31d560c-94bc-4804-ac15-d780e6e58ae8)









