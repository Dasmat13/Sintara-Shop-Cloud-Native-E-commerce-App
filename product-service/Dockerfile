
# Dockerfile for Python Flask Product Service
FROM python:3.10-slim
WORKDIR /app
COPY . .
RUN pip install flask pymongo
CMD ["python", "app.py"]