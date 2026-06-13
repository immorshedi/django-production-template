FROM ${APP_BASE_IMAGE}

WORKDIR /app

COPY . .

CMD ["python", "app/manage.py", "runserver", "0.0.0.0:8000"]