# MERN Stack Invoicing Application

Built with the MERN stack (MongoDB, Express, React and NodeJS).
![Invoice](https://res.cloudinary.com/almpo/image/upload/v1637311386/invoice/invoice-app_tcz0dj.png)

- [Introduction](#introduction)
- [Key Features](#key-features)
- [Technologies used](#technologies-used)
  - [Client](#client)
  - [Server](#server)
  - [Database](#database)
- [Configuration and Setup](#configuration-and-setup)
- [Troubleshooting](#troubleshooting)
- [Appreciation](#appreciation)
- [Author](#author)
- [License](#license)

## Introduction

This is a side project I've been working on. A full stack invoicing application made using the MERN stack (MongoDB, Express, React & Nodejs), specially designed for freelancers and small businesses, but can be used for almost any type of business need. With this application, you can send beautiful invoices, receipts, estimates, quotes, bills etc to your clients. Jump right off the [Live App](https://sys-invoice.netlify.app/) and start sending invoice or download the entire [Source code](https://github.com/allistermugaisi) and run it on your server. This project is something I've been working on in my free time so I cannot be sure that everything will work out correctly. But I'll appreciate you if can report any issue.

![Invoice Dashboard](https://res.cloudinary.com/almpo/image/upload/v1637314504/invoice/dashboard_c5z0is.png)

## Key Features

- Send invoices, receipts, estimates, quotations and bills via email
- Generate and send/download pdf invoices, receipts, estimates, quotations and bills via email
- Set due date.
- Automatic status change when payment record is added
- Payment history section for each invoice with record about payment date, payment method and extra note.
- Record partial payment of invoice.
- Clean admin dashboard for displaying all invoice statistics including total amount received, total pending, recent payments, total invoice paid, total unpaid and partially paid invoices.
- Multiple user registration.
- Authentication using jsonwebtoken (jwt) and Google auth

## Technologies used

This project was created using the following technologies.

#### Client

- React JS
- Redux (for managing and centralizing application state)
- React-router-dom (To handle routing)
- Axios (for making api calls)
- Material UI & CSS Module (for User Interface)
- React simple Snackbar (To display success/error notifications)
- Cloudinary (to allows users to upload their business logo)
- Apex Charts (to display payment history)
- React-google-login (To enable authentication using Google)

#### Server

- Express
- Mongoose
- JWT (For authentication)
- bcryptjs (for data encryption)
- Nodemailer (for sending invoice via email)
- html-pdf (for generating invoice PDFs)

#### Database

MongoDB (MongoDB Atlas)

## Configuration and Setup

In order to run this project locally, simply fork and clone the repository or download as zip and unzip on your machine.

- Open the project in your prefered code editor.
- Go to terminal -> New terminal (If you are using VS code)
- Split your terminal into two (run the client on one terminal and the server on the other terminal)

In the first terminal

- cd client and create a .env file in the root of your client directory.
- Supply the following credentials

```
REACT_APP_GOOGLE_CLIENT_ID =
REACT_APP_API = http://localhost:5000
REACT_APP_URL = http://localhost:3000

```

To get your Google ClientID for authentication, go to the [credential Page ](https://console.cloud.google.com/apis/credentials) (if you are new, then [create a new project first](https://console.cloud.google.com/projectcreate) and follow the following steps;

- Click Create credentials > OAuth client ID.
- Select the Web application type.
- Name your OAuth client and click Create
- Remember to provide your domain and redirect URL so that Google identifies the origin domain to which it can display the consent screen. In development, that is going to be `http://localhost:3000` and `http://localhost:3000/login`
- Copy the Client ID and assign it to the variable `REACT_APP_GOOGLE_CLIENT_ID` in your .env file

```
$ cd client
$ npm install (to install client-side dependencies)
$ npm start (to start the client)
```

In the second terminal

- cd server and create a .env file in the root of your server directory.
- Supply the following credentials

```
DB_URL = mongodb://mongo:27017/Invoice
PORT = 5000
SECRET = JWT_SECRET_KEY_254
SMTP_HOST = smtp.gmail.com
SMTP_PORT = 587
SMTP_USER = youremail@gmail.com
SMTP_PASS = yourpassword

```

Please follow [This tutorial](https://dev.to/dalalrohit/how-to-connect-to-mongodb-atlas-using-node-js-k9i) to create your mongoDB connection url, which you'll use as your DB_URL

```
$ cd server
$ npm install (to install server-side dependencies)
& npm start (to start the server)

```

## Configuration and Setup for Docker

Pull the respective images from docker hub [Hosted Docker Link](https://hub.docker.com/u/allisterhydra).
Create a docker-compose.yml
Paste in the following configuration YAML code to enable docker compose sync the three containers on the mern-app network

```
version: '3'
services:
  react-app:
    image: react-app
    build: ./client
    stdin_open: true
    ports:
      - '3000:3000'
    networks:
      - mern-app
    volumes:
      - ./client/:/usr/src/app
      - /usr/src/app/node_modules
  api-server:
    image: api-server
    build: ./server
    ports:
      - '5000:5000'
    networks:
      - mern-app
    volumes:
      - ./server/:/usr/src/app
      - /usr/src/app/node_modules
    depends_on:
      - mongo
  mongo:
    image: mongo:4.4-bionic
    ports:
      - '27017:27017'
    networks:
      - mern-app
    volumes:
      - mongo-data:/data/db
networks:
  mern-app:
    driver: bridge
volumes:
  mongo-data:
    driver: local

```

Create a Makefike in the root folder and paste the following code

```
run-dev:
	docker-compose up
```

Run the command

```
make run-dev
```

Your configured docker container should start up

## Troubleshooting

If you're getting error while trying to send or download PDF,
please run the following in your server terminal.

```
$ npm install html-pdf -g
$ npm link html-pdf
$ npm link phantomjs-prebuilt
```

## Contributors

Caroline Makena SCCJ/01437/2019
Roy Uri SCCJ/01447/2019
Emmanuel Sanko SCCJ/01438/2019
Richard Ngatia SCCI/00780/2019
Allister Mugaisi SCCJ/01451/2019
John Wanjema SCCJ/01109/2019
