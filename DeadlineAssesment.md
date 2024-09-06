#Submisson deadline

### Create Deadline {{ tag: 'POST', label: '/v1/human-resource/submissionDeadline' }}

### Response
```json
   The message Successfully setting deadline
   The message Error years is not empty
```
### Body
```typescript
    const response = axios.post('/v1/human-resource/submissionDeadline/{years}', {
          year: 2024,
          periods: [
              {
              month: "January",
              submission_deadline: "2024-01-31"
              },
              {
              month: "February",
              submission_deadline: "2024-02-29"
              },
              {
              month: "March",
              submission_deadline: "2024-03-31"
              }
              // Tambahkan bulan lainnya sesuai kebutuhan
          ]
    })
```

### Response success
```json {{ title: '200' }}
        {
            "message": "Succesfuly setting deadline ."
        }
```
### Response error
```json {{ title: '404' }}
        {
            "message": "year is not empty and already exist."
        }
```

## List get tahun assessment dan periode. {{ tag: 'GET', label: '/v1/human-resource/submissionDeadline' }}

### Optional attributes

```json
   Unique this year submission deadline.
   The array of periods month, submission_deadline.
```

### Response

```json
  year : Get this year submission deadline
  periods : The array of periods mont submission deadline
  periods.month :  Get name month in array periods
  periods.submission_deadline : Get date submission_deadline in array periods
```

### Request end point

```typescript
  const response = axios.get('/v1/human-resource/submissionDeadline')
```

### Response 

 ```json {{ title: '200' }}
        {
            "year": 2024,
            "periods": [
            {
                "month": "January",
                "submission_deadline": "2024-01-31"
            },
            {
                "month": "February",
                "submission_deadline": "2024-02-28"
            },
            {
                "month": "Maret",
                "submission_deadline": "2024-12-31"
            }
            ...
            ]
        },
        ...
  ```

### List pertahun assessment dan periode. {{ tag: 'GET', label: '/v1/human-resource/submissionDeadline/{year}' }}
 
## This endpoint takes a list of specific years to display data with year parameter.

### Response

```json
  year : Get this year submission deadline
  periods : The array of periods mont submission deadline
  periods.month :  Get name month in array periods
  periods.submission_deadline : Get date submission_deadline in array periods
```

### Request end point

```typescript {{ title: 'axios' }}
    const response = axios.get('/v1/human-resource/submissionDeadline/{years}')
```

### Response 
```json {{ title: '200' }}
        {
            "year": 2024,
            "periods": [
            {
                "month": "January",
                "submission_deadline": "2024-01-31"
            },
            {
                "month": "February",
                "submission_deadline": "2024-02-28"
            },
            {
                "month": "Maret",
                "submission_deadline": "2024-12-31"
            }
            ...
            ]
        }
```

### Update setting deadline setiap tahun. {{ tag: 'PATCH', label: '/v1/human-resource/submissionDeadline/:id' }}

### Required attributes

```text
  year : The name for the year unique
  periods : The array of allowed periods name.
```

### Request
```text
  success : The message Successfully
  error : The message Error years already exists
```

```typescript {{ title: 'axios' }}
    const response = axios.patch('/v1/human-resource/submissionDeadline/:id', {
        year: 2024,
        created_at : 2024-01-31,
        periods: [
            {
            month: "January",
            submission_deadline: "2024-01-31"
            },
            {
            month: "February",
            submission_deadline: "2024-02-29"
            },
            {
            month: "March",
            submission_deadline: "2024-03-31"
            }
            // Tambahkan bulan lainnya sesuai kebutuhan
        ]
    })
```

Response success
```json {{ title: '200' }}
        {
            "message": "Successfully updated."
        }
```
Response error
```json {{ title: '404' }}
        {
            "message": "Error years already exists."
        }
```

### Delete Deadline . {{ tag: 'DELETE', label: '/v1/human-resource/submissionDeadline/:id' }}

## This endpoint allows you to delete from deadline list.

## Request
```typescript {{ title: 'axios' }}
    const response = axios.delete('/v1/human-resource/submissionDeadline/:id', {
        year: 2024,
        periods: [
            {
            month: "January",
            submission_deadline: "2024-01-31"
            },
            {
            month: "February",
            submission_deadline: "2024-02-29"
            },
            {
            month: "March",
            submission_deadline: "2024-03-31"
            }
            // Tambahkan bulan lainnya sesuai kebutuhan
        ]
    })
```

## Response
 ```json {{ title: '200' }}
        {
            "message": "Successfully delete form ."
        }
  ```

### Post Generate Denda . {{ tag: 'POST', label: '/v1/human-resource/generateDenda' }}

## This endpoint for generate denda.

## Notes

```text
  If the penalty basis is not provided or is null, the penalty amount will also be considered null.
  The current date should be dynamically fetched from the server at the time of the request to ensure accuracy.
```

## Request body

```typescript {{ title: 'axios' }}
    const response = axios.post('/v1/human-resource/generateDenda', {
            employee_id: "E123",
            submission_date: "2023-09-05",
            deadline_date: "2023-09-01",
            status: "draft",
            penalty_basis: 10000
    })
```

## Response
```json {{ title: '200' }}
        {
            "employee_id": "E123",
            "penalty_amount": 40000,
            "days_late": 4,
            "evaluation_status": "draft",
            "message": "Late submission penalty calculated."
        }
```

## All Report Denda . {{ tag: 'GET', label: '/v1/human-resource/reportDenda' }}

## Notes

```text
  The report will include all employees.
```

## Request

 ```typescript {{ title: 'axios' }}
    const response = axios.post('/v1/human-resource/reportDenda')
 ```

 ## Response

```json {{ title: '200' }}
    {
        "report": [
                {
                    "employee_id": "E123",
                    "employee_name": "John Doe",
                    "submission_date": "2023-09-05",
                    "deadline_date": "2023-09-01",
                    "days_late": 4,
                    "penalty_amount": 40000,
                    "evaluation_status": "draft"
                },
                {
                    "employee_id": "E456",
                    "employee_name": "Jane Smith",
                    "submission_date": "2023-09-03",
                    "deadline_date": "2023-09-01",
                    "days_late": 2,
                    "penalty_amount": 20000,
                    "evaluation_status": "submitted"
                }
        ],
        "message": "Report generated successfully."
    }
```

### Report Denda Get Range Date . {{ tag: 'GET', label: '/v1/human-resource/reportDenda?start_date=2023-09-01&end_date=2023-09-05' }}

## Endpoint for generate denda.

## Parameters

```text
  -  start_date (string, optional): Filter report from this date (YYYY-MM-DD).
  -  end_date (string, optional): Filter report until this date (YYYY-MM-DD).
```

## Notes

```text
  - The report will include all employees who have late submissions within the specified date range.
  - If no parameters are provided, the report will default to showing all penalties for the current month.
  - The API should handle cases where no penalties are found, returning an appropriate message and an empty report array.
```

## Request 

```typescript {{ title: 'axios' }}
    const response = axios.post('/v1/human-resource/reportDenda?start_date=2023-09-01&end_date=2023-09-05')
```

## Response

```json {{ title: '200' }}
    {
        "report": [
                {
                    "employee_id": "E123",
                    "employee_name": "John Doe",
                    "submission_date": "2023-09-05",
                    "deadline_date": "2023-09-01",
                    "days_late": 4,
                    "penalty_amount": 40000,
                    "evaluation_status": "draft"
                },
                {
                    "employee_id": "E456",
                    "employee_name": "Jane Smith",
                    "submission_date": "2023-09-03",
                    "deadline_date": "2023-09-01",
                    "days_late": 2,
                    "penalty_amount": 20000,
                    "evaluation_status": "submitted"
                }
        ],
        "message": "Report generated successfully."
    }
```

### History Denda. {{ tag: 'GET', label: '/v1/human-resource/historyDenda?employee_id=E123&start_date=2023-08-01&end_date=2023-09-05' }}

## Endpoint for histoy denda.

## Parameters

```text
  -  employee_id (string, optional): Filter by specific employee ID.
  -  status (string, optional): Filter by evaluation status (e.g., draft, submitted, not submitted).
  -  start_date (string, optional): Filter report from this date (YYYY-MM-DD).
  -  end_date (string, optional): Filter report until this date (YYYY-MM-DD).
```

## Notes 

```text
  - If no penalties are found for the specified filters, the response should contain an empty history array and an appropriate message.
  - The API should handle date validation and return errors for invalid date formats.
  - Pagination may be implemented if the history data set is extensive, to improve performance.
```

## Request

```typescript {{ title: 'axios' }}
    const response = axios.post('/v1/human-resource/historyDenda?employee_id=E123&start_date=2023-08-01&end_date=2023-09-05')
```

## Response 

```json {{ title: '200' }}
    {
        "history": [
            {
                "employee_id": "E123",
                "employee_name": "John Doe",
                "submission_date": "2023-09-05",
                "deadline_date": "2023-09-01",
                "days_late": 4,
                "penalty_amount": 40000,
                "evaluation_status": "draft",
                "penalty_date": "2023-09-06"
            },
            {
                "employee_id": "E123",
                "employee_name": "John Doe",
                "submission_date": "2023-08-28",
                "deadline_date": "2023-08-25",
                "days_late": 3,
                "penalty_amount": 30000,
                "evaluation_status": "submitted",
                "penalty_date": "2023-08-29"
            }
        ],
        "total_penalties": 70000,
        "message": "Penalty history retrieved successfully."
    }
```

# ERD 

```json
+-------------------+
|      Assessments  |
+-------------------+
| id (PK)           |
| year              |
+-------------------+
           |
           | 1
           |
           | N
+------------------------+
|    Assessment_Periods  |
+------------------------+
| id (PK)                |
| assessment_id (FK)     |
| month                  |
| submission_deadline     |
+------------------------+

+-------------------+               +---------------------+
|     Employee      |               |      Evaluation     |
+-------------------+               +---------------------+
| employee_id (PK)  |<---1       *--| evaluation_id (PK)  |
| employee_name     |               | employee_id (FK)    |
| department        |               | submission_date     |
+-------------------+               | deadline_date       |
                                     | status              |
                                     +---------------------+
                                                |
                                                | 1
                                                |
                                                |
                                                | 1
                                     +---------------------+
                                     |       Penalty       |
                                     +---------------------+
                                     | penalty_id (PK)     |
                                     | evaluation_id (FK)   |
                                     | days_late           |
                                     | penalty_amount       |
                                     | penalty_date         |
                                     +---------------------+
```