FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json .
RUN npm install
COPY . .
#BASE URL passed as build argument to the frontend application

ARG NEXT_PUBLIC_API_BASE_URL
ENV NEXT_PUBLIC_API_BASE_URL=${NEXT_PUBLIC_API_BASE_URL}
RUN npm run build

# docker build -t I27-uiimage:v1 --build-arg NEXT_PUBLIC_API_BASE_URL=http://serverpublicip:8080

#Run the application in a lightweight node image
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app ./
EXPOSE 3000
CMD ["npm", "start"]
