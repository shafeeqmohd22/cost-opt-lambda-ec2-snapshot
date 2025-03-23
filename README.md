# cost-opt-lambda-ec2-snapshot
Identifying Stale EBS Snapshots
In this example, we'll create a Lambda function that identifies EBS snapshots that are no longer associated with any active EC2 instance and deletes them to save on storage costs.

Description:
The Lambda function fetches all EBS snapshots owned by the same account ('self') and also retrieves a list of active EC2 instances (running and stopped). For each snapshot, it checks if the associated volume (if exists) is not associated with any active instance. If it finds a stale snapshot, it deletes it, effectively optimizing storage costs.

Steps:

1. Create Ec2 Instance
2. Create Snapshot
3. Create a lambda function
4. Copy the code from GitHub repo to the lambda function.
5. Deploy and test the lambda function.
6. Increase the lambda execution time from 3 sec to 10 sec for testing.
7. Test the lambda function again, you'll see permission for describe snapshot missing.
7. Create the policy with describe and delete of the snapshot permissions. And associate to the lambda Role.
8. Test the lambda function again, you'll see permission for describe instance and volume is missing.
9. Create the policy with describe instance & Volume permissions. And associate to the lambda Role.
10. Run the lambda function again, you'll see now it ran successfully without error. But since you have instance and volume associated with Snapshot, it doesnot
have any action to take.
11. Now try deleting the instance and run the lambda function again, it will delete the snapshot as it doesn't have its associated EC2 or volume.
12. Now try create a volume & snapshot without EC2 instance, and run the lambda function, you'll see that it will delete the snapshot as volume is nt associated to any instance.
13. In order to automate the triggering of lambda function, you can create a role under EventBridge to perform the activity every day or a week to check if any stale sessions available
and delete them.
