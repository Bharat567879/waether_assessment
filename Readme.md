# Weather API

This API allows you to access weather data for various locations and years. The data can be filtered by date and location. The API also provides statistical information on the weather data.

# Pre-Requisites

To run this application make sure your machine has pre-installed:
- Docker 
- Python

# Folder Structure
```
.
├── data                   
    ├── wx_data
    ├── yld_data
    
├── logs                    
├── static                 
├── __init__.py             
├── .coveragerc
├── .gitignore
├── app.py             
├── docker-compose.yml
├── dockerfile
├── ingest.py
├── README.md
├── requirements.txt
└── test_api.py          
```


# Set-Up

- Start Docker and run the following command:
```bash
docker-compose up -d --build
```

- Ingest the give data:

```bash
docker-compose exec web flask create
```

- The API can now be accessed at http://localhost:5003.

## **Swagger**
You can access all the end-points using Swagger at
[http://localhost:5003/swagger/](http://localhost:5003/swagger/)

#### Weather data
- This endpoint returns a paginated list of weather records:
```
GET /api/weather/
```

![](/static/get-weather.png)

- You can use `page` query parameter to get a particular page.
```
GET /api/weather/?page=1
```
![](/static/get-weather-page.png)
- You can filter the results by date and station using `date` and `station` query parameters.
```
GET /api/weather/?date=19850103&station=USC00257715
```
![](/static/get-weather-filter.png)

#### Statistics
- This endpoint returns statistical information about the weather data.
```
GET /api/weather/stats/
```
![](/static/get-weather-stat.png)

- You can use `page` query parameter to get a particular page.
```
GET /api/weather/stats/?page=1
```
![](/static/get-weather-stat-page.png)
- You can filter the results by date and station using `date` and `station` query parameters.
```
GET /api/weather/stats/?date=19850103&station=USC00257715
```

## Testing
For testing the application is leveraging Pytest. You can run test using:
```bash
docker-compose exec web pytest
```
The test coverage is 99%

![](/static/test-coverage.png)

## AWS Deployment Steps:

1. Set up RDS instance:
    - Create a PostgreSQL instance in Amazon RDS.
    - Configure security groups and connectivity.

2. ECS Cluster:
    - Create an ECS cluster.
    - Define a task definition for the Flask application container.
    - Set up a service to run the container in the cluster.


3. Fargate:
    - Use Fargate launch type for serverless container management.
    - Define the networking and load balancer settings.

4. CI/CD Pipeline:
    - Use AWS CodePipeline or GitHub Actions for automated deployment.

<br>
 First, I will set up an Amazon RDS instance with PostgreSQL, with configuring security groups and connectivity to secure data access. Next, I will create an ECS (Elastic Container Service) cluster, defining a detailed task definition for the Flask application container and setting up a service to ensure the container runs reliably within the cluster.

To simplify container management, I will go for AWS Fargate, which allows for serverless management. I defined the necessary networking settings and will integrate a load balancer to ensure effective traffic distribution. Finally, I will establish a CI/CD pipeline using AWS CodePipeline, automating the deployment process and ensuring continuous integration and delivery of updates with minimal manual intervention.