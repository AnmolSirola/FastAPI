## What this Patient Management FastAPI app does

This is a simple Patient Management API built with FastAPI that stores and retrieves patient details from a `patients.json` file. It allows creating new patients, viewing patients, and sorting them based on attributes like height, weight, or BMI.

- PUT: For Updating
- POST: For Creating
- GET: For Retrieving 
---

## 🚀 API Features

### 1. View all patients
- Endpoint: `GET /view`
- Description: Returns all patients stored in the JSON database.

---

### 2. View a specific patient by ID
- Endpoint: `GET /patient/{patient_id}`
- Description: Fetch details of a single patient using their ID.
- Example: `/patient/P001`

---

### 3. Sort patients
- Endpoint: `GET /sort`
- Query Parameters:
  - `sort_by` → `height | weight | bmi`
  - `order` → `asc | desc`
- Description: Returns patients sorted by height, weight, or BMI in ascending/descending order.

---

### 4. Create a new patient
- Endpoint: `POST /create`
- Request Body (JSON Example):
```json
{
  "id": "P002",
  "name": "John Doe",
  "city": "Delhi",
  "age": 30,
  "gender": "male",
  "height": 1.75,
  "weight": 70
}
```


### Automatic Calculations (Pydantic `computed_field`)

When a patient is created or viewed, two computed fields are automatically calculated:

- **BMI:** `weight / (height^2)` (rounded to 2 decimals)
- **Verdict:** Health category based on BMI
  - `< 18.5` → Underweight
  - `18.5 - 24.9` → Normal
  - `25 - 29.9` → Overweight
  - `≥ 30` → Obese

---

## 📂 Data Storage

Patients are stored in a **local JSON file** (`patients.json`) as a dictionary, where the key is the patient’s ID.

**Example JSON:**
```json
{
  "P001": {
    "name": "Alice",
    "city": "Mumbai",
    "age": 25,
    "gender": "female",
    "height": 1.65,
    "weight": 55,
    "bmi": 20.2,
    "verdict": "Normal"
  }
}
