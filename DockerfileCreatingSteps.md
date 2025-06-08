[Writing a Dockerfile | Docker Doc](https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/) - official documentation reference

Creating Dockerfile(docker file is a set of instructions to create docker image for our custom application)

	- FROM image_name:tag
	- docker build -t newdockerimagename /path_to_Dockerfile_directory/ (command to create docker image from Dockerfile)
	- WORKDIR /app (here we give directory to keep source code in a container)
	- COPY . /app (to copy all the content or source code to the directory in container)
	- RUN command (e.g., RUN pip install --no-cache-dir -r requirements.txt) (to perform commands while creating container, like installation of some software etc.) (requirements.txt is a file which contain dependency to run application in container)
	- EXPOSE port_number (use to open the port for connection to external world)(inter-communication between the containers)
	- CMD ["python", "app.py"] (this is to run the application with a command inside the container, after container comes up)

To create an application, 
	- Create a folder e.g., flask-app and under this

○ app.py (source code) - § Content of app.py
   
			from flask import Flask
			
			app = Flask(__name__)
			
			@app.route('/')
			def home():
			    return "Welcome to my Flask App!"
			
			@app.route('/about')
			def about():
			    return "This is a simple web app using Flask."
			
			if __name__ == '__main__':
			    app.run(host="0.0.0.0", port=5000, debug=True)
			
○ requirements.txt 
			- § Content of requirements.txt
   
			Flask
			
○ Dockerfile
			§ Content of created a Docker file -
   
		# this will get the base image from dockerhub
		FROM python:3.9
		
		# Copy the application files
		WORKDIR /app
		
		COPY . /app
		
		#Install Dependencies
		RUN pip install --no-cache-dir -r requirements.txt
		RUN useradd manmohan
		RUN apt update -y
		
		#Expose the port Flask runs on
		EXPOSE 5000
		
		#Define the command to run the application
		CMD ["pythom", "app.py"]
		
		LABEL DESCRIPTION="This is a dockerfile for flask application"
