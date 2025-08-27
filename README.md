
SBDL - Spark Bulk Data Load Application
Overview
The SBDL - Spark Bulk Data Load Application is a PySpark-based data engineering project designed to build a scalable data pipeline for a multinational bank. The project facilitates the movement of master data from an MDM (Master Data Management) platform to a Kafka cluster, where downstream systems can consume the data for their respective requirements.

This project follows software engineering best practices, including modular design, unit testing, CI/CD integration, and resource optimization for production deployment.

Features
Data Ingestion: Reads master data from Hive tables for a given load_date.
Data Transformation: Combines and transforms data from multiple tables into a structured JSON format.
Kafka Integration: Sends transformed data to a Kafka topic in a scalable and efficient manner.
Unit Testing: Implements automated unit tests using the pytest framework for robust code validation.
CI/CD Pipeline: Supports automated builds, testing, and deployment using GitHub Actions.
Resource Optimization: Provides detailed resource estimation for driver and executor configurations in production.
Project Structure
SBDL/
├── conf/
│   ├── sbdl.conf             # Application-specific configurations
│   ├── spark.conf            # Spark-specific configurations
├── lib/
│   ├── __init__.py           # Python library initializer
│   ├── ConfigLoader.py       # Configuration loader functions
│   ├── DataLoader.py         # Functions to load data from Hive tables
│   ├── Transformations.py    # Transformation logic for data processing
│   ├── Utils.py              # Utility functions (e.g., Spark session creation)
│   ├── Logger.py             # Log4J-based logging setup
├── test_data/
│   ├── accounts_sample.csv   # Sample input data for accounts
│   ├── party_samples.csv     # Sample input data for parties
│   ├── address_samples.csv   # Sample input data for addresses
├── results/
│   ├── final_df.json         # Expected output JSON for testing
├── tests/
│   ├── test_pytest_sbdl.py   # Unit test cases using PyTest
├── sbdl_main.py              # Application entry point
├── spark-submit.sh           # Shell script to submit the Spark job
├── Pipfile                   # Dependency management using pipenv
├── log4j.properties          # Log4J configuration for logging
├── .gitignore                # Files to exclude from Git tracking
└── README.md                 # Project documentation
Requirements
Software
Python 3.10
PySpark
Kafka (Confluent Cloud recommended for testing)
Hadoop Cluster (with Hive integration)
Python Dependencies
Managed using pipenv. Key dependencies include:

pyspark
pytest
chispa (optional, for DataFrame comparison)
Getting Started
Local Setup
Clone the repository:
bash

git clone https://github.com/<your-repo-name>.git
cd SBDL
Install dependencies:
bash

pipenv install
Run the application:
bash

python sbdl_main.py --env local --load_date 2023-10-01
Testing
Run unit tests using pytest:

bash

pytest tests/test_pytest_sbdl.py
Kafka Integration
Setting Up Kafka
Create a free Confluent Cloud account at https://www.confluent.io/.
Set up a Kafka cluster and create a topic.
Update sbdl.conf with Kafka connection details:
kafka.bootstrap.servers
kafka.topic
kafka.api_key
kafka.api_secret
Sending Data to Kafka
The application sends transformed data to Kafka using PySpark's DataFrame.write API with the Kafka format.

Resource Estimation
Driver Configuration
CPU Cores: 2
Memory: 4 GB
Memory Overhead: 1 GB
Executor Configuration
CPU Cores: 5 per executor
Memory: 10 GB per executor
Memory Overhead: 1 GB
Number of Executors: 40–160 (depending on cluster capacity)
CI/CD Pipeline
The project includes a CI/CD pipeline for automated testing and deployment:

Unit Testing: Validates code changes using pytest.
Build: Packages the application for deployment.
Deployment: Deploys the application to QA and production environments.
Contribution Guidelines
Create a feature branch from the dev branch:
bash

git checkout -b feature/<feature-name> dev
Commit and push changes to your feature branch.
Raise a pull request to merge changes into the dev branch.
Ensure all unit tests pass and code reviews are completed before merging.
License
This project is licensed under the MIT License. See the LICENSE file for details.
