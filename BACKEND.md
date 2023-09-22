## Description

This repository contains the implementation of a microservice for managing institutions and institution types. It utilizes the NestJS framework for building efficient and scalable server-side applications. This microservice also provides endpoints for creating, fetching, updating, and deleting institution data and institution type data.

## Running Docker Container
You can directly run the Docker container using the command below without actually needing to install dependencies:

```bash
$ npm run dev
```
**Note:** It may take a few minutes for the container to start, depending on the network.

## Installation
Or you can directly download dependency using the below command
```bash
$ npm install
```

<h1>Setting up MongoDB Database Connection</h1>

  <h2>Prerequisites</h2>
    <p>Before you can run the application, you need to set up few things to get started.</p>
    <h3>Step 1: Setting up <code>.env</code> File</h3>
    Create a <code>.env</code> file in the root directory of your project if it doesn't already exist.
    Inside the <code>.env</code> file, add the following key-value pair to configure the MongoDB connection:
    <pre><code>MONGO_URI= //Your mongodb url, example :  mongodb://127.0.0.1:27017/backend</code></pre>
    <p>You can also customize the <code>MONGO_URL</code> value to match your specific MongoDB server configuration or use a different database URL as needed.</p>
    <h4>Example:</h4>
    <pre><code>MONGO_URL=mongodb://username:password@your-mongodb-server:27017/your-database</code></pre>
    <p>Make sure to replace <code>username</code>, <code>password</code>, <code>your-mongodb-server</code>, and <code>your-database</code> with your actual MongoDB credentials and server information.</p>
    <h2>Usage</h2>
    <p>With the <code>.env</code> file properly configured, your application should now be able to connect to the MongoDB database using the specified URL.</p>
    <p>You can use this MongoDB connection URL in your application to establish a connection to the database and perform CRUD operations.</p>





## Running the app
You can run your server using below commands
```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

<code>Server will start listening at </code>

```bash
http://localhost:8080/
```

## Test
you can test your application using the below commands
```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```

## Create Institution

<html>
<body>

  <ul>
    <li><strong>Endpoint:</strong> <code>POST  /institutions</code></li>
    <li><strong>Description:</strong> Create a new institution with provided data.</li>
    <li><strong>Request Body:</strong> <code>createInstitution</code>: A JSON object containing institution data.</li>
    <li><strong>Responses:</strong>
      <ul>
        <li>201 Created: Institution created successfully.</li>
        <li>400 Bad Request: Invalid request body.</li>
      </ul>
    </li>
  </ul>

  <h3>Fetch All Institutions</h3>

  <ul>
    <li><strong>Endpoint:</strong> <code>GET  /institutions</code></li>
    <li><strong>Description:</strong> Fetch all existing institutions.</li>
    <li><strong>Responses:</strong>
      <ul>
        <li>200 OK: Institutions fetched successfully.</li>
        <li>404 Not Found: No institutions data found.</li>
      </ul>
    </li>
  </ul>

  <h3>Fetch Institution by ID</h3>

  <ul>
    <li><strong>Endpoint:</strong> <code>GET  /institutions/:id</code></li>
    <li><strong>Description:</strong> Fetch an institution by its ID.</li>
    <li><strong>Path Parameters:</strong>
      <ul>
        <li><code>id</code>: The ID of the institution to fetch.</li>
      </ul>
    </li>
    <li><strong>Responses:</strong>
      <ul>
        <li>200 OK: Institution fetched successfully.</li>
        <li>400 Bad Request: Invalid institution ID.</li>
        <li>404 Not Found: No institute found with the given ID.</li>
      </ul>
    </li>
  </ul>

  <h3>Update Institution</h3>

  <ul>
    <li><strong>Endpoint:</strong> <code>PUT  /institutions</code></li>
    <li><strong>Description:</strong> Update an existing institution.</li>
    <li><strong>Request Body:</strong> <code>updateInstitution</code>: A JSON object containing institution id and updated institution data.</li>
    <li><strong>Responses:</strong>
      <ul>
        <li>200 OK: Institution updated successfully.</li>
        <li>400 Bad Request: Bad request.</li>
        <li>404 Not Found: No institute found.</li>
      </ul>
    </li>
  </ul>

  <h3>Delete Institution</h3>

  <ul>
    <li><strong>Endpoint:</strong> <code>DELETE  /institutions/:id</code></li>
    <li><strong>Description:</strong> Delete an institution by its ID.</li>
    <li><strong>Path Parameters:</strong>
      <ul>
        <li><code>id</code>: The ID of the institution to delete.</li>
      </ul>
    </li>
    <li><strong>Responses:</strong>
      <ul>
        <li>200 OK: Institution deleted successfully.</li>
        <li>400 Bad Request: Invalid institution ID.</li>
        <li>404 Not Found: Institution not found.</li>
      </ul>
    </li>
  </ul>
  <h1>Institution Type API</h1>

  <h2>Endpoints</h2>

  <h3>Create Institution Type</h3>

  <ul>
    <li><strong>Endpoint:</strong> <code>POST  /types</code></li>
    <li><strong>Description:</strong> Create a new institution type with provided data.</li>
    <li><strong>Request Body:</strong> <code>createInstitutionType</code>: A JSON object containing institution type
      data.</li>
    <li><strong>Responses:</strong>
      <ul>
        <li>201 Created: Institution type created successfully.</li>
        <li>400 Bad Request: Bad request.</li>
        <li>500 Internal Server Error: Invalid request body.</li>
      </ul>
    </li>
  </ul>

  <h3>Fetch All Institution Types</h3>

  <ul>
    <li><strong>Endpoint:</strong> <code>GET  /types</code></li>
    <li><strong>Description:</strong> Fetch all existing institution types.</li>
    <li><strong>Responses:</strong>
      <ul>
        <li>200 OK: Institution types fetched successfully.</li>
        <li>404 Not Found: No institution types found.</li>
      </ul>
    </li>
  </ul>

  <h3>Fetch Institution Type by ID</h3>

  <ul>
    <li><strong>Endpoint:</strong> <code>GET  /types/:id</code></li>
    <li><strong>Description:</strong> Fetch an institution type by its ID.</li>
    <li><strong>Path Parameters:</strong>
      <ul>
        <li><code>id</code>: The ID of the institution type to fetch.</li>
      </ul>
    </li>
    <li><strong>Responses:</strong>
      <ul>
        <li>200 OK: Institution type fetched successfully.</li>
        <li>400 Bad Request: Invalid institution type ID.</li>
        <li>404 Not Found: No institution type found.</li>
      </ul>
    </li>
  </ul>

  <h3>Update Institution Type</h3>

  <ul>
    <li><strong>Endpoint:</strong> <code>PUT  /types</code></li>
    <li><strong>Description:</strong> Update an existing institution type.</li>
    <li><strong>Request Body:</strong> <code>updateInstitutionType</code>: A JSON object containing institution id and updated institution-type data.</li>
    <li><strong>Responses:</strong>
      <ul>
        <li>200 OK: Institution type updated successfully.</li>
        <li>400 Bad Request: Bad request.</li>
        <li>404 Not Found: No institution type found.</li>
      </ul>
    </li>
  </ul>

  <h3>Delete Institution Type</h3>

  <ul>
    <li><strong>Endpoint:</strong> <code>DELETE  /types/:id</code></li>
    <li><strong>Description:</strong> Delete an institution type by its ID.</li>
    <li><strong>Path Parameters:</strong>
      <ul>
        <li><code>id</code>: The ID of the institution type to delete.</li>
      </ul>
    </li>
    <li><strong>Responses:</strong>
      <ul>
        <li>200 OK: Institution type deleted successfully.</li>
        <li>400 Bad Request: Invalid institution type ID.</li>
        <li>404 Not Found: Institution type not found.</li>
      </ul>
    </li>
  </ul>

  <h2>Swagger Documentation (OpenAPI Contract)</h2>

  <p>The API documentation is generated using Swagger. Access the Swagger UI at <a
      href="/api">/api</a> to explore the available endpoints, their request and response structures, and to
    interact with the API directly through the documentation interface.</p>

  <h2>Technologies Used</h2>

  <ul>
    <li><a href="https://nestjs.com/">NestJS</a>: A progressive Node.js framework for building efficient, reliable,
      and scalable server-side applications.</li>
    <li><a href="https://www.mongodb.com/">MongoDB</a>: A popular NoSQL database.</li>
    <li><a href="https://swagger.io/">Swagger</a>: A tool for documenting and testing APIs.</li>
    <li><a href="https://expressjs.com/">Express</a>: A web application framework for Node.js.</li>
  </ul>

</body>
  
</html>
