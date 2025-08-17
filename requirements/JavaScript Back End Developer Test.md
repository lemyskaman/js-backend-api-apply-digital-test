# JavaScript Back End Developer Test

## Table of Contents
1. Introduction
2. Requirements
3. Tasks
4. Evaluation Criteria
5. Submission Guidelines

---

## 1. Introduction
This test is designed to evaluate your skills as a JavaScript Back End Developer. Please read all instructions carefully and complete all tasks as described.

## 2. Requirements
- Node.js (latest LTS version recommended)
- Any framework or libraries of your choice (Express, Koa, etc.)
- Use of Git for version control
- Clear and concise documentation

## 3. Tasks
### 3.1. API Implementation
- Implement a RESTful API with the following endpoints:
  - `GET /items` – List all items
  - `POST /items` – Create a new item
  - `GET /items/:id` – Get a single item by ID
  - `PUT /items/:id` – Update an item by ID
  - `DELETE /items/:id` – Delete an item by ID
- Use in-memory storage (no database required)
- Each item should have at least: `id`, `name`, and `description`

### 3.2. Validation & Error Handling
- Validate input data for all endpoints
- Return appropriate HTTP status codes and error messages

### 3.3. Testing
- Write unit tests for all API endpoints
- Use any testing framework (Jest, Mocha, etc.)

### 3.4. Documentation
- Provide a README.md with:
  - Project description
  - Setup instructions
  - API documentation (endpoints, request/response examples)
  - How to run tests

## 4. Evaluation Criteria
- Code quality and organization
- Correctness and completeness of the implementation
- Proper use of Git (commits, messages, branching if needed)
- Quality of documentation
- Test coverage and reliability

## 5. Submission Guidelines
- Push your code to a public GitHub repository
- Share the repository link with the reviewer
- Ensure the repository contains all code, tests, and documentation

---

Good luck!
