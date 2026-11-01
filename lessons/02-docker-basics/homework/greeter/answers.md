1.
docker build -t greeter:v1 lessons/02-docker-basics/homework/greeter

2.
docker run -d -p 9000:8000 --name greeter greeter:v1

3.
docker run -d -p 9000:8000 --name greeter -e GREETING=Shalom greeter:v1

4.
{"message":"Shalom, Rivka!"}

5.

COPY . .          
EXPOSE 8000            
CMD                   
