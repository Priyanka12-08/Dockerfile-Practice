# DOCKERFILE FOR PYTHON

1. First understand the structure of the project
     - FROM base-image
     - WORKDIR /app
     - COPY file ( requirements)
     - RUN install the lib
     - EXPOSE ports
     - CMD run app

#################################################################################################################################

# DOCKERFILE

FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt
RUN pip install --no-cache-dir -r requirements.txt  # to ensure the latest version is installed and not from the cache memory
COPY ..  # COPY the app code
EXPOSE 5000   # the port exposed in the app
CMD ["python","app.py"]