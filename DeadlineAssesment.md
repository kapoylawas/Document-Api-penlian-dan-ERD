# CRUD Deadline Assesment

## GET /api/assessments

```json
[
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
        "month": "December",
        "submission_deadline": "2024-12-31"
      }
    ]
  }
]
```

## POST /api/assessments

```json
{
  "year": 2024,
  "periods": [
    {
      "month": "January",
      "submission_deadline": "2024-01-31"
    },
    ...
  ]
}
```

## Response success:

```json
{
  "message": "Assessment period created successfully."
}
```

## Response error:

```json
{
  "message": "Assessment and Years must not blank."
}
```

## PUT /api/assessments/{year}

```json
{
  "periods": [
    {
      "month": "January",
      "submission_deadline": "2024-01-25" // contoh perubahan
    },
    ...
  ]
}
```

## Response Success

```json
{
  "message": "Assessment period updated successfully."
}
```

## Response Error: Jika tahun yang diminta sudah dipilih

```json
{
  "error": "This year has already been selected and cannot be modified."
}
```

## DELETE /api/assessments/{year}

```json
{
  "message": "Assessment period deleted successfully."
}
```

## Get: /api/assessments/{year}/{month}

```json
{
  "year": 2024,
  "month": "January",
  "submission_deadline": "2024-01-31"
}
```

## GET /api/employees

```json
[
  {
    "id": 1,
    "name": "John Doe",
    "department": "Sales"
  },
  {
    "id": 2,
    "name": "John Doexx",
    "department": "Sales"
  }
]
```

## POST /api/employees

```json
{
  "name": "John Doe",
  "department": "Sales"
}
```

## response successfully

```json
{
  "message": "Employee created successfully."
}
```

## Response error:

```json
{
  "message": "Name and Department must not blank."
}
```

### Mengambil daftar assessment yang terkait dengan karyawan tertentu.

## GET /api/employees/{employeeId}/assessments

```json
{
  "employeeId": 1,
  "assessments": [
    {
      "id": 1,
      "assessment_period_id": 1,
      "assessment_category": "Performance",
      "submission_deadline": "2024-01-31",
      "created_at": "2023-12-01"
    },
    ...
  ]
}
```

## POST /api/employees/{employeeId}/assessments

```json
{
  "assessment_period_id": 1,
  "assessment_category": "Performance",
  "submission_deadline": "2024-01-31"
}
```

## Response successfully

```json
{
  "message": "Employee assessment created successfully."
}
```

## Response error:

```json
{
  "message": "assessment_category and submission_deadline must not blank."
}
```

# Mengambil detail assessment untuk karyawan tertentu.
## GET /api/employees/{employeeId}/assessments/{assessmentId}

```json
{
  "assessment_period_id": 1,
  "assessment_category": "Performance",
  "submission_deadline": "2024-01-31",
  "created_at": "2023-12-01",
  "kpis": [
    {
      "id": 1,
      "key_performance_indicator": "Sales Target",
      "weight": 30,
      "target": 100,
      "notes": "Achieve monthly target",
      "attachment": "link_to_attachment"
    },
    ...
  ]
}
```

# Memperbarui assessment untuk karyawan tertentu.
## PUT /api/employees/{employeeId}/assessments/{assessmentId}

```json
{
  "submission_deadline": "2024-01-25",
  "kpis": [
    {
      "key_performance_indicator": "Sales Target",
      "weight": 30,
      "target": 100,
      "notes": "Updated notes",
      "attachment": "link_to_new_attachment"
    },
    ...
  ]
}
```

## response 
```json
{
  "message": "Assessment updated successfully.",
  "created_at": "2023-12-01" // diupdate jika ada perubahan
}
```

# Menambahkan KPI baru untuk assessment tertentu.
## POST /api/employees/{employeeId}/assessments/{assessmentId}/kpis

```json
{
  "key_performance_indicator": "Sales Target",
  "weight": 30,
  "target": 100,
  "notes": "Achieve monthly target",
  "attachment": "link_to_attachment"
}
```

## Respon Sukses 
```json
{
  "message": "KPI added successfully."
}
```

## Respon Error
```json
{
    "message": "KPI added Erro Not Found."
}
```
## Memperbarui KPI untuk assessment tertentu.
## PUT /api/employees/{employeeId}/assessments/{assessmentId}/kpis/{kpiId}
```json
{
  "key_performance_indicator": "Updated Target",
  "weight": 30,
  "target": 120,
  "notes": "Revised target",
  "attachment": "link_to_updated_attachment"
}
```

## Respon Success
```json
{
  "message": "KPI updated successfully."
}
```

## Respon Error
```json
{
  "message": "KPI updated Error."
}
```

## Mengirimkan penilaian untuk assessment tertentu.
## POST /api/employees/{employeeId}/assessments/{assessmentId}/submit
```json
{
  "key_performance_indicator": "Updated Target",
  "weight": 30,
  "target": 120,
  "notes": "Revised target",
  "attachment": "link_to_updated_attachment"
}
```

## Respon Successfuly
```json
{
  "message": "KPI updated successfully."
}
```

## Respon Error
```json
{
  "message": "KPI updated error."
}
```

## Penelian Denda
```json
{
  "submission_date": "2024-01-30" // contoh tanggal pengiriman
}
```

## response success
```json
{
  "message": "Assessment submitted successfully.",
  "penalty": false // true jika lewat batas waktu
}
```


## response error
```json
{
  "error": "Submission deadline has passed. A penalty will be applied."
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

+-------------------+
|      Employees    |
+-------------------+
| id (PK)           |
| name              |
| department        |
+-------------------+
           |
           | 1
           |
           | N
+------------------------+
| Employee_Assessments   |
+------------------------+
| id (PK)                |
| employee_id (FK)       |
| assessment_period_id (FK) |
| assessment_category     |
| submission_deadline     |
| created_at             |
+------------------------+
           |
           | N
           |
           | 1
+--------------------------+
|    Key_Performance_Indicators |
+--------------------------+
| id (PK)                  |
| employee_assessment_id (FK) |
| key_performance_indicator |
| weight                   |
| target                   |
| notes                    |
| attachment               |
+--------------------------+
```