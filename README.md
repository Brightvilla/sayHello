# Say Hello - Flask Greeting App

## Project Description

This is a simple Flask web application that greets users by name. The app consists of a single page with a form where users can enter their name and receive a personalized greeting message.

## Project Structure

```
sayHello/
├── app.py                          # Main Flask application
├── templates/
│   └── index.html                  # HTML template for the greeting page
├── static/
│   └── css/
│       └── main.css                # CSS styles for the page
├── requirements.txt                # Python dependencies
├── requirements_versions.txt       # Pinned dependency versions
├── environment.yml                 # Conda environment configuration
├── Procfile                        # Heroku deployment configuration
└── typical list for a professional project.txt  # Alternative dependency list
```

## Setup and Installation

### Prerequisites
- Python 3.9 or higher
- pip (Python package installer)

### Installation Steps

1. **Clone or download the project:**
   ```bash
   git clone https://github.com/Brightvilla/sayHello.git
   cd sayHello
   ```

2. **Create a virtual environment (optional but recommended):**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application:**
   ```bash
   python app.py
   ```

5. **Open your browser and navigate to:**
   ```
   http://localhost:5000/hello
   ```

### Alternative Setup with Conda

If you prefer using Conda:

```bash
conda env create -f environment.yml
conda activate env39
pip install -r requirements.txt
python app.py
```

## Deployment

### Heroku Deployment

The project includes a `Procfile` for Heroku deployment:

```
web: gunicorn app:app
```

To deploy to Heroku:

1. Install Heroku CLI
2. Login to Heroku: `heroku login`
3. Create a new app: `heroku create your-app-name`
4. Push to Heroku: `git push heroku master`

## Code Explanation

### app.py - Main Flask Application

```python
from flask import Flask, render_template, request, flash
```
**Line 1:** Imports necessary modules from Flask:
- `Flask`: The main Flask class for creating the web application
- `render_template`: Function to render HTML templates
- `request`: Object to handle HTTP requests and access form data
- `flash`: Function to display temporary messages to users

```python
app = Flask(__name__)
```
**Line 2:** Creates a Flask application instance. `__name__` is a special Python variable that represents the name of the current module.

```python
app.secret_key = "manbearpig_MUDMAN888"
```
**Line 3:** Sets a secret key for the Flask application. This is required for session management and flashing messages. In production, this should be a secure, randomly generated key stored as an environment variable.

```python
@app.route("/hello")
def index():
```
**Line 4:** Defines a route decorator for the URL path "/hello". This tells Flask that the following function should handle requests to this URL.

```python
    flash("what's your name?")
    return render_template("index.html")
```
**Lines 5-6:** 
- **Line 5:** Uses `flash()` to store a message that will be displayed on the next request. This message asks for the user's name.
- **Line 6:** Renders and returns the "index.html" template, which will display the flashed message and the form.

```python
@app.route("/greet", methods=["POST", "GET"])
def greet():
```
**Line 7:** Defines another route for "/greet" that accepts both POST and GET HTTP methods. POST is used when submitting the form, GET might be used for direct access.

```python
    flash("Hi " + str(request.form['name_input']) + ", great to see you!")
    return render_template("index.html")
```
**Lines 8-9:**
- **Line 8:** Creates a personalized greeting message using the name submitted in the form. `request.form['name_input']` accesses the value from the form field named "name_input". The message is flashed for display.
- **Line 9:** Renders the same "index.html" template, which will now show the greeting message.

### templates/index.html - HTML Template

```html
<!DOCTYPE html>
<html>
```
**Lines 1-2:** Standard HTML5 document declaration and opening html tag.

```html
      <head>
      	   <meta charset="UTF-8">
      	   <title>Say Hello</title>
      	   <link rel="stylesheet" href="{{ url_for('static', filename='css/main.css')}}">
      </head>
```
**Lines 3-7:**
- **Line 3:** Opening head tag
- **Line 4:** Meta tag specifying UTF-8 character encoding
- **Line 5:** Title tag that sets the page title to "Say Hello"
- **Line 6:** Link tag that loads the CSS stylesheet. `{{ url_for('static', filename='css/main.css') }}` is a Jinja2 template expression that generates the URL for the static file
- **Line 7:** Closing head tag

```html
      <body>
      	    <img src="https://raw.githubusercontent.com/MariyaSha/SimpleGreetingApp/main/logo.png">
```
**Lines 8-9:**
- **Line 8:** Opening body tag
- **Line 9:** Image tag displaying a logo from an external GitHub repository

```html
          <br>
      	    <form action="greet" method="post">
```
**Lines 10-11:**
- **Line 10:** Line break
- **Line 11:** Opening form tag that submits to the "/greet" route using POST method

```html
      	        {% for message in get_flashed_messages()%}
      	       	    <p> {{message}} </p>
      	   	    {% endfor %}
```
**Lines 12-15:** Jinja2 template loop that iterates through flashed messages and displays each one in a paragraph tag.

```html
      	   	    <br>
      	     	  <input type ="text" name="name_input">
```
**Lines 16-17:**
- **Line 16:** Line break
- **Line 17:** Text input field with name "name_input" for user to enter their name

```html
      	       	<br>
      	    	    <input type="submit" value="GREET" id="greet">
```
**Lines 18-19:**
- **Line 18:** Line break
- **Line 19:** Submit button with text "GREET" and CSS id "greet"

```html
      	    </form>	

      </body>

</html>
```
**Lines 20-23:** Closing tags for form, body, and html.

### static/css/main.css - Stylesheet

```css
body {
     background-color: slategray;
     text-align: center;
     }
```
**Lines 1-4:** Styles for the body element:
- Sets background color to slategray
- Centers all text horizontally

```css
     
  p {
     color: white;
     font: Shanti;
     font-size: 1.2em;
     margin: 20px;
     }
```
**Lines 6-11:** Styles for paragraph elements:
- White text color
- Uses "Shanti" font family
- Font size of 1.2em (120% of default)
- 20px margin on all sides

```css
     
img {
     margin: 60px 0 30px 0;
     width: 250px;
     }
```
**Lines 13-16:** Styles for image elements:
- Top margin of 60px, bottom margin of 30px, no left/right margins
- Fixed width of 250px

```css
     
 input {
      width: 300px;
      height: 50px;
      margin: 20px;
      border-radius: 10px;
      text-align: center;
      font-size: 1.3em;
      }
```
**Lines 18-25:** Styles for all input elements:
- Width of 300px, height of 50px
- 20px margin on all sides
- 10px border radius for rounded corners
- Center-aligned text
- Font size of 1.3em

```css
      
#greet {
       background-color: palevioletred;
       color: white;
       width; 200px;
       }
```
**Lines 27-31:** Styles for the element with id "greet" (the submit button):
- Pale violet red background color
- White text color
- Width of 200px (note: there's a syntax error here - should be "width: 200px;" not "width; 200px;")

```css
       
#greet:hover {
        background-color: mediumvioletred;
        cursor: white;
       }
```
**Lines 33-36:** Hover styles for the greet button:
- Changes background to medium violet red on hover
- Sets cursor to white (this is incorrect - cursor should be a cursor type like "pointer", not a color)

## Dependencies

### requirements.txt
Lists the basic Python packages required:
- Flask: Web framework
- gunicorn: WSGI server for production
- Other Flask dependencies (Jinja2, Werkzeug, etc.)

### requirements_versions.txt
Same packages but with specific versions pinned for reproducibility.

### environment.yml
Conda environment configuration with Python 3.9 and additional packages (matplotlib, numpy, jupyter, pandas) that aren't actually used in this simple app.

### typical list for a professional project.txt
An alternative list with more Flask extensions commonly used in professional projects.

## Usage

1. Navigate to `/hello` to see the greeting form
2. Enter your name in the text field
3. Click "GREET" to submit
4. The page will display a personalized greeting message

## Notes

- This is a basic Flask application demonstrating routing, templates, and form handling
- The app uses Flask's flash messaging system for temporary messages
- Static files (CSS, images) are served from the `/static` directory
- Templates are stored in the `/templates` directory
- The app runs on Flask's default development server (not suitable for production)

## Contributing

Feel free to submit issues and enhancement requests!</content>
<parameter name="filePath">/home/bright-mahonga/Python/sayHello/README.md

## Copyright
Python Web Development Simplified ,Mariyah Shah
Aws,2026
