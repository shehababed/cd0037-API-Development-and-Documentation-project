## Trivia App

Udacity is invested in creating bonding experiences for its employees and students. A bunch of team members got the idea to hold trivia on a regular basis and created a webpage to manage the trivia app and play the game,so they can hold trivia and see who's the most knowledgeable of the bunch .

## Description of the Trivia App API

1. Displays questions - both all questions and by category. Questions shows the question, category and difficulty rating by default and can show/hide the answer.
2. Deletes questions.
3. Adds questions, question and answer text are required.
4. Searches for questions based on a text query string.
5. Playes the quiz game, randomizing either all questions or within a specific category.

# Backend - Trivia API

## Setting up the Backend

### Install Dependencies

1. **Python 3.7** - Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

2. **Virtual Environment** - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

3. **PIP Dependencies** - Once your virtual environment is setup and running, install the required dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

#### Key Pip Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use to handle the lightweight SQL database. You'll primarily work in `app.py`and can reference `models.py`.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross-origin requests from our frontend server.

### Setting up the Database

With Postgres running, create a `trivia` database:

```bash
createbd trivia
```

Populate the database using the `trivia.psql` file provided. From the `backend` folder in terminal run:

```bash
psql trivia < trivia.psql
```

### Runnig the Server

From within the `./src` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

The `FLASK_APP=flaskr` will direct flask to use the `flaskr` directory and the `__init__.py` file to find the application.
The `export FLASK_ENV=development` will set the variable `FLASK_ENV` to `development`, detect file changes and restart the server automatically.

# Frontend - Trivia API

## Getting Setup

> _tip_: this frontend is designed to work with [Flask-based Backend](../backend) so it will not load successfully if the backend is not working or not connected. We recommend that you **stand up the backend first**, test using Postman or curl, update the endpoints in the frontend, and then the frontend should integrate smoothly.

### Installing Dependencies

1. **Installing Node and NPM**
   This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (the download includes NPM) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

2. **Installing project dependencies**
   This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the `frontend` directory of this repository. After cloning, open your terminal and run:

```bash
npm install
```
> _tip_: `npm i`is shorthand for `npm install``

# Required Tasks

### Running Your Frontend in Dev Mode

The frontend app was built using create-react-app. In order to run the app in development mode use `npm start`. You can change the script in the `package.json` file.

Open [http://localhost:3000](http://localhost:3000) to view it in the browser. The page will reload if you make edits.

```bash
npm start
```

### Tests
In order to run tests navigate to the backend folder and run the following commands: 

```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```

The first time you run the tests, omit the dropdb command. 

All tests are kept in that file and should be maintained as updates are made to app functionality.

### Error Handling
Errors are returned as JSON objects in the following format:
```
{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
```
The API will return the following error types when requests fail:
- 400: Bad Request.
- 404: Resource Not Found.
- 405: Method Not Allowed.
- 422: Not Processable.
- 500: Internal Server Error.

### Endpoints

#### GET /questions
- General:
    - Returns a list of question objects, success value, and total number of questions.
    - Results are paginated in groups of 10. starting from 1. 
- Sample:
`curl http://localhost:5000/questions`
{
    "categories": [
        "Entertainment",
        "Sports",
        "History",
        "Geography"
    ],
    "category": [],
    "questions": [
        {
            "answer": "Apollo 13",
            "category": 5,
            "difficulty": 4,
            "id": 2,
            "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
        },
        {
            "answer": "Tom Cruise",
            "category": 5,
            "difficulty": 4,
            "id": 4,
            "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
        },
        {
            "answer": "Maya Angelou",
            "category": 4,
            "difficulty": 2,
            "id": 5,
            "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
        },
        {
            "answer": "Edward Scissorhands",
            "category": 5,
            "difficulty": 3,
            "id": 6,
            "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
        },
        {
            "answer": "Muhammad Ali",
            "category": 4,
            "difficulty": 1,
            "id": 9,
            "question": "What boxer's original name is Cassius Clay?"
        },
        {
            "answer": "Brazil",
            "category": 6,
            "difficulty": 3,
            "id": 10,
            "question": "Which is the only team to play in every soccer World Cup tournament?"
        },
        {
            "answer": "Uruguay",
            "category": 6,
            "difficulty": 4,
            "id": 11,
            "question": "Which country won the first ever soccer World Cup in 1930?"
        },
        {
            "answer": "George Washington Carver",
            "category": 4,
            "difficulty": 2,
            "id": 12,
            "question": "Who invented Peanut Butter?"
        },
        {
            "answer": "Lake Victoria",
            "category": 3,
            "difficulty": 2,
            "id": 13,
            "question": "What is the largest lake in Africa?"
        },
        {
            "answer": "The Palace of Versailles",
            "category": 3,
            "difficulty": 3,
            "id": 14,
            "question": "In which royal palace would you find the Hall of Mirrors?"
        }
    ],
    "success": true,
    "total_questions": 23
}

#### POST /books
- General:
    - Creates a new question using the submitted question, answer and category in the react frontend.
    - Returns the id of the created question, success value and total questions.
    - If search field is present will return a result that matches the search_term.

- Sample(create): 
`curl http://localhost:5000/questions -X POST -H "Content-Type: application/json" -d '{"question": "How many grammies does DJ Khalid have?", "answer": "All of them", "category": 5, "difficulty": 4}'`
```
{
    "created": 31,
    "question": {
        "answer": "All of them",
        "category": 5,
        "difficulty": 4,
        "id": 31,
        "question": "How many grammies does DJ Khalid have?"
    },
    "success": true,
    "total_questions": 25
}
```
- Sample(search):
`curl http://localhost:5000/questions -X POST -H "Content-Type: application/json" -d '{"search_term":"1996"}'`
```
"questions": [
        {
            "answer": "Apollo 13",
            "category": 5,
            "difficulty": 4,
            "id": 2,
            "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
        },
        ],
    "success": true,
    "total_questions": 1
    }
```

### GET '/categories/<cat_id>/questions'
- Returns JSON response of the category, and the questions of that category.

- Sample: `curl http://localhost:5000/categories/4/questions`
```
{
    "categories": [
        {
            "id": 4,
            "type": "History"
        }
    ],
    "questions": [
        {
            "answer": "Maya Angelou",
            "category": 4,
            "difficulty": 2,
            "id": 5,
            "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
        },
        {
            "answer": "Muhammad Ali",
            "category": 4,
            "difficulty": 1,
            "id": 9,
            "question": "What boxer's original name is Cassius Clay?"
        },
        {
            "answer": "George Washington Carver",
            "category": 4,
            "difficulty": 2,
            "id": 12,
            "question": "Who invented Peanut Butter?"
        },
        {
            "answer": "Scarab",
            "category": 4,
            "difficulty": 4,
            "id": 23,
            "question": "Which dung beetle was worshipped by the ancient Egyptians?"
        }
    ],
    "success": true,
    "total_questions": 4
}
```

### DELETE '/questions/<int:question_id>'
- Deletes a selected question by id.
- If question is successfully deleted, it will return 200.
- If question did not exist, it will return 404.
- Returns JSON object of deleted id, remaining questions, and length of total questions.

- Sample: `curl -X DELETE http://localhost:5000/question/4`
```
{
    "deleted": 4,
    "questions": [
        {
            "answer": "Tom Cruise",
            "category": 5,
            "difficulty": 4,
            "id": 4,
            "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
        }    
        ...
    ],
    "success": true,
    "total_questions": 24
}
```

### POST '/quizzes'
- Gets a quiz based on category or a random selection depending on what the user chooses.
- Returns a random question.

- Sample: `curl http://localhost:5000/quizzes -X POST -H "Content-Type: application/json" -d '{"previous_question":[], "category":{"type":"Entertainment","id":5}}'`
```
{
    "question": {
        "answer": "Tom Cruise",
        "category": 5,
        "difficulty": 4,
        "id": 4,
        "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    },
    "success": true
}
```
## Deployment N/A