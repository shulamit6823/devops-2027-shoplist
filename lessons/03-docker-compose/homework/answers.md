1. יהיו 2 Containers ו־1 Image, כי יש שני services שמשתמשים באותו Dockerfile.

2. `http://localhost:9001/hello/Rivka` יחזיר:
   {"message": "Shalom, Rivka!"}

  `http://localhost:9002/hello/Rivka` יחזיר:
   {"message": "Hello, Rivka!"}

3. שני ה־services לא יכולים להשתמש באותו פורט במחשב, כי Docker צריך לדעת לאיזה container להעביר את הבקשה. לעומת זאת, הם יכולים להשתמש באותו פורט בתוך ה־container, כי לכל container יש סביבת רשת נפרדת.

4. greeter-fr:
  build:
    context: ../../02-docker-basics/homework/greeter
  environment:
    GREETING: Bonjour
  ports:
    - "9003:8000"

5. ב־Greeter אין מידע קבוע שצריך לשמור, ולכן אין צורך ב־volume. ב־Postgres יש נתונים שצריך לשמור גם אם ה־container נמחק, ולכן משתמשים ב־volume.