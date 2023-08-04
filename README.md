# Extract and Transform Weather Data with Airflow
This project uses Apache Airflow to extract weather data from an API, transform the data, and load it into an S3 bucket. The workflow is designed to run daily and can be easily customized to extract weather data for any city.

# Requirements
* Python 3.6 or higher
* Apache Airflow
* Pandas
* Boto3
# Installation
Clone the repository:


```git clone https://github.com/chaba-victor/Simple-ETL-Pipeline-Automation-With-Airflow.git```


Install the required packages:

```pip install pandas boto3 apache-airflow ```

Set up AWS credentials:
You'll need to set up AWS credentials to save the transformed data to an S3 bucket. You can do this by creating a new IAM user with S3 permissions and adding the credentials to your environment variables or AWS config file.

# Set up Airflow:
You'll need to set up Airflow to run the workflow. Follow the instructions in the [official Airflow documentation](https://airflow.apache.org/docs/apache-airflow/stable/index.html) to install and configure Airflow.

# Add the DAG to Airflow:
Copy the weather_dag.py file to the dags folder in your Airflow installation directory. You may need to restart the Airflow scheduler and webserver for the DAG to appear in the Airflow UI.

# Set up the weather API connection:
In the Airflow UI, go to the Admin tab and select Connections. Click the Create button and fill in the following details:

* Conn Id: weathermap_api
* Conn Type: HTTP
* Host: api.openweathermap.org
* Port: 8080
* Login: (leave blank)
* Password: (leave blank)
* Extra: {"endpoint": "/data/2.5/weather?q=Portland&APPID=YOUR_API_KEY"}
* Replace YOUR_API_KEY with your OpenWeatherMap API key.

# Usage
Once you've set up the DAG and connections, the workflow will run automatically on the schedule you've set (default is daily). You can monitor the progress of the workflow in the Airflow UI.

The transformed weather data will be saved to an S3 bucket in CSV format. You can use this data for analysis or visualization.

# Customization
To extract weather data for a different city, modify the endpoint parameter in the HttpSensor and SimpleHttpOperator tasks in the weather_dag.py file. You'll also need to update the transform_load_data function to extract the relevant data for the new city.

You can customize the workflow further by adding new tasks or modifying the existing tasks. Refer to the official Airflow documentation for more information on creating and managing Airflow workflows.

# License
This project is licensed under the MIT License. See the LICENSE file for details.
