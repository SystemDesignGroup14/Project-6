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
