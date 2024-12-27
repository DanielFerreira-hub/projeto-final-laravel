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
      
      



















