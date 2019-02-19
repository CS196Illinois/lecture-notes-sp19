## Introduction to Servers: Part 1 ##
### Background ###

**TL;DR:** Servers and APIs are an important aspect of computing, and knowing how to use them is an essential skill.

In this class, we want to teach you the basic skills neccesary to explore your interests within Computer Science (and to work on your projects). One of the most important of these skills is the ability to work with servers and APIs. Servers, in the simplest sense, are just a remote computers running applications to handle logic or give access to shared resoures. If you are new to Computer Science, this may seeem like an odd concept — you might be tempted to ask why we don't just handle all of our app's logic on the device the app is running on? For very simple or offline apps (like a text editor), this might work, but as you'll soon see when working on your own project, you'll often  need a way to communicate with other devices or access shared files. Take, for example, a basic messaging app. Clearly, you cannot receive messages from other users without somehow communicating with their device. To solve this problem, you can have a separate computer running somewhere remotely that listens to messsages from the devices using the messaging app, and sends updates to each user when a new message comes in (in some cases, you can use communication protocols that send messages directly between devices, but these genereally rely on some type of server as well).

Another example of the use of servers is accessing information through an Application Programming Interface (or API for short). When it comes to web applications, an API is basically a set of functions that allow you to send or retrieve information from a server. A weather API, for example, may have one function that returns you temperature values and another that returns precipitation data (and these functions may take in paramters, like zipcode or date). Using APIs is very common, as APIs give you access to things like weather data, stock data, or even advanced machine learning techniques — things that you might not be able to code and/or run efficiently on your own! The internet is full of useful tools and information, and APIs are the gateway to a large portion of it!

*Side Note:* When discussing servers, we will often use the word *client*, which refers to a user/device that is requesting information from a server. A simple example of this is you when you loaded this webpage to read these notes. You (or more specifically your device) acted as a a client by sending a request to the GitHub server, and the server, in return, gave you this page.


#### How do we communicate with servers? ####
When communicating with servers, we need a way to send and receive messages in a way that both a client and a server can understand. One of the most common ways of sending such information is Hyper Text Transfer Protocol (or HTTP for short). In simple terms, HTTP is a protocol that defines how messages are sent between computers. Within HTTP, there are different types of messages, called requests, that can be sent in order to request data and share information. We will be most concerned with **GET** and **POST** requests. Below is a very basic description of what each does:

- **GET Request:** GET requests are used to retrieve information from a specified URL. When you load a simple website in your browser, you are likely sending  a GET request for that site's URL. In general, it is assumed that GET requests are *repeatable*, meaning that you can safely send a GET request and retrieve information multiple times in a row without worrying about the server making internal changes. (e.g. for a banking application, you could use a GET request to see the balance of  an account, because viewing the balance repeatedly would not affect the balance itself). When making a GET request, you can send in arguments by using *URL parameters*, as we will see in a later section.

- **POST Request** In contrast with GET requests, POST requests are generally used to send larger amounts of data and are *not* assumed to be repeatable (in our bank account example from above, we would use a POST request to change the account balance). When making a POST requests, you include a *content body* with the data that you want to send to the server. Unlike other request types, POST requests have no limit to the amount of data that can be sent in the content body, so you should use them when sending a lot of information at once (e.g. complex parameters/information or files).

The descriptions above should be sufficient to follow the tutorial below, but if you would like to know more about HTTP, feel free to check out [this article](https://www.httpwatch.com/httpgallery/introduction/) (for more info on GET and POST requests, skip ahead to the [methods section](https://www.httpwatch.com/httpgallery/methods/) of the article).

### Flask: The basics. ###
#### Overview ####
Flask is a framework for creating web applications, that is, the applications you will run on a server. There are many frameworks for doing this, some popular ones include Flask (Python), Django (Python), NodeJS (JavaScript), and Ruby on Rails (Ruby). There are pros and cons to all of these, but for this course we will stick with Flask because it is relatively simple (and because it is Python-based). Below we will show how to setup Flask and how to build a simple server/API. 

#### Installing Flask ####

To install flask on your machine, you can use *pip*:

If you don't have pip already, you can do the following:

1. Download the pip installation file:
```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
```
2. Run the installation file:
```
python get-pip.py
```

If this doesn't work, check out [this site](https://www.makeuseof.com/tag/install-pip-for-python/) for a variety of alternative installation methods.

Once pip is installed, you can install Flask using the following command:

```
pip install Flask
```

If this command executes succesfully, you now have all the libraries you need to start using Flask!

#### Hello World ####

Below is an example of how to set up a very simple 'Hello World' application in Flask.

Create a new file called *app.py*. Add the following:

```python
from flask import Flask
app = Flask(__name__)
 
@app.route("/")            # The URL for our request
def hello():               # The function to run when a client makes a request
    return "Hello World!"  # The data to return
 
if __name__ == "__main__":
    app.run()
```

You can start the server by executing the python file in your terminal. The output should look something like this:

```
python app.py 
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Go to your web browser, and type "http://127.0.0.1:5000/" into the address bar. When you click enter, a page containing the words "Hello World!" should show up. Congratulations, you just built your first server!

For now, don't worry too much about what the first two lines and the last two lines of *app.py* do, it's just basic code that handles importing the Flask library and starting our server. The important stuff is in the middle. The *app.route* decorator tells Flask to run the function below it (in this case 'hello'), when a client accesses the server's URL. By default, Flask treats this as a GET request (we'll discuss how to set up a POST request later)

#### Setting up more endpoints ####

To set up another *endpoint* (that is, another URL that our server uses to receive data), we can use *app.route* and define more functions:

```python
from flask import Flask
app = Flask(__name__)
 
@app.route("/")
def boring_url():
    return "Boring! Try one of the different URLs (/poem or /quote)"
    
@app.route("/quote")
def get_quote():
    return '"Get busy living or get busy dying." - Stephen King'
    
@app.route("/poem")
def get_poem():
    return "Roses are red, violets are blue, learning servers will help you!"
 
if __name__ == "__main__":
    app.run()
```

Start the app again, and go to http://127.0.0.1:5000/, http://127.0.0.1:5000/quote, http://127.0.0.1:5000/poem. The repsonses should correlate with the functions we just defined! Note that it deosn't matter what we name the functions underneath *app.route* — we could have used the function name *not_a_poem* instead of *get_poem* and it would have worked fine!

#### Using parameters from a GET request ####

As mentioned earlier, get requests allow clients to send in parameters to GET requests. To handle this in Flask, we can do the following:

```python
from flask import Flask
from flask import request    # The module used to access info from the request
app = Flask(__name__)
 
@app.route("/")
def boring_url():
    return "Boring! Try one the /double url"
 
@app.route("/multiply")
def multiply():
    return str(int(request.args.get('num1')) * int(request.args.get('num2')))
    
if __name__ == "__main__":
    app.run()
```

To test your endpoint, type the following in your web browser:
http://127.0.0.1:5000/multiply?num1=5&num2=6

The '?' specifies that we are defining a URL parameter, and the & separates different URL parameters. For our basic implementation, if you leave either parameter out, you will get an internal server error. In general, you would do some preliminary checking to ensure that the correct number/type of arguments were passed in, and return the proper error.

Another way to pass in parameters is by using the endpoint directly:

```python
from flask import Flask
from flask import request
app = Flask(__name__)

@app.route("/")
def boring_url():
    return "Boring! Try one the /double url"

@app.route("/multiply/<num1>/<num2>")
def multiply(num1, num2):
    return str(int(num1) * int(num2))

if __name__ == "__main__":
    app.run()
```

To get the same result, we can now go to: http://127.0.0.1:5000/multiply/5/6

#### Using data from a POST request ####

We'll cover this in more detail later on, but if you want to use the data from a POST request, you can do the following:

```python
from flask import Flask
from flask import request
app = Flask(__name__)

@app.route('/check_code', methods = ['POST'])  # This is how we tell Flask this is a POST request
def check_code():
    code = request.form['secret_code']
    if code == '1234':
        return 'Correct!'
    else:
        return 'Incorrect :('
        
if __name__ == "__main__":
    app.run()
```

The body of a POST request cannot be sent in via the URL like the parameters of a GET request. To test POST requests, you will either need to programatically send a POST request in Python, or use a tool like [Postman](https://www.getpostman.com/) (I will show examples of this in lecture)

**IMPORTANT:** The code snippets above are only basic examples of what you can do in Flask. If you want to learn more about Flask's features, and how to use Flask to build a robust API or website (with things like HTML templates, forms, an user login), check out [this Flask Tutorial](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). (Or Google one! There are a lot of online resources for learning Flask!)


