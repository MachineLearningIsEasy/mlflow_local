Deploy mlflow locally with postgresql and aws S3 bucket.

An AWS account is required.

Steps:

1. Create aws bucket (in S3 service)
2. Download file with Credentials (in section My Security Credentials)
3. Install awscli (for MacOs  "brew install awscli" in terminal)
4. Enter parameters to access aws services via awscli
	- awscli configure (in MacOS terminal)
and enter the data from the file uploaded in step 2. (for the zone you need to enter the bucket zone - in the bucket settings)
5. Check the correctness of access using the command
	- aws s3api list-buckets
You will see a list of buckets.
6. Start PG docker container (in the terminal in the project directory, execute the command docker-compose up)
7. Install mlflow
	- pip3 install mlflow
8. Run mlflow
mlflow server --backend-store-uri postgresql://user_name:password@0.0.0.0/database_name \
                --default-artifact-root s3://bucket_name \
                --host 0.0.0.0 \
                --port 5000
user_name, password, database_name in database.env file
9. Follow the link http://0.0.0.0:5000/