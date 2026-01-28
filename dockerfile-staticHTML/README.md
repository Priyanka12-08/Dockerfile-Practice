# DOCKERFILE FOR STATIC HTML I(Nginx)

1. First understand the structure of the project
   static-site/
     - index.html
     - Dockerfile

# SKELETON DOCKERFILE STUCTURE

     - FROM nginx: alpine
     - COPY index.html /usr/share/nginx/html/index.html
     - EXPOSE 80

