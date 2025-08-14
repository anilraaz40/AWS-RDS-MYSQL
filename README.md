# AWS-RDS-MYSQL

## 1. Launch a Free-Tier MySQL Database in RDS

<pre>
Go to AWS Management Console → search RDS.

Click Create database.

Database creation method → choose Standard create.

Engine options:

Engine type: MySQL

Version: select the latest Free Tier eligible version.

Templates → choose Free tier.

Settings:

DB instance identifier: e.g., mydb

Master username: e.g., admin

Master password: set a strong password.

DB instance size:

DB instance class: db.t3.micro (Free tier).

Storage:

Storage type: General Purpose (SSD)

Allocated storage: 20 GB (Free tier limit).

Enable storage autoscaling: Optional.

Connectivity:

VPC: choose the default VPC.

Public access: Yes (to allow external connections).

Choose existing security group or create new one.

Database authentication: Password authentication.

Leave other settings as default → Click Create database.

Wait until the DB instance status changes to Available (takes ~5–10 minutes).
</pre>
## 2. Configure Security Group for RDS

<pre>
Go to EC2 → Security Groups.

Find the security group attached to your RDS instance.

Click Inbound rules → Edit inbound rules.

Add:

Type: MySQL/Aurora

Port: 3306

Source: My IP (for local) OR Security Group of your EC2 instance (for EC2 connection).

Save rules.
</pre>
## 3. Connect RDS from EC2 Instance
### Step 1: Install MySQL Client on EC2
<pre>
sudo apt update
sudo apt install mysql-client -y

</pre>
### Step 2: Get RDS Endpoint
<pre>
Go to RDS → Databases → mydb.
Copy the Endpoint (e.g., mydb.xxxxxx.ap-south-1.rds.amazonaws.com) and note the port (3306).
</pre>
### Step 3: Connect Using MySQL Client
<pre>
  mysql -h RDS-ENDPOINT -u admin -p
</pre>
<p>Enter your RDS password when prompted.</p>
<p>If connection is successful, you’ll get the MySQL prompt:</p>
<pre>
mysql>
</pre>
## 4. Test the Connection
### Inside MySQL prompt:
<pre>
CREATE DATABASE testdb;
USE testdb;
CREATE TABLE users (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50));
INSERT INTO users (name) VALUES ('Anil');
SELECT * FROM users;

</pre>
