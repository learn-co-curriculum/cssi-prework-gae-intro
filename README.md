
# Intro to Google App Engine

**Google App Engine** is a Platform as a Service (PaaS) offering that lets you build and run applications on Google’s infrastructure. You upload your files through the App Engine interface and your app gets hosted on Google's servers. App Engine connects the back-end (the Python scripts) and front-end (the HTML/CSS/JavaScript) for you with minimal work on your end.

## MVC
The model-view-controller framework guides Google App Engine.

<img src="http://lh3.ggpht.com/aviadezra/SHj6gLRSkSI/AAAAAAAAALg/0xkCGOXuefc/image_thumb3.png?imgmax=800" width=300px>

+ **Models** (Back-end data - Datastore in App Engine)
  + Stores the data
+ **Views** (Front-end - HTML Template in App Engine)
  + The front end, this is what the user sees.
+ **Controller** (Back-end logic - our Python scripts in App Engine)
 + The code that is in charge of making the back end communicate to the front end

Keeping the functionality of our application in these separate directories helps us add layers of complexity while still keeping our code organized.

## Clients and Servers
Before we continue to introduce Google App Engine, let's review how anyone on the internet can access the code that you write locally at home.

The internet is a network of computers that communicate with eachother using HTTP - a protocol which defines how data is delivered. HTTP isn't a main focus for your students at CSSI but you can learn more about it [here](http://www.tutorialspoint.com/http/http_overview.htm).

The computers that are communicating in this vast network can either be clients, servers or often times both.

![Client and Server Diagram](https://mdn.mozillademos.org/files/4291/client-server.png)


## Requests
Your webapp needs to be able to get data (a request) from a user and send data back from the server (a response).

There are two ways that a client (users) can make a request (send data): **GET** and **POST**
 + GET - data is stored within a URL
 + POST - data is submitted and temporarily stored
 
(Technically, there are also a few other types of request, but we're not going to be talking about them or using them during CSSI)

You will learn how to deal with both of these types of requests during our time together at CSSI training.

## Responding to Requests using Handlers and Routes
When a user puts in a certain url or presses a button, you need to add instructions to your App Engine controller on how to respond. In Google App Engine, those instructions are called  handlers. Each handler is a block of code that is set up to send a certain response to get and post requests.

```python
class MainHandler(webapp2.RequestHandler):
    def get(self):
        self.response.write('Hello world!')

class CountHandler(webapp2.RequestHandler):
    def get(self):
        for i in range(1, 101):
            self.response.write(i)

app = webapp2.WSGIApplication([
    ('/', MainHandler),
    ('/count', CountHandler),
], debug=True)
```

MainHandler and CountHandler both respond in different ways. MainHandler displays "Hello World" while CountHandler will print 1-100. But when does CountHandler get executed and when does MainHandler get executed? The distinction is written in the controller's routes. A route is a like a map that shows which handler to run for each url. In App Engine, the routes are listed as a parameter to the `WSGIApplication` method.
For example:
* If the user's request was `localhost:8080/` , then the MainHandler would respond
* If the user's request was `localhost:8080/count` , then the CountHandler would respond

## Conclusion
Google App Engine allows the three pieces of a webapp - the model, view and controller to connect to eachother. The controller is the interface that sends data back and forth between the views (which the user interacts with) and the model (where the data is stored). Within the controller, handlers and routes are written to respond in specific ways so that you webapp can be responsive. You will practice writing handlers and routes during our time together in Mountain View for CSSI training. 
