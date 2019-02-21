# More Flask Notes
Before reading this week's notes, I recommend first checking out [last week's notes](https://github.com/CS196Illinois/lecture-notes-sp19/blob/master/flask.md) on the basics of Flask.

This week we will continue discussing flask but will dive deeping into some of the more interesting things you can do with it. Prior to reading these notes, make sure you are comfortable with GET and POST requests on Flask. You can find a short tutorial [here](https://scotch.io/bar-talk/processing-incoming-request-data-in-flask).

## Response Types
So far, all we've done when our Flask app is called is return a string which is then displayed on the webpage. Fortunately, we can do a lot more with our responses. In addition to these notes, you can find more information about response types [here](http://flask.pocoo.org/docs/0.12/quickstart/). 
### JSON
One of the most common response types of responses is a JSON (JavaScript Object Notation). A typical JSON object may look something like this.
```javascript
{ "class" : "cs-196", 
  "topics" : ["python", "flask", "github"]
}
```
That looks pretty much like a series of nested dictionaries and arrays, and that is exactly what JSON is. In fact, we will cover exactly how to go from a dictionary/array to a JSON and vice versa later in these notes. JSON are extremely useful when conveying complicated data or even an object. If you want to learn more about JSON, you can check out [this page](https://www.w3schools.com/python/python_json.asp).

Now, for our use of JSON, we will be using the json package in python. You should already have access to this python package, but in case you don't, you can download this package by running
```
pip install json
```
There are four main commands we will be using from this package, `dump`, `dumps`, `load`, `loads`. You can find comprehensive documentation on these [here](https://docs.python.org/2/library/json.html). 

The dump and dumps functions can be used to convert a dictionary/array into a json object. The dump conmmand converts it to an actual json object, while dumps converts to a string representation of the json object (which is what we need for our flask app since we will want to be sending and receiving strings from our server). Here is an example.

```python
import json
my_dict = ['greeting': 'hello', 'fairwell' : 'goodbye'}
my_json = json.dump(my_dict)
my_str = json.dumps(my_dict)
```
The load and loads functions do the opposite. load converts a json object to a dictionary/array, and loads converts a string representation of json into a dictionary.

#### Using JSON with Flask
Now that you understand JSON, lets see how we can use it for our flask app. A common use of JSON for flask is when making get and post requests. I will now demo a simple flask app here, which we will dissect part by part. This app will store student's informations and will have both GET and POST functionalities

```python
from flask import Flask, request
import json

students = {}
app = Flask(__name__)

@app.route('/info', methods = ['POST', 'GET'])
def info():
	if request.method == 'POST':
		my_dict = request.args
		name = my_dict.get('name', "")
		students[name] = my_dict
		return json.dumps(students)
	else:
		r = request.args
		my_student = students.get(r['name'], "")
		return json.dumps(my_student)


if __name__ == "__main__":
    app.run()
```
Lets go through this part by part. We have 1 method called info. This method allows us to both add students and remove students. As you 
Becan see by the route, this method performs both GET and POST. The if-statement here checks the method being performed is a POST request. If it is, I can access the parameters to the post via `request.args` and from that I get the name of the student being added and use that to add my student to my `students` dictionary. The value being returned here is the response that the POSTer will receive. In this case, I am just returning the full dictionary of students (Note that I convert the dictionary to a JSON string). 

Before I continue to what the rest of the function is doing, let us discuss how we can test this. We can use a tool called Postman. 
You can find more information on POST requests and how to download Postman [here](https://techtutorialsx.com/2017/01/07/flask-parsing-json-data/). Postman allows you to specify the endpoint. Which can be the url here, specify the parameters, and run the request. Here is a screenshot demonstrating a response from Postman for our server here. 

![Postman Post](https://github.com/CS196Illinois/lecture-note-images/blob/master/PostmanPOST.png)

Now, lets move onto the else statement. The else statement works to tell us what to do if the request is a GET request. If the request is a GET, we will assume that the user will pass in the desired name as an arg. So we can use `request.args` to get the args, find the "name" parameter, search our students dictionary for the name, and return the relevant object (once again converting the object to a string representation of a JSON). Here is an example of how to test this on Postman.

![Postman GET](https://github.com/CS196Illinois/lecture-note-images/blob/master/PostmanGET.png)


In these examples, we only focus on the `args` and `method` fields of a request object, but there are also many other fields avaiable to us. In additional to a request object, there are also response objects which can be retrieved after performing a command. The response object can be to check the status of a request in addition to any response message the server may return. When using Postman, the `body` field of the response object is printed. This `body` field is whatever is being returned by your python method. You can learn more about requests and responses [here](https://flask-restless.readthedocs.io/en/latest/requestformat.html). 

Hopefully this has provided you with a brief overview of how JSON can be used in conjunction with Flask

### Error Handling
As you experiment with Flask, I'm sure you've reached a point where you try to perform a compand or look at a page, and an error has been thrown. Luckily, you are actually able to control your flask app's response to some of these errors. Lets look at a common error that may occur. 404: Page not found. Here is a simple handler for the error.
```python
@app.errorhandler(404)
def page_not_found(error):
	return "This page does not exist"
```
Here, if the status code of the request is a 404, rather than allowing a default error page to be displayed, we will instead get sent to a page with this message. The ability to handler errors can be extremely versatile.

### Redirect
Flask also allows you to redirect a user from one route to another. This other route can be another webpage altogether or even another route defined in the app.

```python
from flask import Flask, redirect, url_for
app = Flask(__name__)

@app.route('/')
def index():
	return redirect(url_for('greeting'))

@app.route('/greeting')
def greeting():
	return "Hello World"
```
In this example, when we visit our index page via the `/` route, we will automatically get redirected to a page that says Hello World. In this example, the `url_for` method is used to get the url associated with the greeting route. In practice, `redirect` can be passed in any url to redirect to.


### Files
We discussed earlier the `args` and `method` field of request, but `request` also has a `files` field which can be used to store files. Here is an example of a flask app that takes in a file and stores it to its local storage.
```python
from flask import Flask, request
app = Flask(__name__)

@app.route('/uploadphoto', methods = ['POST'])
def upload_photo():
	if request.method == 'POST':
		f = request.files['myPhoto']
		f.save('[insert url path here]/myPhoto.png')
```
This method takes the photo with the key name 'myPhoto' and saves it to the server's local storage. 

There are many other useful/interseting response types available for Flask that you should definitely look into. You can find information about many of them in the links above. 


