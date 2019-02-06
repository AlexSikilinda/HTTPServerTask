# Goal:
Develop a basic HTTP server.

# Task:
Create a HTTP server wich is based on HttpListener class. It should map incoming requests to appropriate classes and methods.

# Minimal functionality:

1. HttpListener which can process HTTP messages.
2. Each HTTP requests is mapped on a coresponding class and method (we will call such classes "Controllers" and such methods - "Actions").
3. There should be a way to pass some parameters to the methods (see data binding section).
4. The response of the method should be returned as HTTP response.
5. Using this controller features write a simple "Chat" application using HTTP protocols. Write a simple console client for this chat. (You are encouraged to write win forms or html implementation for this chat client).
6. All possible scenarios should be covered with unit tests (xUnit)
7. As the next, third project you need to store chat messages in a database using ADO.NET (ideally both Disconnected Layer and EntityFramework)

# Routing

We will call the process of determening which "Controller" and which "action method" to invoke as "Routing".
Routing system will take the incoming request's URL and return Type object and Method object to invoke.
Routing is based on URL segments, e.g.:

http://localhost:51111/myapp/home/index -> we use two last segments of the URL: "home" and "index".
This means that we are going to use class **HomeController** (let's agree that all controllers end with Controller suffix) 
and **Index** method.

http://localhost:51111/myapp/chat/getallchatitems -> **ChatController** class, **GetAllChatItems** method.

# Data Binding 

Just invoking methods is not enough. We should be ablo to pass some parameters to this method (for example chat message
or user name). We will get this parameters from URL, e.g.:

URL: http://localhost:51111/myapp/chat/postmessage?message=helloworld&username=Alexander
Controller and action: **ChatController**, **PostMessage**
Paramters: 1) message - "helloworld", username - "Alexander"

With this url our server will need to call the following method:

    public class ChatController
    {
        public string PostMessage(string message, string username)
        {
            // here message variable = "helloworld", username = "Alexander"
            // now we can write the logic here to user our parameters
        }
    }

# Advanced tasks (desirable but not obligatory):

1. Incorporate your IoC container for creating controllers (thus you can injects some dependencies in controller's constructor or property).
2. Add ability to databind different types (not only string, but also int, bool and even complex types (user defined classes)).
3. Add ability to inspect request's headers in controller. (You may need a base Controller class for this).
4. Add ability to set response headers in controller.
6. injection of simple types, such as integers, strings etc.

# Resources:
* Networking lecture
* ADO.NET lecture
* EF lecture
