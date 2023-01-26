1.	First, we need 2 MySQL database instances. We transfer the table data from one database instance to s3 and then from s3 we use that file to make a table in another database instance.
2.	Here we have 2 database instances named rds and rds2.
3.	We transfer data from rds to rds2.
4.	First login to the rds database instance using ec2 and make sure that ec2 has s3FullAccess role.
5.	To login to the rds instance, run the below command in ec2:
```
mysql -h [db_hostname] -P 3306 -u [db_user] -p
```
6.	Now create a database, create table in it and insert some entries in that table.

    ![image](https://user-images.githubusercontent.com/73180656/214885668-00527164-21f4-45e1-bbd2-6255e063b946.png)
    
7.	Exit MySQL.
8.	To transfer the table data file to s3 run the below command in ec2:
```
mysqldump -h [db_hostname] -u [db_user] -p[db_passwd] [databasename] [tablename] | aws s3 cp - s3://[s3_bucketname]/[mysqldump_filename].sql
```
.
    ![image](https://user-images.githubusercontent.com/73180656/214885818-a39d5cd9-be6b-4907-bcec-6729b038596c.png)

9.	Now, we will pull that file in our ec2 machine. Use the following command to do this:
```
aws s3 cp s3://[s3_bucket_name]/ [mysqldump_filename].sql .
```
10.	 Now we have the sql file in the ec2 instance.
11.	 We will import that file to a new database instance (rd2) using the following command:
```
mysql -h [db_hostname] -u [db_user] -p [databasename] < [mysqldump_filename].sql]
```
.
    ![image](https://user-images.githubusercontent.com/73180656/214885959-907b1770-9aac-4490-a95b-3d3f8d94e979.png)

