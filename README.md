# Telegram notifications API

A simple API to send notifications/messages to your phone through a Telegram bot.

## Why?

I was looking for a way to programmatically send notifications to my phone, and after considering multiple options, I ended up using Telegram bots for that, and these are the main reasons for using Telegram:

1- You don't have to build your own app just for the notifications feature!

2- It is super easy to create and manage Telegram bots

3- There's a good Node.js package that makes the interaction with the bots very simple

4- it is Free!



For the apps I built, I was sending the notifications directly from each app, and later I though to build this API so it can be used as a single 'send notifications API' for my different apps.

## How it works

The app acts as a web server that receives requests to send notifications through the API endpoint `/send-notification`
you can think of it as an independent "microservice".

so you basically keep it running, then connect to it from your main app through API requests.

## Usage

**Note**: Before you proceed, make sure that `node` and `npm` are installed on your machine.

1- Clone (or download) this repository: `git clone https://github.com/nassirGH/Notification_Bot`

2- go to the project path and run `npm install`

3- Rename the file **env.sample** to **.env**

4- Set these variables in your **.env** file:

- **TELEGRAM_BOT_TOKEN**: This is your bot access token [[check this section for more details on how to create a new Telegram bot and get its token](#steps-to-create-a-bot-using-the-telegram-app)].

- **API_SECRET_TOKEN**: This is a secret token that you will have to use with each API request.

To generate this token, go to the app path, and type: `npm run generate-api-token`, then copy the token to your **.env** file


- **MY_CHAT_ID**: This is your unique chat id on the Telegram app, it is needed so your bot knows to whom it should send the notifications/messages.

Before you get the "chat id", make sure you set the values for **TELEGRAM_BOT_TOKEN** and **API_SECRET_TOKEN**, and that you saved the **.env** file.

Now to get the "chat id", simply run the app using this command: `npm run prod`, and since **MY_CHAT_ID** is not set, the app will provide you with a number, and it will ask you to message your bot, so all you have to do is go to your Telegram app, and message your bot with that number, then check your console, you will get your chat id, copy the id and assign it to **MY_CHAT_ID** in the **.env** file then save the file.





- **PORT** (optional): This is the app port, default value is 3007, but you can change it to another value if you want.

5- After you successfully set all these values, you are now ready to start the app, simply type: `npm run prod`, and you will see a screen similar to this one:


**Note**: for security reasons, always make sure to use https, especially in production.

## Send notifications (through the API)

After you successfully started the app, and in order to send notifications, you will have to communicate with it through API requests:

API endpoint: `/send-notification` (A full path might be something like that: http://localhost:3007/send-notification)

Method: `POST`

Parameters (form urlencoded or JSON format, both are acceptable):

- `token` (this is the API token you specified in the .env file)

- `message` (the notification message)

These are two examples using curl:

- sending a message (JSON)

```console
curl -i -d '{"token":"wyrhoYv.lNPjwoOEgYfFSMbusd8wZgIPUzVgNY.c7bAXMK-evkoXIXyZxPDRdDtW2C4qDVkkjTKf6mkFOwK1j.Z1Le9S8jK4Up7mtYU7U","message":"Hello, this is a test message"}' -H "Content-Type: application/json" -X POST http://localhost:3007/send-notification
```

- sending a message (form urleconded)
```console
curl -i -d "token=wyrhoYv.lNPjwoOEgYfFSMbusd8wZgIPUzVgNY.c7bAXMK-evkoXIXyZxPDRdDtW2C4qDVkkjTKf6mkFOwK1j.Z1Le9S8jK4Up7mtYU7U&message=Hello, this is a test message" -X POST http://localhost:3007/send-notification
```

and here's a screenshot after sending the request:



**Note**: for security reasons, always make sure to use https, especially in production.

## Steps to create a bot using the Telegram app

1- Open Telegram app, then start a new message and  
search for **BotFather**.




2- Tap **Start** to begin your interaction with **BotFather**,  
after doing so, the bot will send you a list of commands  
you can use, tap on **/newbot**.



4- Now you will have to enter your bot username, this  
username should be unique (you will get an error if  
it wasn't), and it should end with the word **bot**.



5- If everything went well, you should receive a message  
similar to the one below, and it will include your bot  
access token (**This token should be a secret, and it  
shouldn't be shared**), and in case someone was able  
to get your token, you can revoke it and get a new one  
using **botFather**.




6- Congratulation, you have created a bot! now let's  
message the new bot, simply start a new message, and  
search for your bot username.




## License

MIT License

Copyright (c) 2020 Nassir GH

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.