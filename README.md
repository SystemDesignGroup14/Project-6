# Group 12 Scrum Team
## Product Owner
Abheek Ranjan Das
## Scrum Master
Aravinda Reddy Gangalakunta 
## Developers
- Gokul Reddy Devarapalli
- Ramgopal Hyndav Bollepalli
- Danny Bylla



# Project 6: Full Stack Photo Sharing App

## Introduction

This project enhances our photo sharing application by integrating MongoDB for data persistence, allowing dynamic content management. We've encapsulated the environment setup using Docker Compose for ease of development and deployment.

## Setup

### Requirements

- Docker and Docker Compose optional
- Node.js (for local development)

### Getting Started

1. **Docker Compose Setup**: To spin up the MongoDB database , simply run:

```bash
docker-compose up -d
```

This command starts all required services as defined in our `docker-compose.yml` file, including the MongoDB instance and express.



You should see containers for both the MongoDB database and express.


## API Overview

With the integration of MongoDB, our app's API now directly interacts with a live database, enhancing data management and scalability. Here's a brief overview:

- **User List (`/user/list`)**: Fetches a list of all users from the MongoDB `User` collection, displaying essential details like name and occupation.

- **User Details (`/user/:id`)**: Retrieves detailed information about a specific user by their ID, including their photos and comments.

- **Photos of User (`/photosOfUser/:id`)**: Returns all photos uploaded by a specific user, along with comments on each photo, leveraging MongoDB for data retrieval.

### Example: Fetching User Details

```javascript
app.get("/user/:id", async (request, response) => {
  try {
    const user = await User.findById(request.params.id);
    if (!user) {
      return response.status(404).send("User not found");
    }
    response.json(user);
  } catch (error) {
    response.status(500).send("Internal Server Error");
  }
});
```

This endpoint demonstrates how we interact with MongoDB to fetch and return user details, ensuring a dynamic and responsive application experience.


## Problem 1: Convert the web server to use the database

### Description

In this problem, we need to convert the web server of our photo sharing application to utilize MongoDB for data storage and retrieval. Currently, the application's model fetching routes use "magic models" rather than a database. Our task is to update these routes to interact with MongoDB and ensure that there are no accesses to models in the code.

### Requirements

1. Modify the existing routes to fetch data from MongoDB instead of using magic models.
2. Implement four specific API endpoints:
    - `/test`: Return schema info and object counts of the database for testing purposes.
    - `/user/list`: Return a list of users' models appropriate for the navigation sidebar list.
    - `/user/:id`: Return detailed information of a user specified by their ID.
    - `/photosOfUser/:id`: Return photos of the user with the specified ID, along with comments on each photo.
3. Ensure that the GET requests return the required information for the UI without accessing models directly.
4. Handle errors and edge cases appropriately, including invalid requests and database errors.
5. Do not alter the database schema.

### Notes

- The MongoDB system returns models from objects stored in the database, while the request should return the data models needed by the Photo App views. Special care must be taken to align these models properly.
- Utilize processing techniques to assemble the necessary model data for the front end.
- Avoid directly modifying Mongoose models to match front end requirements. Instead, create copies of the Mongoose model objects.



