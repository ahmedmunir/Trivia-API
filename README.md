# Full Stack API Final Project

## Full Stack Trivia

Udacity is invested in creating bonding experiences for its employees and students. A bunch of team members got the idea to hold trivia on a regular basis and created a  webpage to manage the trivia app and play the game, but their API experience is limited and still needs to be built out. 

That's where you come in! Help them finish the trivia app so they can start holding trivia and seeing who's the most knowledgeable of the bunch. The application must:

1) Display questions - both all questions and by category. Questions should show the question, category and difficulty rating by default and can show/hide the answer. 
2) Delete questions.
3) Add questions and require that they include question and answer text.
4) Search for questions based on a text query string.
5) Play the quiz game, randomizing either all questions or within a specific category. 

Completing this trivia app will give you the ability to structure plan, implement, and test an API - skills essential for enabling your future applications to communicate with others. 

## Tasks

There are `TODO` comments throughout project. Start by reading the READMEs in:

1. [`./frontend/`](./frontend/README.md)
2. [`./backend/`](./backend/README.md)

We recommend following the instructions in those files in order. This order will look familiar from our prior work in the course.

## Starting and Submitting the Project

[Fork](https://help.github.com/en/articles/fork-a-repo) the [project repository]() and [Clone](https://help.github.com/en/articles/cloning-a-repository) your forked repository to your machine. Work on the project locally and make sure to push all your changes to the remote repository before submitting the link to your repository in the Classroom. 

## About the Stack

We started the full stack application for you. It is desiged with some key functional areas:

### Backend

The `./backend` directory contains a partially completed Flask and SQLAlchemy server. You will work primarily in app.py to define your endpoints and can reference models.py for DB and SQLAlchemy setup. 

### Frontend

The `./frontend` directory contains a complete React frontend to consume the data from the Flask server. You will need to update the endpoints after you define them in the backend. Those areas are marked with TODO and can be searched for expediency. 

Pay special attention to what data the frontend is expecting from each API response to help guide how you format your API. 

[View the README.md within ./frontend for more details.](./frontend/README.md)

## Installation:
### Backend:

```
cd ./backend
python -m virtualenv venv # Create virtual environment
./venv/Scripts/activate.bat # Activate virtual environment
pip install -r requirements.txt # Install all requirements
export FLASK_APP=flaskr
export FLASK_ENV=development # Run in development mode
flask run # Run backend server
```

### Frontend:
Install Node.JS then at termonal
```
cd ./frontend
npm install # Install dependancies required by front end React project
npm start # Start front end project
```

## API Reference:
### Getting Started:
- Base URL: The base URL for this application will be: **http://127.0.0.1:5000/** and doesn't require authentication or API keys.

### Error Handling:
Errors are returned as JSON objects in the following format:
```
  "success": False,
  "error": 400,
  "message": "bad request"
```
The API will return three error types when requests fail:
- 400: Bad request
- 404: resource not found
- 422: unprocessable

### Endpoints: 

### GET /categories
- General: returns a list of categories and success value.
- Sample: curl http://127.0.0.1:5000/categories
```
{
    "categories": {
        "1": "Science",
        "2": "Art",
        "3": "Geography",
        "4": "History",
        "5": "Entertainment",
        "6": "Sports"
    },
    "success": true
}
```

### GET /questions:
- General: returns a list of questions paginated in group of 10, success value, list of categories, total_questions which will frontend code depend on to make pagination and current category value.
- Sample: curl http://127.0.0.1:5000/questions
```
  "categories": {
      "1": "Science",
      "2": "Art",
      "3": "Geography",
      "4": "History",
      "5": "Entertainment",
      "6": "Sports"
  },
  "currentCategory": null,
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
          "answer": "Edward Scissorhands",
          "category": 5,
          "difficulty": 3,
          "id": 6,
          "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
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
  "total_questions": 19
```
### Delete /questions/<int:question_id>
- General: delete a question using its id, if deletion succeeded the returned value will be success, deleted which points to the id of deleted question.
- Sample: curl -X DELETE http://127.0.0.1:5000/questions/2
```
{
    "deleted": "2",
    "success": true
}
```

### POST /questions
- General: create a new question, data that need to be provided at post request are (question, answer, difficullty, category), if succeeded the return value will be success value and the id of created_question
- Sample: curl http://127.0.0.1:5000/questions -X POST -H "Content-Type: application/json" -d '{"question":"Who won the last ballon d'or?", "answer":"Messi", "difficulty":"1", category: "6"}'
```
{
  "success": true,
  "created_question": 20
}
```

### POST /questions/search
- General: search for a question using any keyword without depending on case sensetive, the result will be success value, list of all questions that has search keyword, total questons that have search keyword and current category.
- Sample: curl http://127.0.0.1:5000/questions/search -X POST -H "Content-Type: application/json" -d '{"searchTerm": "go"}'
```
{
    "current_category": null,
    "questions": [
        {
            "answer": "One",
            "category": 2,
            "difficulty": 4,
            "id": 18,
            "question": "How many paintings did Van Gogh sell in his lifetime?"
        }
    ],
    "success": true,
    "total_questions": 1
}
```

### GET /categories/<int:category_id>/questions:
- General: get all questions depending on the category id, the result will be success value, list of questions depending on the value of category, total questions and the current category will be the id of category
- Sample: curl http://127.0.0.1:5000/categories/2/questions
```
{
    "current_category": 2,
    "questions": [
        {
            "answer": "Escher",
            "category": 2,
            "difficulty": 1,
            "id": 16,
            "question": "Which Dutch graphic artist–initials M C was a creator of optical illusions?"
        },
        {
            "answer": "Mona Lisa",
            "category": 2,
            "difficulty": 3,
            "id": 17,
            "question": "La Giaconda is better known as what?"
        },
        {
            "answer": "One",
            "category": 2,
            "difficulty": 4,
            "id": 18,
            "question": "How many paintings did Van Gogh sell in his lifetime?"
        },
        {
            "answer": "Jackson Pollock",
            "category": 2,
            "difficulty": 2,
            "id": 19,
            "question": "Which American artist was a pioneer of Abstract Expressionism, and a leading exponent of action painting?"
        },
        {
            "answer": "Ahmed",
            "category": 2,
            "difficulty": 2,
            "id": 24,
            "question": "What is your name"
        }
    ],
    "success": true,
    "total_questions": 5
}
```
