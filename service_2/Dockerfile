FROM python:3.10-slim
WORKDIR /app
COPY . .
RUN apt update && \
    apt install -y curl && \
    pip install flask && \
    apt clean
CMD ["python", "app.py"]

