✅ Step 1: Create Flask App (app.py)
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Dockerised Flask!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
✅ Step 2: Create Requirements File (requirements.txt)
flask
✅ Step 3: Create Dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]

docker build -t joyvincia/flask-app .
docker run -d -p 5000:5000 joyvincia/flask-app
docker push joyvincia/flask-app
