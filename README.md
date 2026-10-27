# Customer Accounts Microservice

![Build Status](https://github.com/YOUR_GITHUB_USERNAME/devops-capstone-project/actions/workflows/ci-build.yaml/badge.svg)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.9](https://img.shields.io/badge/Python-3.9-green.svg)](https://shields.io/)

This repository contains the DevOps Capstone Project: a Customer Accounts RESTful microservice built with Flask, tested with nose, checked by GitHub Actions CI, secured with Talisman and CORS, containerized with Docker, deployed to Kubernetes/OpenShift, and delivered by a Tekton CD pipeline.

## API

| Method | Endpoint             | Description        |
|--------|----------------------|--------------------|
| POST   | /accounts            | Create an account  |
| GET    | /accounts            | List all accounts  |
| GET    | /accounts/{id}       | Read an account    |
| PUT    | /accounts/{id}       | Update an account  |
| DELETE | /accounts/{id}       | Delete an account  |

## Author

Yash Baldawa

## License

Licensed under the Apache License. See [LICENSE](LICENSE)
