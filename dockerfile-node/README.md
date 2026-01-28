# DOCKERFILE FOR NODE.js

1. First understand the structure of the project
     - FROM base-image
     - WORKDIR /app
     - COPY file (packages)
     - RUN install the lib
     - EXPOSE ports
     - CMD run app

#################################################################################################################################

# DOCKERFILE

FROM node:18-alpine
WORKDIR /app
COPY packages*.json ./
RUN npm install
COPY ..  # COPY the app code
EXPOSE 3000   # the port exposed in the app
CMD ["node","service.js"]