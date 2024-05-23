FROM node:alpine

# We don't need the standalone Chromium
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD true

# Install necessary dependencies
RUN apk update && \
    apk add --no-cache \
    chromium \
    nss \
    freetype \
    harfbuzz \
    ttf-freefont

# Set the environment variable for Chromium
ENV CHROME_BIN=/usr/bin/chromium-browser

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

# Ensure .env file is copied correctly
COPY src/.env ./

RUN node src/deploy-commands.js
CMD ["node", "./src/index.js"]
