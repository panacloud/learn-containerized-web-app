In this step we want to run a Node.js Express Web App in a container locally.


First lets create a Node.js and Express Hello World App:

http://expressjs.com/en/starter/hello-world.html

Once I have run the app.js successfully, then I moved to reading chapter 1-8 of this book:

https://www.amazon.com/Docker-Deep-Dive-Nigel-Poulton/dp/1521822808/ref=sr_1_1

Create a Dockerfile as demonstrated in Chapter 8.

Assuming you have already installed Docker on your local computer, give the following command as suggested in chapter 8 of the book:

docker image build -t web-express:latest .

To check if the image has been created:

docker image ls


To run it:

docker container run -d --name c1 -p 80:3000 web-express:latest


To check if the container is running:

docker container ls
