# Payment Processor

## Description

The `payment-processor` is a robust and scalable backend service designed to handle various payment processing tasks. It acts as a central hub for managing transactions, interacting with different payment gateways, and providing a unified API for applications to initiate and track payments. This service simplifies the integration of payment functionality into applications, abstracting away the complexities of individual payment providers and offering features like transaction management, reporting, and fraud detection.  The goal is to provide a secure, reliable, and efficient payment processing solution adaptable to various business needs.

## Features

*   **Unified Payment API:** Provides a consistent API for initiating and managing payments across multiple payment gateways.
*   **Multiple Payment Gateway Support:** Currently supports Stripe, PayPal, and Authorize.net.  Easily extensible to support other gateways.
*   **Transaction Management:** Tracks the status of all transactions, including pending, successful, and failed payments.
*   **Payment Method Management:** Allows users to securely store and manage multiple payment methods.
*   **Recurring Payments:** Supports the creation and management of recurring payment subscriptions.
*   **Fraud Detection:**  Implements basic fraud detection rules and integrates with third-party fraud detection services (optional).
*   **Reporting & Analytics:** Generates reports on payment activity, providing insights into transaction trends and revenue.
*   **Webhooks:**  Provides real-time updates on payment events through webhooks.
*   **Secure Data Storage:** Uses encryption and tokenization to protect sensitive payment data.
*   **Scalable Architecture:** Designed to handle a high volume of transactions.
*   **Configurable:** Easily customizable to meet specific business requirements through configuration files.
*   **Error Handling and Logging:** Comprehensive error handling and logging for debugging and monitoring.
*   **API Rate Limiting:** Implements rate limiting to prevent abuse.

## Technologies Used

*   **Programming Language:** Python 3.9+
*   **Framework:** Django (4.0+)
*   **Database:** PostgreSQL
*   **Message Queue:** RabbitMQ (for asynchronous tasks)
*   **Cache:** Redis
*   **Web Server:** Gunicorn
*   **API Documentation:** drf-spectacular (Swagger/OpenAPI)
*   **Testing:** pytest, coverage.py
*   **ORM:** Django ORM

## Installation

These instructions will guide you through the process of setting up and running the `payment-processor` service.

### Prerequisites

*   Python 3.9+
*   pip
*   PostgreSQL
*   RabbitMQ
*   Redis
*   Git

### Steps

1.  **Clone the repository:**

    ```bash
    git clone <repository_url>
    cd payment-processor
    ```

2.  **Create and activate a virtual environment:**

    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Install dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

4.  **Configure the database:**

    *   Create a PostgreSQL database.
    *   Update the `DATABASE` settings in `payment_processor/settings.py` with your database credentials.  Example:

        ```python
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.postgresql',
                'NAME': 'payment_processor_db',
                'USER': 'your_username',
                'PASSWORD': 'your_password',
                'HOST': 'localhost',
                'PORT': '5432',
            }
        }
        ```

5.  **Configure RabbitMQ:**

    *   Ensure RabbitMQ is running.
    *   Update the `CELERY_BROKER_URL` and `CELERY_RESULT_BACKEND` settings in `payment_processor/settings.py` with your RabbitMQ connection details.  Example:

        ```python
        CELERY_BROKER_URL = 'amqp://user:password@localhost:5672/'
        CELERY_RESULT_BACKEND = 'redis://localhost:6379/0'
        ```

6.  **Configure Redis:**

    *   Ensure Redis is running.
    *   Update the `CACHES` setting in `payment_processor/settings.py` with your Redis connection details. Example:

        ```python
        CACHES = {
            'default': {
                'BACKEND': 'django_redis.cache.RedisCache',
                'LOCATION': 'redis://127.0.0.1:6379/1',
                'OPTIONS': {
                    'CLIENT_CLASS': 'django_redis.client.DefaultClient',
                }
            }
        }
        ```

7.  **Configure Payment Gateway Credentials:**

    *   Add your API keys and secrets for each payment gateway (Stripe, PayPal, Authorize.net) to the environment variables or appropriate configuration settings.  Refer to the documentation for each payment gateway for details on obtaining these credentials.  Sensitive information should never be committed to the repository.

8.  **Run migrations:**

    ```bash
    python manage.py makemigrations
    python manage.py migrate
    ```

9.  **Create a superuser (optional):**

    ```bash
    python manage.py createsuperuser
    ```

10. **Start the Celery worker:**

    Open a new terminal window and run:

    ```bash
    celery -A payment_processor worker -l info
    ```

11. **Start the Django development server:**

    ```bash
    python manage.py runserver
    ```

    The service will be accessible at `http://localhost:8000`.

12. **Access the API documentation:**

    Navigate to `http://localhost:8000/api/schema/swagger-ui/` to access the Swagger UI documentation.

## Usage

Refer to the API documentation for details on how to use the `payment-processor` service. The Swagger UI provides interactive documentation and allows you to test the API endpoints directly.

## Contributing

Please read `CONTRIBUTING.md` for details on our code of conduct, and the process for submitting pull requests to us.

## License

This project is licensed under the MIT License - see the `LICENSE` file for details.