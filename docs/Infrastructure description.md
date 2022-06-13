# Infrastructure Description

To deploy this application we used the following services from AWS:
- RDS for the database
- Elastic Beanstalk for the server
- S3 for the UI

## Relational Database Service (RDS)
We used RDS to deploy the PostgreSQL database for the Udagram app. First, we use Amazon RDS to create the database in the following steps.
- `create database`
 ![Create database](/docs/screenshots/RDS/RDS1.png)

- `standard`
- `postgreSql`
![Engin options](/docs/screenshots/RDS/RDS2.png)

- `free tier`
![Templates](/docs/screenshots/RDS/RDS3.png)

- `database-1` database instance
![Settings](/docs/screenshots/RDS/RDS4.png)

- `db-t3-micro`, uncheck `Enable storage autoscaling`
![Instance configuration, Storage](/docs/screenshots/RDS/RDS5.png)

- `Public access`, `Create new` VPC security group
![VPC security group](/docs/screenshots/RDS/RDS6.png)

- Create a database named `udagram`
![Additional configuration](/docs/screenshots/RDS/RDS9.png)

- `create database`
![Create database](/docs/screenshots/RDS/RDS6.png)

Finally, we change the value of the `POSTGRES_HOST` environment variable to the endpoint value. As well as `DB_PORT`, `POSTGRES_PASSWORD`, `POSTGRES_USERNAME` and `POSTGRES_DB` if we used different values. 
![Connectivity & security](/docs/screenshots/RDS/RDS7.png)

## S3
We used S3 to deploy the frontend for the Udagram app. We start by creating a bucket to store files in the `www` folder where the frontend is built.

- `Create bucket`
![Create bucket](/docs/screenshots/S3/bucket_create1.png)

- `Bucket name`
![General configuration](/docs/screenshots/S3/bucket_create2.png)

- uncheck `Block all public access`
![Block Public Access settings for this bucket](/docs/screenshots/S3/bucket_create3.png)

- `Create bucket`
![Create bucket](/docs/screenshots/S3/bucket_create4.png)

After creating a bucket we go to bucket `properties`.
![Create bucket](/docs/screenshots/S3/bucket_properties1.jpg)

- Then we scroll down to Static website hosting and click edit.
![Static website hosting](/docs/screenshots/S3/bucket_properties2.jpg)

- Then we enable static web hosting, choose the index document to be `index.html`, and click `Save changes`.
![Save changes](/docs/screenshots/S3/bucket_properties3.jpg)

To make bucket accessible to the public we go to `permissions`. We scroll down to `Bucket policy` and click `Edit`.
![Edit bucket policy](/docs/screenshots/S3/bucket_permissions1.jpg)

- Then paste the following bucket policy and `Save changes`.
```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PublicReadGetObject",
			"Principal": "*",
			"Effect": "Allow",
			"Action": [
			    "s3:GetObject"
			    ],
			"Resource": [
			    "arn:aws:s3:::shorouk4udagram/*"
			    ]
		}
	]
}
```
![Create bucket](/docs/screenshots/S3/bucket_permissions2.jpg)

We now go to `objects` to upload the website contents and click `upload`.
![Objects](/docs/screenshots/S3/bucket_upload1.jpg)

- We upload `www` folder
![www](/docs/screenshots/S3/bucket_upload3.jpg)

- Uploading...
![Uploading](/docs/screenshots/S3/bucket_upload4.jpg)

- After upload finishes click `Close`
![Close](/docs/screenshots/S3/bucket_upload5.jpg)

We go back to properties to find the URL `http://shorouk4udagram.s3-website-us-east-1.amazonaws.com`
![Bucket website endpoint](/docs/screenshots/S3/bucket_properties4.jpg)

In order to deploy the frontend using CircleCI, we had to `enable ACLs` to fix `(AccessControlListNotSupported) when calling the PutObject operation: The bucket does not allow ACLs` error.

![Edit Object Ownershp](/docs/screenshots/S3/bucket_permissions4.jpg)


## Elastic Beanstalk
To run our udagram-api on a server, we use the Elastic Beanstalk service. We deploy udagram-api according to the following steps.
1. From cmd we run the `aws configure` command from the root. Then set `AWS Access Key ID`, `AWS Secret Access Key`, `Default region name`, and `Default output format`.
2. Navigate to `udagram-api` in the terminal using the `cd udagram-api` command.
3. Run `eb init` command` from there to create `.elasticbeanstalk/config.yml`.
4. Run `eb create udagram-env` to create an environment.
5. Use the environment by running the `eb use udagram-env` command.
6. Finally, deploy the application using the `eb deploy` command.

## Resources
- [For an Amazon S3 bucket deplolyent from Guithub how do I fix the error AccessControlListNotSupported: The bucket does not allow ACLs?](https://stackoverflow.com/questions/70333681/for-an-amazon-s3-bucket-deplolyent-from-guithub-how-do-i-fix-the-error-accesscon)