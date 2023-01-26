1.	First, we need a Lambda function which will take snapshot of EBS or any particular Volume ID.
2.	Goto lambda function and start creating a new function.
3.	Select Author from scratch and give function name.
4.	Select the runtime environment. Her we will use Python 3.9
5.	Expand the Change default execution role and select use an existing role.
6.	Make a new role in IAM and give EC2 full access and CloudWatch full access. 
7.	Select that role for this Lambda function.
8.	Write the code for EBS snapshot:
```python
import boto3
def lambda_handler(event, context):
    ec2 = boto3.client('ec2')
    result = ec2.describe_volumes( Filters=[{'Name': 'volume-id', 'Values': ['<VolumeID_for_snapshot>']}])
        for volume in result['Volumes']:
        print("Backing up {volume['VolumeId']} in {volume['AvailabilityZone']}")
       # Create snapshot
        result = ec2.create_snapshot(VolumeId=volume['VolumeId'],Description='Created by Lambda backup function ebs-snapshots')
        # Get snapshot resource
        ec2resource = boto3.resource('ec2')
        snapshot = ec2resource.Snapshot(result['SnapshotId'])
        # Find name tag for volume
        if 'Tags' in volume:
            for tags in volume['Tags']:
                if tags["Key"] == 'Name':
                    volumename = tags["Value"]
        else:
            volumename = 'N/A'
        # Add volume name to snapshot for easier identification
        snapshot.create_tags(Tags=[{'Key': 'Name','Value': volumename}])
```
9.	Now we will configure the CloudWatch trigger which will call the function in every 24hrs and take snapshots of the EBS Volume. 
10.	To add trigger, click on Add trigger in the function overview tab above the code.
11.	Select the source as EventBridge (CloudWatch Events) and create a new rule.
12.	Give name for the rule and in the schedule expression section enter ```‘rate(1 day)’```.
13.	 After this CloudWatch will trigger lambda function every day and take snapshot of the volumeID specified in the code.
