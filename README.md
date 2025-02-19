# Tobacco Report Service API

This project is a Spring Boot application designed to retrieve, process, and display information from the **FDA's Tobacco Problem Reports API**. It uses **embedded MongoDB** for local testing and provides several endpoints to interact with and store tobacco product problem reports.

## Project Overview

The application meets the following requirements:
- Retrieves data from the FDA's Tobacco Problem Reports API:
    - https://open.fda.gov/apis/tobacco/problem/how-to-use-the-endpoint/
- Provides endpoints to:
    - Find the most common tobacco product mentioned in reports.
    - List reports submitted on a specific date.
    - Store specific report records with details such as `report_id`, `date_submitted`, `product_type`, and `problem_description`.

### Key Features
- **Embedded MongoDB**: An in-memory embedded MongoDB instance is used for local testing.
- **Swagger Documentation**: All endpoints are documented in Swagger for easy testing and exploration.
- **Clean Code Practices**: The code follows SOLID principles and test-driven development (TDD) where applicable.

## Prerequisites

To run this application locally, you need:

- **Java 17** or later
- **Maven 3.9.9** or later

The application uses **embedded MongoDB**, so no standalone MongoDB installation is required.

## Setup Instructions

### Clone the Repository

```bash
git clone https://github.com/anuj-bv-kumar/tobacco-report-service.git
cd tobacco-report-service
```

### Build the Application

Use Maven to build the application:

```bash
mvn clean install
```
### Testing the Application

Run the following command to execute the tests:

```bash
mvn test
```

### Running the Application Locally

Start the application using the following command. Embedded MongoDB allows you to test the application locally:

```bash
mvn spring-boot:run
```

This will start the Spring Boot application on the default port, typically **localhost:8080**.

### Swagger Documentation

Swagger UI is available for API documentation and testing. Once the application is running, navigate to:

```
http://localhost:8080/swagger-ui.html
```

## API Endpoints

### 1. **Find the Most Common Tobacco Product**

- **Endpoint**: `GET /api/fda/tobacco/reports/products/common`
- **Description**: Returns the most frequently mentioned tobacco product type from the API data.
- **Response**: JSON containing the most common product.

### 2. **List Reports Submitted on a Specific Date**

- **Endpoint**: `GET /api/fda/tobacco/reports`
- **Parameters**:
    - `date_submitted` (query parameter): Date in `MM/dd/yyyy` format.
- **Description**: Lists all reports submitted on the specified date.
- **Response**: JSON Object with list of reports.

### 3. **Save a Report Record**

- **Endpoint**: `POST /api/fda/tobacco/reports`
- **Description**: Stores a specific report record in the embedded MongoDB database.
- **Request Body**:
  ```json
  {
      "reportId": "6780",
      "dateSubmitted": "06/21/2019",
      "productType": "Cigarettes",
      "problemDescription": "Packaging issues"
  }
  ```
- **Response**: JSON object with the saved report details.

## Project Structure

- **Controller**: Handles incoming HTTP requests.
- **Service**: Contains business logic and interacts with the repository.
- **Repository**: Manages data persistence with embedded MongoDB.
- **Model**: Defines the structure of different DTO's.
- **Entity**: Defines the structure of entity class(es).
- **Mapper**: Handles mapping between DTO and entity using mapStruct.
- **Config**: Contains spring boot config classes.
- **Exception**: Handles custom exceptions.

## Additional Notes

- **Embedded MongoDB**: The application uses an embedded MongoDB instance, enabling quick local testing without a standalone MongoDB installation.
- **Profiles**: The application currently uses `default` Spring Boot profiles for local testing however different profiles can be added for different environments for e.g. application-test.properties for test, application-prod.properties for production.