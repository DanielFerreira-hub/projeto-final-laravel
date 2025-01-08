# API Testing with Insomnia
FALTA OS DELETES, OS GETS DE ALL USERS/DOCTORS/PATIENTS, O GET APPOINTMENT ESPECIFICO POR ID, GET TODOS OS SCHEDULES DO DOCTOR, GET TDS OS APPOINTMENTS DO PATIENT, E TESTAR EM CENARIOS DE ERROR 

This README provides detailed information about the endpoints available in your Laravel API for the "Sistema de Gestão de Consultas Médicas" project. You can use these endpoints to test your API using Insomnia or any other API testing tool.

## Authentication

### Register User
**Endpoint:** `POST /api/auth/register`  
**URL:** `http://127.0.0.1:8000/api/auth/register`  
**Headers:** `none`  
**Content-Type:** `application/json`  
**Request Body:**  
```
{
    "name": "John Doe",
    "email": "johndoe@example.com",
    "password": "securepassword",
    "role": "doctor",
    "phone_number": "1234567890",
    "specialization_summary": "Cardiology Specialist",
    "specialties": [1, 2]
}
```

### Login User

**Endpoint:** `POST /api/auth/login`  
**URL:** `http://127.0.0.1:8000/api/auth/login`  
**Headers:**
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "email": "johndoe@example.com",
    "password": "securepassword"
}
```

## Users
### Create User

**Endpoint:** `POST /api/users`  
**URL:** `http://127.0.0.1:8000/api/users`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "name": "Jane Smith",
    "email": "janesmith@example.com",
    "password": "anotherpassword",
    "role": "patient",
    "birth_date": "1990-01-01",
    "gender": "female"
}
```

### Update User

**Endpoint:** `PUT /api/users/{id}`  
**URL:** `http://127.0.0.1:8000/api/users/1 // Replace 1 with the actual user ID`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "name": "Jane Doe",
    "email": "janedoe@example.com"
}
```

## Patients
### Create Patient

**Endpoint:** `POST /api/patients`  
**URL:** `http://127.0.0.1:8000/api/patients`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  

**Request Body:**
```
{
    "user_id": 2,
    "birth_date": "1990-01-01",
    "gender": "female"
}
```

### Update Patient

**Endpoint:** `PUT /api/patients/{id}`  
**URL:** `http://127.0.0.1:8000/api/patients/1 // Replace 1 with the actual patient ID`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  

**Request Body:**
```
{
    "birth_date": "1991-01-01"
}
```

## Doctors
### Create Doctor

**Endpoint:** `POST /api/doctors`  
**URL:** `http://127.0.0.1:8000/api/doctors`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "user_id": 3,
    "phone_number": "0987654321",
    "specialization_summary": "Dermatology Specialist",
    "specialties": [3, 4]
}
```

### Update Doctor

**Endpoint:** `PUT /api/doctors/{id}`  
**URL:** `http://127.0.0.1:8000/api/doctors/1 // Replace 1 with the actual doctor ID`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "phone_number": "1122334455"
}
```

## Rooms
### Create Room

**Endpoint:** `POST /api/rooms`  
**URL:** `http://127.0.0.1:8000/api/rooms`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "name": "Room 101",
    "floor": 1,
    "capacity": 2
}
```

### Update Room

**Endpoint:** `PUT /api/rooms/{id}`  
**URL:** `http://127.0.0.1:8000/api/rooms/1 // Replace 1 with the actual room ID`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "capacity": 4
}
```

## Schedules
### Create Schedule

**Endpoint:** `POST /api/schedules`  
**URL:** `http://127.0.0.1:8000/api/schedules`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "doctor_id": 1,
    "room_id": 1,
    "day_of_week": "Monday",
    "start_time": "09:00",
    "end_time": "17:00"
}
```

### Update Schedule

**Endpoint:** `PUT /api/schedules/{id}`  
**URL:** `http://127.0.0.1:8000/api/schedules/1 // Replace 1 with the actual schedule ID`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "day_of_week": "Tuesday"
}
```

## Appointments
### Create Appointment

**Endpoint:** `POST /api/appointments`  
**URL:** `http://127.0.0.1:8000/api/appointments`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "doctor_id": 1,
    "patient_id": 1,
    "room_id": 1,
    "schedule_id": 1,
    "date_time": "2025-01-10 09:30:00",
    "status": "scheduled"
}
```

### Update Appointment

**Endpoint:** `PUT /api/appointments/{id}`  
**URL:** `http://127.0.0.1:8000/api/appointments/1 // Replace 1 with the actual appointment ID`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "status": "completed"
}
```

## Prescriptions
### Create Prescription

**Endpoint:** `POST /api/prescriptions`  
**URL:** `http://127.0.0.1:8000/api/prescriptions`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "appointment_id": 1,
    "description": "Take one pill daily"
}
```

### Update Prescription

**Endpoint:** `PUT /api/prescriptions/{id}`  
**URL:** `http://127.0.0.1:8000/api/prescriptions/1 // Replace 1 with the actual prescription ID`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "description": "Take two pills daily"
}
```
## Specialties
### Create Specialty

**Endpoint:** `POST /api/specialties`  
**URL:** `http://127.0.0.1:8000/api/specialties`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "name": "Neurology"
}
```

### Update Specialty

**Endpoint:** `PUT /api/specialties/{id}`  
**URL:** `http://127.0.0.1:8000/api/specialties/1 // Replace 1 with the actual specialty ID`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  
**Content-Type:** `application/json`  
**Request Body:**
```
{
    "name": "Neurosurgery"
}
```

## Custom Method: Get Appointments by Status

**Endpoint:** `GET /api/appointments/status/{status}`  
**URL:** `http://127.0.0.1:8000/api/appointments/status/scheduled // Replace scheduled with the desired status`  
**Headers:**
**Content-Type:** `Bearer <your_jwt_token>`  


Roles and Access Control

    Admin: Has access to all endpoints.
    Doctor: Has access to endpoints related to patients, doctors, rooms, schedules, appointments, prescriptions, and specialties.
    Patient: Can access their own user information and appointments.

Make sure to replace <your_jwt_token> with the actual JWT token obtained after logging in.

Testing with Insomnia
    1. Open Insomnia.
    2. Create a new request.
    3. Set the method (e.g., POST, PUT, GET) and the URL as described above.
    4. Add the headers as described above.
    5. Add the request body (if applicable) as described above.
    6. Send the request and verify the response.

Feel free to customize and expand this README as needed for your specific testing requirements.
