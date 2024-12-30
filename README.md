# projeto-final-laravel
Criação de uma API que oferece a integração de dados e serviços a partir de uma aplicação Laravel

Tema escolhido: "Sistema de Gestão de Consultas Médicas


CONFIGURACAO DO FICHEIRO .ENV COM OS DETALHES DO BANCO DE DADOS (MARIADB)

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=medical_appointments
DB_USERNAME=teu_usuario
DB_PASSWORD=teu_password

(Instalacao do pacote de autenticacao JWT
composer require tymon/jwt-auth


Estrutura de Class
  Classes Principais:
    User: Pacientes, médicos e administradores
    Doctor: Detalhes dos médicos (id, nome, especialidade, etc.)
    Patient: Dados dos pacientes (id, nome, etc.)
    Appointment: Informações sobre as consultas
    Speciality: Especialidades médicas (Cardiologia, Pediatria, etc.)
    Prescription: Receita médica associada às consultas.
    Room: Salas onde as consultas ocorrem.
    Schedule: Horários disponíveis para os médicos.

  Relações Planeadas:
    (1:1):
      Appointment <-> Patient (cada consulta está associada a um paciente).
      Room <-> Appointment (cada consulta ocorre numa sala específica).
    (1:N):
      Doctor <-> Appointment (um médico pode ter várias consultas).
      Patient <-> Appointment (um paciente pode ter várias consultas).
      Doctor <-> Schedule (um médico pode ter vários horários disponíveis).
    (N:N):
      Doctor <-> Speciality (um médico pode ter várias especialidades, e uma especialidades pode                                 ter vários mádicos).
      Room <-> Schedule (Uma sala pode estar disponível em múltiplos horários, e um horário pode                             estar associado a várias salas).
    Outras relações relevantes:
      Patient <-> Prescription (Um paciente pode ter várias receitas médicas).
      Appointment <-> Schedule (Cada consulta deve respeitar um horário disponível).

  Routes:
    Rotas agrupadas em api.php:
      Autenticação:
        POST "/auth/login"
        POST "/auth/register"
      Consultas:
        GET "/appointments"
        POST "/appointments"
        GET "/appointments/{id}"
      Médicos:
        GET "/doctors"
        POST "/doctors"
        GET "/doctors/{id}"
        GET "/doctors/{id}/appointments"
      Pacientes:
        GET "/patients"
        POST "/patients"
        GET "/patients/{id}"
        GET "/patients/{id}/appointments"
      Receitas Médicas:
        GET "/prescriptions"
        POST "/prescriptions"
        GET "/prescriptions/{id}"
      Salas e Horários:
        GET "/rooms"
        POST "/rooms"
        GET "/schedules"
        POST "/schedules"
O que fazer aseguir:
  Configuração das Migrations para as tabelas principais e suas relações.
  Criar os Models e definir as relações nas classes.
  Implementar os Controllers com métodos CRUD e lógica de validação.
  Definir mensagens de validação personalizadas e garantindo consistência nos dados.


MIGRATIONS:
  Planeamento de Tabelas:
    USERS
      id (PK)
      name (string)
      email (string, unique)
      password (string)
      role (enum: admin, doctor, patient);
    Doctors
      id (PK)
      user_id (FK p/ users)
      phone_number (string)
      specialization_summary (text)
    Patients
      id (PK)
      user_id (FK p/ users)
      birth_date (date)
      gender (enum: male, female, other)
    Appointments
      id (PK)
      doctor_id (FK p/ doctors)
      patient_id (FK p/ patients)
      room_id (FK p/ rooms)
      schedule_id (FK p/ schedules)
      date_time (datetime)
      status (enum: scheduled, completed, cancelled)
    Specialties
      id (PK)
      name (string, unique)
    Doctors_Specialty (tabela pivot M:M)
      doctor_id (FK p/ doctors)
      specialty_id (FK p/ specialties)
    Rooms
      id (PK)
      name (string, unique)
      floor (integer)
      capacity (integer)
    Schedules
      id (PK)
      doctor_id (FK p/ doctors)
      room_id (FK p/ rooms)
      day_of_week (enum: Monday,..., Sunday)
      start_time (time)
      end_time (time)
    Prescriptions
      id (PK)
      appointment_id (FK p/ appointments)
      description (text)


Models
  Terminal:
    php artisan make:model Doctor
    php artisan make:model Patient
    php artisan make:model Appointment
    php artisan make:model Specialty
    php artisan make:model Room
    php artisan make:model Schedule
    php artisan make:model Prescription

    
Controllers
  Terminal:
    php artisan make:controller DoctorController
    php artisan make:controller PatientController
    php artisan make:controller AppointmentController
    php artisan make:controller SpecialtyController
    php artisan make:controller RoomController
    php artisan make:controller ScheduleController
    php artisan make:controller PrescriptionController

ROUTES
  AuthController
    Route::post('login', [AuthController::class, 'login']);
    Route::post('register', [AuthController::class, 'register']);
    
  AppointmentController;
    Route::middleware('auth:api')->group(function () {
        Route::get('appointments', [AppointmentController::class, 'index']);
        Route::post('appointments', [AppointmentController::class, 'store']);
        Route::get('appointments/{id}', [AppointmentController::class, 'show']);
        Route::put('appointments/{id}', [AppointmentController::class, 'update']);
        Route::delete('appointments/{id}', [AppointmentController::class, 'destroy']);
    });

  DoctorController
    Route::get('doctors', [DoctorController::class, 'index']);
    Route::get('doctors/{id}', [DoctorController::class, 'show']);
    Route::get('doctors/{id}/appointments', [DoctorController::class, 'appointments']);
  
  PatientController
    Route::get('patients', [PatientController::class, 'index']);
    Route::get('patients/{id}', [PatientController::class, 'show']);
    Route::get('patients/{id}/appointments', [PatientController::class, 'appointments']);

  


      
