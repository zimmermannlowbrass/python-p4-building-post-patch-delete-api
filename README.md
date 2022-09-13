# Building a POST/PATCH/DELETE API

## Learning Goals

- Build an API to handle POST, PATCH, and DELETE requests.

***

## Key Vocab

- **Application Programming Interface (API)**: a software application that
  allows two or more software applications to communicate with one another.
  Can be standalone or incorporated into a larger product.
- **HTTP Request Method**: assets of HTTP requests that tell the server which
  actions the client is attempting to perform on the located resource.
- **`GET`**: the most common HTTP request method. Signifies that the client is
  attempting to view the located resource.
- **`POST`**: the second most common HTTP request method. Signifies that the
  client is attempting to submit a form to create a new resource.
- **`PATCH`**: an HTTP request method that signifies that the client is attempting
  to update a resource with new information.
- **`DELETE`**: an HTTP request method that signifies that the client is
  attempting to delete a resource.

***

## Introduction

So far, we've seen how to set up an API with Flask to allow frontend
applications to access data from a database in a JSON format. For many
applications, just being able to access/read data isn't enough — what kind of
app would Twitter be if you couldn't write posts? What would Instagram be if you
couldn't like photos? How embarrassing would Facebook be if you couldn't go back
and delete those regrettable high school photos?

All of those applications, and most web apps, can be broadly labeled as CRUD
applications — they allow users to **C**reate, **R**ead, **U**pdate, and
**D**elete information.

We've seen a few ways to Read data in an API. We've also already seen how to
Create/Update/Delete records from a database using SQLAlchemy. All that's
left is to connect what we know from SQLAlchemy with some new techniques for
establishing routes and accessing data in our Flask application.

***

## Setup

We'll continue working on the game review application from the previous lessons.
To get set up, run:

```console
$ pipenv install && pipenv shell
$ cd app
$ flask db upgrade
$ python seed.py
```

You can view the models in the `app/models.py` module, and the migrations in the
`app/migrations/versions` directory. Here's what the relationships will look
like in our ERD:

![Game Reviews ERD](https://curriculum-content.s3.amazonaws.com/phase-3/active-record-associations-many-to-many/games-reviews-users-erd.png)

Then, run the server with Flask:

```console
$ flask run
```

With that set up, let's start working on some CRUD!

***

## Handling DELETE Requests

Let's start with the simplest action: the DELETE request. Imagine we're building
a new feature in our frontend React application. Our users want some way to
delete their reviews, in case they change their minds. In React, our component
for handling this delete action might look something like this:

```js
function ReviewItem({ review, onDeleteReview }) {
  function handleDeleteClick() {
    fetch(`http://localhost:9292/reviews/${review.id}`, {
      method: "DELETE",
    })
      .then((r) => r.json())
      .then((deletedReview) => onDeleteReview(deletedReview));
  }

  return (
    <div>
      <p>Score: {review.score}</p>
      <p>{review.comment}</p>
      <button onClick={handleDeleteClick}>Delete Review</button>
    </div>
  );
}
```

So, it looks like our server needs to handle a few new things:

- Handle requests with the `DELETE` HTTP verb to `/reviews/:id`.
- Find the review to delete using the ID.
- Delete the review from the database.
- Send a response with the deleted review as JSON to confirm that it was deleted
  successfully, so the frontend can show the successful deletion to the user.

Let's take things one step at a time. First, we'll need to handle requests by
adding a new route in the controller. We can write out a route for a DELETE
request just like we would for a GET request, just by changing the method:

***

## Conclusion

.

***

## Solution Code

You're at the point now where you can create a JSON API that handles all four
CRUD actions: Create, Read, Update, and Delete. With just these four actions,
you can build an API for almost any application you can think of!

***

## Resources

- [Flask - Pallets](https://flask.palletsprojects.com/en/2.2.x/)
- [POST - Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST)
- [PATCH - Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH)
- [DELETE - Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE)
- [flask.json.jsonify Example Code - Full Stack Python](https://www.fullstackpython.com/flask-json-jsonify-examples.html)
- [SQLAlchemy-serializer - PyPI](https://pypi.org/project/SQLAlchemy-serializer/)
