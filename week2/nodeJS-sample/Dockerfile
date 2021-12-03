# This is your base image, the starting point.
# In this case, it’s the official image from the Node.js and has Node.js version 8.x installed. That means we don’t have to install any framework; 
# it’s already included with this base image.
FROM ubi8/nodejs-12
# Add application sources 
ADD app.js .
ADD package.json .
# Installs all of the required dependencies inside your image.
RUN npm install
# This is what runs when the image is started
CMD npm run -d start