# RTT - Reddit topic tracker
## Overview

The Reddit topic tracker App is designed to collect textual data from Reddit. It employs a modular architecture with microservices to ensure scalability and flexibility. This set of repositories constitutes a comprehensive Reddit Data ETL (Extract, Transform, Load) tool designed to efficiently extract text data from Reddit, transform it, and load it into MongoDB. The tool is orchestrated using Apache Airflow and optimizes data processing by leveraging Redis for intermediate storage.

## Architecture

1. Data Ingestion: The data ingestion process involves collecting posts and comments from _Reddit_. This is accomplished using a Python microservice that interacts with the _Reddit_ API. The service fetches data based on specified subreddits, keywords, or other criteria, and then stores it in a temporary data store.

2. _ETL_ Pipeline Once the data is ingested, it undergoes the _ETL_ process:
- **Extract**: Another microservice extracts the data from the temporary store and prepares it for transformation.

- **Transform**: The transformed data is processed to extract valuable insights, such as sentiment analysis, keyword extraction, and user engagement metrics. Python libraries like NLTK and spaCy can be used for natural language processing tasks.

- **Load**: The transformed data is stored in a _MongoDB_ database for easy retrieval and analysis.

3. Redis for Optimization: _Redis_ is used within the _ETL_ pipeline to cache frequently accessed data and optimize processing speed. This helps reduce the load on the Reddit API and improves overall system performance.

## Technology Stack

- **Apache Airflow**: Orchestrates the ETL pipeline and scheduling tasks.
- **Python Microservices**: Python microservice used for data ingestion, transformation, and loading.
- **MongoDB**: Stores the transformed Reddit text data.
- **Redis**: Caches data to optimize ETL processes.
- **Python Flask**: Provides a RESTful API for interaction with the application.
- **Docker**: Used to run the applications in container mode.

## Application Components

The Reddit Data ETL Tool consists of the following repositories, each with its specific functionality:

1. **db-API Repository**:
   - Responsible for starting the MongoDB and API containers.
   - MongoDB is used to persist the transformed text data.
   - The API container provides the interface for registering Reddit comments with the external API.

2. **Collector-API Repository**:
   - Hosts the Collector API, which offers functions for extracting and transforming Reddit data.
   - Utilizes Redis for optimizing data transfer between the extract and transform steps.
   - Runs both the API and Redis containers.

3. **Collector-Airflow Repository**:
   - Contains the Apache Airflow DAGs responsible for scheduling the ETL tasks.
   - Orchestrates the data extraction, transformation, and loading processes.

## Running the Application

To run the Reddit Data ETL Tool, follow these steps:

1. **db-API**:
   - Clone the repository: `https://github.com/RTT-app/db-api.git`
   - Navigate to the repository: `cd db-api`
   - Use the Makefile to start the MongoDB and API containers: ```$ make run```

2. **Collector-API**:
   - Clone the repository: `git clone https://github.com/RTT-app/collector-api.git`
   - Navigate to the repository: `cd collector-api`
   - Use the Makefile to start the API and Redis containers: ```$ make run```

3. **Collector-Airflow**:
   - Clone the repository: `git clone https://github.com/RTT-app/collector-airflow.git`
   - Navigate to the repository: `cd collector-airflow`
   - Use the Makefile to run Apache Airflow and schedule the ETL tasks: ```$ make docker-up```

## Customization

You can customize each repository to suit your specific Reddit data processing needs. Modify the ETL logic, API endpoints, and Airflow DAGs as required.

## Contributing

Feel free to contribute to any of the repositories by opening issues, proposing improvements, or submitting pull requests.
