# Get the base node image
FROM node:16-alpine 

# Author: Reagan Charana
LABEL maintainer="Reagan Charana <reagan.charana@student.moringaschool.com>"

# Set the working directory to /frontend
WORKDIR /backend

# Copy all files to the working directory
COPY ./ /backend

# Install dependencies
RUN npm install