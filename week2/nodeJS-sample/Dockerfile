# This is your base image, the starting point.
# In this case, it’s the official Red Hat NodeJS image
FROM ubi8/nodejs-12
# Add application sources 
ADD app.js .
ADD package.json .
# Installs all of the required dependencies inside your image.
RUN npm install
# This is what runs when the image is started
CMD npm run -d start