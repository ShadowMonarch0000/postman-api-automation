# REST API Automation Testing using Postman

[![Postman API Automation Tests](https://github.com/ShadowMonarch0000/postman-api-automation/actions/workflows/postman-api-tests.yml/badge.svg)](https://github.com/ShadowMonarch0000/postman-api-automation/actions/workflows/postman-api-tests.yml)

A beginner-friendly API testing project that automates REST API checks with **Postman** and runs them in **GitHub Actions CI/CD**.

## Project Overview

This project tests the demo REST API provided by [JSONPlaceholder](https://jsonplaceholder.typicode.com/). Postman test scripts validate HTTP status codes, JSON responses, response fields, data types, filtering, result limits, related comments, negative cases, and basic response-time expectations.

> **Note:** JSONPlaceholder is a public demo API. Create, update, and delete requests are simulated; changes are not persisted like they would be in a production database.

## Tech Stack

- Postman — request collection and JavaScript assertions
- Postman CLI — command-line collection execution
- GitHub Actions — automated CI/CD workflow
- JSONPlaceholder — demo REST API

## Test Coverage

The collection currently contains **14 requests** across these areas:

| Area | Example checks |
|---|---|
| GET posts | Status code, JSON content, response time, required fields, data types |
| GET single post | Requested ID matches response; headers and fields are valid |
| POST create | HTTP 201 and expected response fields |
| PUT update | HTTP 200 and updated values |
| PATCH partial update | HTTP 200 and updated title |
| DELETE | Successful response status |
| Negative tests | Invalid post and invalid endpoint return 404 |
| Users API | User list and single-user fields |
| Filter posts | All returned posts match user ID 1 |
| Limit results | Exactly five posts; IDs are numeric and unique |
| Post comments | Comments relate to post 1; required fields and email format |
| Boundary test | Post ID 0 returns 404 |

The collection uses Postman's built-in test scripts. The total assertion count can change as tests are added or edited.

## Run Locally

### 1. Requirements

- Node.js and npm
- Postman CLI

Install Postman CLI:

```bash
npm install -g postman-cli
```

### 2. Run the collection

Download or clone this repository, open a terminal in the folder containing the collection, and run:

```bash
postman collection run "REST API Automation - JSONPlaceholder.postman_collection.json" --env-var "baseUrl=https://jsonplaceholder.typicode.com" --env-var "postId=1" -r cli,html
```

Review the terminal output for passed and failed assertions. The HTML reporter generates a report file; check the CLI output for the report location.

## Continuous Integration (GitHub Actions)

The workflow at [`.github/workflows/postman-api-tests.yml`](.github/workflows/postman-api-tests.yml) runs the collection automatically on pushes to `main`, pull requests, and manual workflow dispatches.

- View workflow runs: [GitHub Actions](https://github.com/ShadowMonarch0000/postman-api-automation/actions)
- The workflow attempts to upload an HTML report as an artifact, including when tests fail.
- To download a report, open a successful or failed workflow run, scroll to **Artifacts**, and select **postman-api-test-report**. Extract the ZIP file to view the HTML report.

## Repository Structure

```text
.
├── .github/
│   └── workflows/
│       └── postman-api-tests.yml
├── REST API Automation - JSONPlaceholder.postman_collection.json
└── README.md
```

## Learning Goals

- Understand REST methods: GET, POST, PUT, PATCH, DELETE
- Write automated assertions in Postman
- Validate response status, structure, headers, and data types
- Test query parameters, related resources, and invalid inputs
- Run API tests automatically through CI/CD

## Disclaimer

This is an educational portfolio project using a public demo API. Its test results demonstrate the collection and workflow at the time of execution; they are not a guarantee of a production API's availability or behavior.
