How can I grant a user access to a specific folder in my Amazon S3 bucket?
https://aws.amazon.com/premiumsupport/knowledge-center/s3-folder-user-access/
https://www.youtube.com/watch?v=aq4y5B1jjMg
==================================================================================
I want to grant an AWS Identity and Access Management (IAM) user access to a specific folder in my Amazon Simple Storage Service (Amazon S3) bucket. How can I do that? 

Resolution
Use an IAM policy to grant the user access to the folder and to specify which Amazon S3 actions the user can perform on the folder. For example, the following IAM policy allows a user to download objects from the folder awsexamplebucket/media using the Amazon S3 console. The policy includes these statements:

AllowStatement1 allows the user to list the buckets that belong to their AWS account. The user needs this permission to be able to navigate to the bucket using the console.
AllowStatement2A allows the user to list the folders within awsexamplebucket, which the user needs to be able to navigate to the folder using the console. The statement also allows the user to search on the prefix media/ using the console.
AllowStatement3 allows the user to list the contents within awsexamplebucket/media.
AllowStatement4A allows the user to download objects (s3:GetObject) from the folder awsexamplebucket/media.
{
 "Version":"2012-10-17",
 "Statement": [
   {
     "Sid": "AllowStatement1",
     "Action": ["s3:ListAllMyBuckets", "s3:GetBucketLocation"],
     "Effect": "Allow",
     "Resource": ["arn:aws:s3:::*"]
   },
  {
     "Sid": "AllowStatement2A",
     "Action": ["s3:ListBucket"],
     "Effect": "Allow",
     "Resource": ["arn:aws:s3:::awsexamplebucket"],
     "Condition":{"StringEquals":{"s3:prefix":["","media"]}}
    },
  {
     "Sid": "AllowStatement3",
     "Action": ["s3:ListBucket"],
     "Effect": "Allow",
     "Resource": ["arn:aws:s3:::awsexamplebucket"],
     "Condition":{"StringLike":{"s3:prefix":["media/*"]}}
    },    
   {
     "Sid": "AllowStatement4A",
     "Effect": "Allow",
     "Action": ["s3:GetObject"],
     "Resource": ["arn:aws:s3:::awsexamplebucket/media/*"]
   }
 ]
}
As another example, the following IAM policy grants the user access to all Amazon S3 actions in the folder awsexamplebucket/media using either the console or programmatic methods like the AWS Command Line Interface (AWS CLI) or the Amazon S3 API. The differences from the previous IAM policy are:

AllowStatement2B includes "s3:delimiter":["/"], which specifies the forward slash character (/) as the delimiter for folders within the path to an object. It's a best practice to specify the delimiter if the user will make requests using the AWS CLI or the Amazon S3 API.
AllowStatement4B allows the user to perform all object-level actions on the folder awsexamplebucket/media.
{
 "Version":"2012-10-17",
 "Statement": [
   {
     "Sid": "AllowStatement1",
     "Action": ["s3:ListAllMyBuckets", "s3:GetBucketLocation"],
     "Effect": "Allow",
     "Resource": ["arn:aws:s3:::*"]
   },
  {
     "Sid": "AllowStatement2B",
     "Action": ["s3:ListBucket"],
     "Effect": "Allow",
     "Resource": ["arn:aws:s3:::awsexamplebucket"],
     "Condition":{"StringEquals":{"s3:prefix":["","media"],"s3:delimiter":["/"]}}
    },
  {
     "Sid": "AllowStatement3",
     "Action": ["s3:ListBucket"],
     "Effect": "Allow",
     "Resource": ["arn:aws:s3:::awsexamplebucket"],
     "Condition":{"StringLike":{"s3:prefix":["media/*"]}}
    },
   {
     "Sid": "AllowStatement4B",
     "Effect": "Allow",
     "Action": ["s3:*"],
     "Resource": ["arn:aws:s3:::awsexamplebucket/media/*"]
   }
 ]
}
