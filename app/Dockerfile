# Use an official Python image
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Copy the application files into the container
COPY . /app

# Install the dependencies
RUN pip install Flask pymongo

# Set the Flask app environment variable
ENV FLASK_APP=app.py

# Install dependencies
RUN pip install -r requirements.txt

# Expose port 5000 for Flask
EXPOSE 5000

# Run the Flask app
CMD ["flask", "run", "--host=0.0.0.0"]
#CMD ["python", "app.py"]