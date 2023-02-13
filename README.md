# [JollyTalk](https://chipper-valkyrie-8f33c6.netlify.app/)

#### Sample Username and Password
Username: Photographer

Password: 123123

## ***Modules of the WebApp***

**Index.js**
![image1](https://user-images.githubusercontent.com/87146827/218466303-62b29960-da1e-4429-b991-d51ded3b7168.png)

The program begins with an index file which imports the React library and starts the app.js file. Running this using npm start will run the chat interface.

**App.js**
![image2](https://user-images.githubusercontent.com/87146827/218466313-57d67b8e-2b45-4468-93f0-65d88eeeebfe.png)

App.js imports all the required components for the program to run, mainly ChatFeed.jsx and LoginForm.jsx, as well as App.css for the user interface of the program. Separating the program into separate modules allows for abstraction and are executed as a single program using App.js The sub-program checks if the user is not logged in using a conditional statement and returns LoginForm if not logged in and the chat application if already logged in. This is done by the statement if (!localStorage.getItem(‘username’)) return <LoginForm/>;. Different variables are used to store the input values of the “Username” and “Password”.  It also contains the Project ID, which is used to connect the application to Chat Engine, which is used to create a secure account for the user. This is the main module run to execute the program.


**MessageForm.jsx**
![image3](https://user-images.githubusercontent.com/87146827/218466333-3ec8f6c3-c4f7-450d-b623-c2f0cc04acd3.png)

MessageForm.jsx is responsible for sending and storing messages. When a message longer than 0 characters is sent, it is given a cred and a charId, and is saved in the variable “text”. This is done using the statement if (text.length > 0) {sendMessage(creds, chatId, { text}); This variable is later used by MyMessage.jsx and TheirMessage.jsx. The same is done for image uploads. In addition to this, MessageForm.jsx also provides the user with a way to send messages and upload images. This is done by providing a box to type the text of the message, a file input/output for the images, and a send button to store the text or image in the variable to later be displayed. MessageForm.jsx also has the additional feature to check and display if a user is currently typing a message. This is done by importing the react-chat-engine library and using the isTyping sub-procedure.

**MyMessage.jsx**
![image4](https://user-images.githubusercontent.com/87146827/218466360-ac3c59a5-f372-491e-8d58-01aeac0624fc.png)

MyMessage.jsx retrieves the message sent by the user from MessageForm.jsx and displays it on the chat interface. It first checks whether an image was uploaded or text was sent using the conditional statement if (message.attachments && message.attachments.length > 0). Depending on the outcome of the conditional statement, it formats the image or text and then renders it on the user interface.

**TheirMessage.jsx**
![image5](https://user-images.githubusercontent.com/87146827/218466380-8905a3ff-4b92-4acf-aac1-adca62382bb7.png)

TheirMessage.jsx retrieves the message sent by another user, generally the photographer,  from MessageForm.jsx and displays it on the chat interface. It begins by checking whether the message sent was the first in a consecutive set of messages, or is a message following an older message. This is done using the statement isFirstMessageByUser = !LastMessage || lastMessage.sender.username !== message.sender.username;.  This is used to determine whether the profile picture of the user should be displayed or not. It then, like MyMessage.jsx, checks whether an image was uploaded or text was sent using if (message.attachments && message.attachments.length > 0). Depending on the outcome of the conditional statement, it formats the image or text and then renders it on the user interface.

**ChatFeed.jsx**
![image6](https://user-images.githubusercontent.com/87146827/218466410-2d5d28f9-63e6-4b39-ab04-48f956e1b42d.png)

ChatFeed.jsx imports MessageForm.jsx, MyMessage.jsx, and TheirMessage.jsx to create the interface where the messages appear.  It is responsible for the chatting section of the program. In addition, it also checks which all users saw the message to display read receipts, which will allow the user to check if the photographer is reading the messages of the user. It also renders the conversations’s title along with the messages. 

**LoginForm.jsx**
![image7](https://user-images.githubusercontent.com/87146827/218466548-f2152788-dd5d-4f15-ae04-22d67501f4b1.png)


LoginForm.jsx is responsible for authenticating users using Chat Engine. It takes the user’s username and password as an input and compares it with the credentials stored in Chat Engine. If the credentials match, the user is logged in, otherwise the error message “Oops, incorrect credentials” is displayed . The correct account is searched for using the project Id, which is set as a constant using const projectId. It also displays an error message if the credentials do not match. The statement const authObject = {‘Project-ID’:projectId, ‘User-Name’: username, ‘User-Secret’: password}; is used to check the credentials. The input is done using the statement input type=“text” value={username} onChange={(e) ⇒ setUsername(e.target.value)} className=“input” placeholder= “Username” required for username and input type=“password” value={password} onChange={(e) ⇒ setPassword(e.target.value)} className=“input” placeholder= “Password” required.

