FROM node:16-alpine

# Install app dependencies
COPY package.json ./

RUN npm install

# Bundle app source
COPY . .

ENV EXCEL_PATH /data/data.xlsx
ENV PORT 80

EXPOSE 80
CMD [ "npm", "run", "start"]