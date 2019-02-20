# More Flask Notes
Before reading this week's notes, I recommend first checking out [last week's notes](https://github.com/CS196Illinois/lecture-notes-sp19/blob/master/flask.md) on the basics of Flask.

This week we will continue discussing flask but will dive deeping into some of the more interesting things you can do with it. Prior to reading these notes, make sure you are comfortable with GET and POST requests on Flask. You can find a short tutorial [here](https://scotch.io/bar-talk/processing-incoming-request-data-in-flask).

## Response Types
So far, all we've done when our Flask app is called is return a string which is then displayed on the webpage. Fortunately, we can do a lot more with our responses. 
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
Now that you understand JSON, lets see how we can use it for our flask app. A common use of JSON for flask is when making get and post requests. For example, if we want to get and post some information about myself, I can do the following.

```python
from flask import Flask, request
import json

app = Flask(__name__)

app.route('/info', methods = ['POST'])
def postinfo():
  
```
Note here that when I am describing the route, I specify that the method I want to use is POST. I can now test this method out by using POST a useful tool called Postman which allows me to easily test my HTTP requests from an easy to use tool. You can find more info about postman and POST requests on flask [here](https://techtutorialsx.com/2017/01/07/flask-parsing-json-data/).

Another way I can test this code out is by writing a GET request that will return to me this json of information. 


