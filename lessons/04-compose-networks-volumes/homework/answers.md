1. ל־backend אין `ports`, אבל `stats` מגיע אליו באמצעות שם השירות `backend` ברשת הפנימית של Docker. הדפדפן לא ניגש ישירות ל־backend אלא פונה ל־frontend, ו־Nginx מעביר את הבקשה ל־backend.

2. המוצרים נשארים אחרי `docker compose down` ואז `up`, כי הנתונים נשמרים ב־named volume בשם `postgres-data`. אם עושים `docker compose down -v`, ה־volume נמחק ולכן גם נתוני המוצרים נמחקים.

3. זה bind mount, כי בצד שמאל של `:` מופיע נתיב לקובץ במחשב (`../sql/init.sql`). אם משנים את `init.sql` אחרי שהמסד כבר נוצר, השינוי לא ירוץ אוטומטית על המסד הקיים.

4. הרשת ש־Compose יצר היא `docker_default`, וה־volume הוא `docker_postgres-data`. השמות נוצרו לפי שם הפרויקט של Compose (`docker`) בתוספת `_default` לרשת ו־`_postgres-data` ל־volume.

5. ב־image הסופי יש Nginx, הקבצים שנבנו בתיקיית `dist` ו־`nginx.conf`, אבל אין בו Node והקבצים של שלב הבנייה. אין `CMD` כי ל־Nginx כבר יש `CMD` ב־image הבסיסי שלו. ל־stats לא צריך multi-stage כי אין לו שלב build נפרד והוא מריץ ישירות את `server.js`.

6. `multi` כמעט באותו גודל כמו `single` כי בשניהם ה־image הסופי מבוסס על Nginx ומכיל את קבצי ה־build. שלב ה־build של ה־multi-stage לא נכנס ל־image הסופי.

7. `/api/stats` מתאים גם ל־`/api/` וגם ל־`/api/stats`, אבל Nginx בוחר את ה־location הספציפי יותר ולכן הבקשה מגיעה ל־stats. בבקשה `/api/products`, ה־`/` בסוף `proxy_pass` גורם ל־Nginx להחליף את `/api/` ב־`/`, ולכן הבקשה מגיעה ל־backend כ־`/products`.

