# CodeCraftHub

## Project Overview

CodeCraftHub is a personal learning goal tracker API designed for developers to manage and track their learning courses. It provides a simple RESTful API to create, read, update, and delete courses, helping users stay organized and focused on their learning objectives.

## Features

- Add new courses with details such as name, description, target completion date, and status.
- Retrieve a list of all courses or a specific course by ID.
- Update existing course information.
- Delete courses that are no longer needed.
- Track the status of each course with predefined values: `Not Started`, `In Progress`, and `Completed`.
- Get statistics about total courses and courses grouped by status.
- Search courses by name, description, or status.
- Automatically creates a JSON file for data storage if it does not exist.

## Installation Instructions

1. Clone the repository:

   ```bash
   git clone <repository-url>
   cd codecrafthub
   ```

2. Install dependencies:

   Make sure you have Node.js installed. Then run:

   ```bash
   npm install
   ```

## How to Run the Application

To start the server, use the following command:

```bash
npm start
```

The server will run on:

```text
http://localhost:5000
```

## API Endpoint Documentation

### 1. Add a New Course

Endpoint:

```http
POST /api/courses
```

Request body:

```json
{
  "name": "Course Name",
  "description": "Course Description",
  "target_date": "YYYY-MM-DD",
  "status": "Not Started"
}
```

The `status` value must be one of:

- `Not Started`
- `In Progress`
- `Completed`

Example:

```bash
curl -X POST http://localhost:5000/api/courses \
  -H "Content-Type: application/json" \
  -d '{"name":"JavaScript Basics","description":"Learn the fundamentals of JavaScript.","target_date":"2025-12-31","status":"Not Started"}'
```

PowerShell example:

```powershell
Invoke-RestMethod `
  -Uri "http://localhost:5000/api/courses" `
  -Method POST `
  -ContentType "application/json" `
  -Body '{"name":"JavaScript Basics","description":"Learn the fundamentals of JavaScript.","target_date":"2025-12-31","status":"Not Started"}'
```

### 2. Get All Courses

Endpoint:

```http
GET /api/courses
```

Example:

```bash
curl http://localhost:5000/api/courses
```

PowerShell example:

```powershell
Invoke-RestMethod -Uri "http://localhost:5000/api/courses" -Method GET
```

### 3. Get a Specific Course

Endpoint:

```http
GET /api/courses/:id
```

Example:

```bash
curl http://localhost:5000/api/courses/1
```

PowerShell example:

```powershell
Invoke-RestMethod -Uri "http://localhost:5000/api/courses/1" -Method GET
```

### 4. Update a Course

Endpoint:

```http
PUT /api/courses/:id
```

Request body:

```json
{
  "name": "Updated Course Name",
  "description": "Updated Description",
  "target_date": "YYYY-MM-DD",
  "status": "In Progress"
}
```

Example:

```bash
curl -X PUT http://localhost:5000/api/courses/1 \
  -H "Content-Type: application/json" \
  -d '{"status":"In Progress"}'
```

PowerShell example:

```powershell
Invoke-RestMethod `
  -Uri "http://localhost:5000/api/courses/1" `
  -Method PUT `
  -ContentType "application/json" `
  -Body '{"status":"In Progress"}'
```

### 5. Delete a Course

Endpoint:

```http
DELETE /api/courses/:id
```

Example:

```bash
curl -X DELETE http://localhost:5000/api/courses/1
```

PowerShell example:

```powershell
Invoke-RestMethod -Uri "http://localhost:5000/api/courses/1" -Method DELETE
```

### 6. Get Course Statistics

Endpoint:

```http
GET /api/courses/stats
```

Example:

```bash
curl http://localhost:5000/api/courses/stats
```

PowerShell example:

```powershell
Invoke-RestMethod -Uri "http://localhost:5000/api/courses/stats" -Method GET
```

Example response:

```json
{
  "success": true,
  "total_courses": 3,
  "by_status": {
    "Not Started": 1,
    "In Progress": 1,
    "Completed": 1
  }
}
```

### 7. Search Courses

Endpoint:

```http
GET /api/courses/search?q=term
```

The search term is matched against the course `name`, `description`, and `status` fields. The search is case-insensitive.

Example:

```bash
curl "http://localhost:5000/api/courses/search?q=JavaScript"
```

PowerShell example:

```powershell
Invoke-RestMethod -Uri "http://localhost:5000/api/courses/search?q=JavaScript" -Method GET
```

Example response:

```json
{
  "success": true,
  "query": "JavaScript",
  "count": 1,
  "courses": [
    {
      "id": 1,
      "name": "JavaScript Basics",
      "description": "Learn the fundamentals of JavaScript.",
      "target_date": "2025-12-31",
      "status": "Not Started",
      "created_at": "2026-04-16 11:30:00"
    }
  ]
}
```

## Troubleshooting

### Server Not Starting

Ensure you have Node.js installed and that you are in the correct project directory.

### File Read or Write Errors

Check file permissions for the directory where `courses.json` is created.

### Invalid Data Errors

Make sure the request body follows the required format and includes all necessary fields.

### Course Not Found

Ensure the course ID you are trying to access exists in the system.

