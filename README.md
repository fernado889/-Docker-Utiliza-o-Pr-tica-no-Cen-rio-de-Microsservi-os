# -Docker-Utiliza-o-Pr-tica-no-Cen-rio-de-Microsservi-os
my-microservice/
├── app/
│   ├── app.py
│   └── requirements.txt
├── Dockerfile
└── docker-compose.yml
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/api')
def home():
    return jsonify(message="Hello from Python Microservice!")

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
Flask==2.3.3
# Utiliza a imagem base oficial do Python
FROM python:3.9-slim

# Define o diretório de trabalho
WORKDIR /app

# Copia o arquivo de dependências para o container
COPY app/requirements.txt .

# Instala as dependências
RUN pip install -r requirements.txt

COPY app/ .

# Expõe a porta 5000 para o serviço
EXPOSE 5000

# Define o comando para iniciar a aplicação
CMD ["python", "app.py"]
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - ./app:/app

      docker-compose build
      docker-compose up
      http://localhost:5000/api
