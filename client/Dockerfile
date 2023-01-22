# Get the base node image
FROM node:16-alpine 

# Author: Reagan Charana
LABEL maintainer="Reagan Charana <reagan.charana@student.moringaschool.com>"

# Set the working directory to /frontend
WORKDIR /frontend

# Copy all files to the working directory
COPY ./ /frontend

# Install dependencies
RUN npm install
