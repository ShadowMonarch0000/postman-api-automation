# REST API Automation Testing using Postman

[![Postman API Automation Tests](https://github.com/ShadowMonarch0000/postman-api-automation/actions/workflows/postman-api-tests.yml/badge.svg)](https://github.com/ShadowMonarch0000/postman-api-automation/actions/workflows/postman-api-tests.yml)

An API automation testing project using **Postman**, **Postman CLI**, and **GitHub Actions**. It tests REST endpoints, validates responses with JavaScript assertions, and runs automatically in CI.

## Project Overview

The project tests [JSONPlaceholder](https://jsonplaceholder.typicode.com/), a public demo REST API. It includes a main collection for common API scenarios and a separate data-driven collection that tests multiple post IDs using JSON test data.

> **Note:** JSONPlaceholder is a demo API. POST, PUT, PATCH, and DELETE responses are simulated; changes are not persisted like they would be in a production database.

## Tech Stack

- **Postman** — API requests and JavaScript test assertions
- **Postman CLI** — command-line execution and HTML reports
- **GitHub Actions** — automated CI workflow on pushes, pull requests, and manual runs
- **JSONPlaceholder** — demo REST API

## Test Coverage

### Main collection

| Area | Example validations |
|---|---|
| GET requests | Status codes, JSON content, headers, response time, required fields and data types |
| Schema validation | JSON response structure |
| POST, PUT and PATCH | Expected status codes and returned field values |
| DELETE | Successful response status |
| Negative and boundary cases | Invalid post, invalid endpoint, and post ID 0 |
| Users and comments | Required fields and relationships between resources |
| Query parameters | Filtering by user, result limits, and empty results when no user matches |
| Pagination | Five posts returned for the requested pagination window, with expected IDs |

### Data-driven collection

The separate **Post ID Data-Driven Tests** collection uses `post-id-test-data.json` to run the same request and assertions against **six post IDs**. Each iteration checks the status code, JSON response, returned post ID, expected user ID, and required fields.

This demonstrates reusable tests with external test data rather than duplicating a request for every input.

## Run Locally

### 1. Requirements

- Node.js and npm
- Postman CLI

Install Postman CLI:

```bash
npm install -g postman-cli
```

### 2. Run the main collection

Run these commands from the repository root:

```bash
postman collection run "REST API Automation - JSONPlaceholder.postman_collection.json" --environment "JSONPlaceholder Environment.postman_environment.json" -r cli,html
```

### 3. Run the data-driven tests

```bash
postman collection run "Post ID Data-Driven Tests.postman_collection.json" --environment "JSONPlaceholder Environment.postman_environment.json" --iteration-data "post-id-test-data.json" -r cli,html
```

Review the CLI output for passed and failed assertions. The HTML reporter generates a report; check the CLI output for its location.

## Continuous Integration

The workflow in [`.github/workflows/postman-api-tests.yml`](.github/workflows/postman-api-tests.yml) runs both collections on pushes to `main`, pull requests, and manual workflow dispatches.

- [View workflow runs and CI status](https://github.com/ShadowMonarch0000/postman-api-automation/actions)
- The workflow uploads an HTML report artifact when available, even if a test step fails.
- To view a report, open a workflow run, scroll to **Artifacts**, download `postman-api-test-report`, and extract the ZIP file.

## Repository Structure

```text
.
├── .github/
│   └── workflows/
│       └── postman-api-tests.yml
├── REST API Automation - JSONPlaceholder.postman_collection.json
├── JSONPlaceholder Environment.postman_environment.json
├── Post ID Data-Driven Tests.postman_collection.json
├── post-id-test-data.json
└── README.md
```

## Skills Demonstrated

- REST API testing with GET, POST, PUT, PATCH, and DELETE
- Writing reusable JavaScript assertions in Postman
- Validating response codes, payloads, schemas, data types, and relationships
- Testing query parameters, pagination, negative cases, and boundary inputs
- Data-driven testing with JSON iteration data
- Running automated tests in CI with GitHub Actions
- Generating and publishing HTML test reports as workflow artifacts

## Disclaimer

This is an educational portfolio project using a public demo API. Test results demonstrate the behavior observed during a particular run and do not guarantee the availability or behavior of a production API.
