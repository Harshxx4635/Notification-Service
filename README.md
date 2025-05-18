
# Notification Service

A backend notification API service built using FastAPI that allows sending notifications via Email, SMS, and In-App methods through PostgreSQL database.

---

## Features

- Send Notifications via:
    - E-Mail
    - SMS
    - In-App
- Retrieve notifications using user ID
- Swagger UI for docs and testing


## Tech Stack

**FastAPI:** Web Framework

**PostgreSQL:** Storing notification data

**SQLAlchemy:** ORM for database management

**Pydantic:** Used for data validation

**Twilio:** Service for sending SMS

**Google SMTP:** Service for sending E-Mails


## Prerequisites

- **Python** installed on the system
- **PostgreSQL** set up on the system
- **Git** for version control
## Setup

### 1️. Clone the Project

```bash
git clone https://github.com/Harshxx4635/Notification-Service
cd Notification-Service
```

### 2️.Create a Virtual Environment

```bash
python -m venv venv

venv\Scripts\activate
```

### 3️.Install Dependencies

```bash
pip install -r requirements.txt
```
## Database Setup

Start PostgreSQL service and create a database named `notificationdb`

```sql
psql -U postgres

postgres#= CREATE DATABASE notificationdb;
```
## Environment Variables

To run this project, you will need to add the following environment variables to your `.env` file

```env
DATABASE_URL=postgresql+asyncpg://<username>:<password>@localhost:5432/notificationdb
```

#### Google SMTP Variables (Get from myaccount.google.com/security)

```env
EMAIL_FROM=<your-email>@gmail.com
EMAIL_USERNAME=<your-email>@gmail.com
EMAIL_PASSWORD=16 digit Google App Password
EMAIL_HOST=smtp.gmail.com  
EMAIL_PORT=587
```


#### Twilio Variables (Get from console.twilio.com)

```env
TWILIO_ACCOUNT_SID : From Twilio Dashboard
TWILIO_AUTH_TOKEN : From Twilio Dashboard
TWILIO_PHONE_NUMBER : +123456789
```

## Run Locally

Open command prompt in the project directory and run the following command to start the API

```bash
 uvicorn app.main:app --reload
```
## Run the API

### Send Notification

**POST /notifications**

**Body Example:**
```json
{
  "user_id": 1,
  "type": "email",
  "email": "<receiver email>",
  "message": "Notification"
}
```

```json
{
  "user_id": 2,
  "type": "sms",
  "phone": "<receiver phone number>",
  "message": "Notification"
}
```

### Fetch Notification

**GET /users/{user_id}/notifications**

Replace `{user_id}` with the target user ID to get their notifications.


**Response Example:**
```json
[
    {
        "user_id": 123,
        "type": "email",
        "message": "Hello",
        "id": 1,
        "status": "failed",
        "created_at": "2025-05-18T13:41:55.718954"
    },
    {
        "user_id": 123,
        "type": "email",
        "message": "Hello again!",
        "id": 2,
        "status": "sent",
        "created_at": "2025-05-18T13:43:33.649254"
    }
]
```
## Documentation

After running locally, you can access the [Swagger Docs](https://127.0.0.1/8000) for the FastAPI documentation


## Troubleshooting

| Issue                            | Solution                                                  |
|----------------------------------|-----------------------------------------------------------|
| `DATABASE_URL`  / Connection error             | Check .env file & restart PostgreSQL service                     |
| Notifications not sending        | Verify email/SMS config in `.env` and if the receiver email/phone number is valid                        |
| Missing permissions        | Give yourself privileges from psql shell                        |
