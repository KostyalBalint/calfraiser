FROM node:18-alpine AS builder
ENV JQ_VERSION=1.6
RUN wget --no-check-certificate https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 -O /tmp/jq-linux64
RUN cp /tmp/jq-linux64 /usr/bin/jq
RUN chmod +x /usr/bin/jq

ENV GENERATE_SOURCEMAP=false

WORKDIR /app
COPY package.json ./
COPY yarn.lock ./
RUN yarn install --frozen-lockfile
COPY . .

#In the public/config.json file substitue the environment variables with {key: $key, key2: $key2}
#When the docker image is started the start-nginx.sh script will substitute the environment variables with the values
#Guide: https://developers.redhat.com/blog/2021/03/04/making-environment-variables-accessible-in-front-end-containers#inject_the_environment_variables
RUN jq 'to_entries | map_values({ (.key) : ("$" + .key) }) | reduce .[] as $item ({}; . + $item)' ./public/config.json > ./public/config.tmp.json && mv ./public/config.tmp.json ./public/config.json

RUN yarn build

FROM nginx:1.19-alpine AS server

ENV CONF_FILE=/usr/share/nginx/html/config.json
COPY ./start-nginx.sh /usr/bin/start-nginx.sh
RUN chmod +x /usr/bin/start-nginx.sh
COPY ./etc/nginx.conf /etc/nginx/conf.d/default.conf

WORKDIR /usr/share/nginx/html

COPY --from=builder ./app/build /usr/share/nginx/html

ENTRYPOINT [ "start-nginx.sh" ]