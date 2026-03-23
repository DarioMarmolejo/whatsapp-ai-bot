# whatsapp-ai-bot
Arquitectura Técnica — WhatsApp AI Bot (Gestión de Gastos y Tareas)

## 1. Descripción General
Sistema conversacional basado en WhatsApp que permite gestionar gastos y tareas mediante lenguaje natural. Utiliza Gemini con Function Calling para ejecutar operaciones CRUD sobre PostgreSQL.
##2. Arquitectura del Sistema
Flujo desde recepción de mensaje hasta respuesta generada por IA.

Usuario -> WhatsApp -> Webhook -> Validación -> IA (Gemini)
-> Function Calling -> Backend -> PostgreSQL -> Respuesta -> Usuario


## 3. Stack Tecnológico

Backend: Java 21 + Spring Boot 3.4 (Virtual Threads)
IA: Gemini 2.5 Flash/Pro vía LangChain4j
Base de Datos: PostgreSQL (Neon)
Integración: WhatsApp Business Cloud API
Infraestructura: Docker + Railway/Koyeb


## 4. Modelo de Datos
Tablas principales del sistema:

users(id, phone_number, name, created_at)
messages(id, user_id, content, direction, created_at)
expenses(id, user_id, amount, category, description, expense_date, created_at)
tasks(id, user_id, title, completed, due_date, created_at)


## 5. Definición de Agentes (LangChain4j)
Tools principales para interacción con la IA:

createExpense(amount, category, description, date)
getExpenses(startDate, endDate)
createTask(title, dueDate)
completeTask(taskId)


## 6. Seguridad

- Validación X-Hub-Signature-256 (HMAC SHA256)
- Uso de variables de entorno
- Sanitización de inputs
- Rate limiting


## 7. Endpoints

GET /webhook -> validación Meta
POST /webhook -> recepción de mensajes


## 8. Plan de Pruebas

- Mock de modelo IA
- Test unitarios de tools
- Test de integración con payloads reales
- Uso de Testcontainers


## 9. Despliegue

- Docker container
- Deploy en Railway o Koyeb
- Manejo de secrets con variables de entorno


