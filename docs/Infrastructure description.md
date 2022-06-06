# Infrastructure Description

To deploy this application we used the following services from AWS:
- RDS for the database
- Elastic Beanstalk for the server
- S3 for the UI

## Relational Database Service (RDS)
We used RDS to deploy the PostgreSQL database for the udagram app. First, we use Amazon RDS to create the database in the following steps.
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
finally we change the value of `POSTGRES_HOST` environment variable to the endpoint value. As well as `DB_PORT`, `POSTGRES_PASSWORD`, `POSTGRES_USERNAME` and `POSTGRES_DB` if we used different values. 
![Connectivity & security](/docs/screenshots/RDS/RDS7.png)

