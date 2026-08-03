
# Run the application in a Python 3.14 slim image   
FROM python:3.14-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8083
CMD ["python", "-m","uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8083"]