{% if values.language == "python" %}
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 8080
CMD ["python", "main.py"]
{% elif values.language == "nodejs" %}
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 8080
CMD ["node", "index.js"]
{% elif values.language == "golang" %}
FROM golang:1.21-alpine AS builder
WORKDIR /app
COPY . .
RUN go build -o main .
FROM alpine:latest
COPY --from=builder /app/main .
EXPOSE 8080
CMD ["./main"]
{% endif %}
