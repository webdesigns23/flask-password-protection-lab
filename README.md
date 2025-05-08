# Password Protection Lab

## Introduction

We're going to make a Flask app that covers a simple authentication flow: users
can create accounts, log in, and log out.

## Tools & Resources

- [GitHub Repo](https://github.com/learn-co-curriculum/flask-password-protection-lab)
- [Flask-Bcrypt](https://flask-bcrypt.readthedocs.io/en/1.0.1/)

## Set Up

There is some starter code in place for a Flask API backend and a React frontend.
To get set up, run:

```console
$ pipenv install && pipenv shell
$ npm install --prefix client
$ cd server
$ flask db upgrade
```

You can work on this lab by running the tests with `pytest -x`. It will also be
helpful to see what's happening during the request/response cycle by running the
app in the browser. You can run the Flask server with:

```console
$ python app.py
```

And you can run React in another terminal with:

```console
$ npm start --prefix client
```

You don't have to make any changes to the React code to get this lab working.

## Instructions

### Task 1: Define the Problem

Our app has three pages:

1. A signup page, where the user enters their username, password, and password
   confirmation.
2. A login page, where the user submits their username and password and are then
   logged in.
3. A user homepage, which says, "Welcome, ${username}!"

Users should not be able to log in if they enter an incorrect password.

> **Note: we're not covering password validations in this lab, so don't worry
> about those. Password validation is hard to get right anyway — it's
> surprisingly easy to produce rules that decrease password security rather than
> enhance it.**

### Task 2: Determine the Design

We need to implement a way for users to sign up, log in, and log out with secure
passwords.

To complete the lab and get the tests passing, you will need to:

- Create a `Signup` resource with a `post()` method that responds to a
  `POST /signup` request. It should: create a new user; save their hashed
  password in the database; save the user's ID in the session object; and return
  the user object in the JSON response.

- Add a `get()` method to your `CheckSession` resource that responds to a
  `GET /check_session` request. If the user is authenticated, return the user
  object in the JSON response. Otherwise, return an empty response with a 204
  status code.

- Create a `Login` resource with a `post()` method for logging in that
  responds to a `POST /login` request and returns the user as JSON.
  
- Create a `Logout` resource with a `delete()` method for logging out
  that responds to a `DELETE /logout` request.

#### Note on Configuration

Take note of the new `config.py` file in the `server/` directory. As our app is
getting more and more complex, setting up the a config file can help clean up our
code a bit.

In each of our applications so far, `app.py` needed to import from `models.py`
in order to initialize the database's connection to the app. That's still the
case here, but we also find ourselves with the need to import an instantiated
`Bcrypt` from `app.py` into `models.py`! This creates a _circular import_, where
objects in two separate files are dependent upon one another to function.

To avoid this, you can often refactor your objects to avoid unnecessary
dependencies (we're all guilty of this!), you can refactor your code into one
large file, or you can move some of your imports and configurations into a third
file. That's what we did here- check out `config.py` and you'll notice a lot of
familiar code. We took the imports and configurations from `app.py` and
`models.py` and put them together to avoid circular imports. These are then
imported by `app.py` and `models.py` when they're ready to be used.

### Task 3: Develop, Test, and Refine the Code

#### Step 1: Create Signup Endpoint

Create `POST /signup` endpoint. Implement the following:
- Create a new user. 
- Save user to db with their hashed password using bcrypt.
- Log the user in with sessions.
- Return the user object.

Test your logic with `pytest` and commit your code.

#### Step 2: Create Check Session Endpoint

Create `GET /check_session` endpoint. Implement the following:
- If the user is authenticated, return the user object in the JSON response. 
- Else, return an empty response with a 204 status code.

Test your logic with `pytest` and commit your code.

#### Step 3: Create Login Endpoint

Create `POST /login` endpoint. Implement the following:
- Log the user in with sessions.
- Returns the user as JSON.

Test your logic with `pytest` and commit your code.

#### Step 4: Create Logout Endpoint
  
Create `DELETE /logout` endpoint. Implement the following:
- Log the user out with sessions.

Test your logic with `pytest` and commit your code.

#### Step 5: Commit and Push Git History

Once all tests are passing, `git commit` (if needed) and `git push` your final code
to GitHub:

```bash
git add .
git commit -m "final solution"
git push
```

If you created a separate feature branch, remember to open a PR on main and merge.

### Task 4: Document and Maintain

Best Practice documentation steps:
* Add comments to the code to explain purpose and logic, clarifying intent and 
functionality of your code to other developers.
* Update README text to reflect the functionality of the application following 
https://makeareadme.com. 
  * Add screenshot of completed work included in Markdown in README.
* Delete any stale branches on GitHub
* Remove unnecessary/commented out code
* If needed, update git ignore to remove sensitive data

## Submit your solution

CodeGrade will use the same test suite as the test suite included.

Once all tests are passing, commit and push your work using `git` to submit to 
CodeGrade through Canvas.
