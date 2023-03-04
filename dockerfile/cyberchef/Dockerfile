#
# BUILD STAGE
#

# Get basic(slim) nginx server image
FROM nginx:1.23.3-alpine-slim as build

# Install git to get cyberchef & tools to build cyberchef
RUN apk update
RUN apk --update add git nodejs npm

# Clone and build cyberchef
RUN git clone https://github.com/gchq/CyberChef.git /tmp/cyberchef
WORKDIR /tmp/cyberchef
RUN npm install
RUN npm run build

# Remove default nginx index.html
RUN rm -f /usr/share/nginx/html/index.html

# Unzip compiled cyberchef zip package
RUN find /tmp/cyberchef/build/prod/ -type f -name "*.zip" | xargs -n1 unzip -d /usr/share/nginx/html/
WORKDIR /usr/share/nginx/html

# Move CyberChef html file to index.html
# https://stackoverflow.com/questions/72253410/how-to-properly-use-xargs-with-cp
RUN find . -type f -name "*.html" | xargs -I {FileName} mv {FileName} ./index.html

#
# MAIN STAGE
#

# use same nginx alpine slim image as build stage uses
FROM nginx:1.23.3-alpine-slim as main

# Copy build cyberchef files to main for nginx to serve
COPY --from=build /usr/share/nginx/html /usr/share/nginx/html

# Start nginx
CMD ["nginx", "-g", "daemon off;"]