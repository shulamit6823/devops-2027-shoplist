# משתמשים ב-Python 3.11 כבסיס ל-image
FROM python:3.11-slim
# קובע את תיקיית העבודה בתוך ה-Container
WORKDIR /app
# מעתיק את קובץ התלויות לתיקיית העבודה
COPY requirements.txt .
# מתקין את ספריות ה-Python שהשירות צריך
RUN pip install -r requirements.txt
# מעתיק את כל קבצי השירות לתיקיית העבודה
COPY . .
# מציין שהשירות משתמש בפורט 8000 בתוך ה-Container
EXPOSE 8000
# מגדיר את הפקודה שתופעל כאשר ה-Container מתחיל
CMD ["python", "app.py"]