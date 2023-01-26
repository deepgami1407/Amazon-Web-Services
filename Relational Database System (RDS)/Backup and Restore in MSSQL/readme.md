**Step 1: Create MSSQL Database.**

1.	Goto RDS and start creating Database.
2.	Select Easy create method and select Microsoft SQL Server.
3.	Select free tier for database instance size.
4.	Give name for the database instance, master username and password.
5.	Click on create database.

    ![image](https://user-images.githubusercontent.com/73180656/214888023-c6d48f2f-aaf9-4692-bdaf-5c9cea25b407.png)

**Step 2: Backup and Restore in MSSQL.**

1.	When the database becomes available go to the modify option to modify the database instance.
2.	Now, go to Option groups and create a new option group.
3.	Give name, engine, engine version and create it.
4.	Goto that option group and add option for backup and restore.
5.	Select option name ‘SQLSERVER_BACKUP_RESTORE’ , select create new IAM role and give name to that role.
6.	Give the name of the S3 bucket to use for backup and restore.
7.	Apply immediately and add option.
8.	Now, make the database publicly accessible by modifying the below option:

    ![image](https://user-images.githubusercontent.com/73180656/214888135-20612922-57f9-4989-b9c4-ef65f834335c.png)

9.	Then, assign the option group that we created:

    ![image](https://user-images.githubusercontent.com/73180656/214888196-fe0f3b37-0ee6-41c9-ab4f-18818f6c40e7.png)

10.	 Save the changes immediately.
11.	 Add inbound rule in MSSQL security group to connect to the database.
12.	 Download Microsoft SQL Server Management Studio (SSMS) by clicking [this link](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16&tabs=command-line).
13.	 Connect to MSSQL database using database endpoint, username and password.

     ![image](https://user-images.githubusercontent.com/73180656/214889119-79a007a1-51bd-4aab-a2fa-33bc94cbda95.png)

14.	 Here I have Table_A in TEST_A database.
15.	 We will backup this database and restore it to a database named TEST_B.
16.	 Run the below query in the SSMS studio to backup the TEST_A database in S3 bucket.
```
exec msdb.dbo.rds_backup_database
@source_db_name='TEST_A', @s3_arn_to_backup_to='arn:aws:s3:::<bucketname>/backupfile_name.bak';
```
17.	 This will send the backup file in the s3 bucket we associated in option group.
18.	 Now, to restore the that backup use the below command:
exec msdb.dbo.rds_restore_database
```
@restore_db_name='TEST_B',
@s3_arn_to_restore_from='arn:aws:s3:::/ <bucketname>/backupfile_name.bak';
```
19.	 We have restored data of TEST_A in TEST_B

     ![image](https://user-images.githubusercontent.com/73180656/214889572-01eb65e1-8450-4655-b239-db2c9f93ef7a.png)
