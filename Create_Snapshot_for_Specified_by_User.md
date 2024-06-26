...
Description: This code is used to create the snapshot for the AWS EC2 Instance Id specified by the user and display the Snapshot Id

'''
import boto3

session = boto3.Session(profile_name="default", region_name="us-east-2")
ec2_con_cli = session.client("ec2")

# Get the Instance Id from the User
Instance_Id = input("Enter the Instance Id: ")

# Get all the Instances present in that particular region (Here it is: us-east-2)
all_instances = []
ec2_con = session.client("ec2")
for each_in in ec2_con.describe_instances()['Reservations']:
    for details in each_in['Instances']:
        all_instances.append(details['InstanceId'])

# If the Instance Id entered by the user is present in the instance list, create the snapshot of it and display the Snapshot Id
if Instance_Id in all_instances:
    response = ec2_con_cli.create_snapshots(
    Description='Creating snapshot',
    InstanceSpecification={
        'InstanceId': Instance_Id,
        'ExcludeBootVolume': False
    },
    )['Snapshots']
    for value in response:
        print('Snapshot created successfully, Snapshot Id is {}'.format(value['SnapshotId']))
else:
    print("Please enter the valid Instance Id!")
