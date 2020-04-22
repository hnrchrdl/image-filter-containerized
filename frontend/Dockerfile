## Build
FROM beevelop/ionic AS ionic

ARG CI=false
# Create app directory
WORKDIR /usr/src/app
# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./
RUN npm ci
# Bundle app source
COPY . .
# Build for production in CI, else use a local build setup.
RUN if [ "$CI" = "true" ] ; then ionic build --configuration=production ; else ionic build ; fi

## Run
FROM nginx:alpine
#COPY www /usr/share/nginx/html
COPY --from=ionic /usr/src/app/www /usr/share/nginx/html
