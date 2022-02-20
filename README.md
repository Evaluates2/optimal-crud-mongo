# mongo-greatest-CRUD-in-all-the-land

## Goals of This Project

This is meant to be the most __efficient__, __scalable__, and __fast__ production-ready serverless REST API backend which provides CRUD operations for a MongoDB collection!!

It is meant to be optimized for:

### ⚡ Execution Speed
Written in Rust with most optimized compiler settings and zero "virtual machine bloat" that exists with languages such as python, node, or go.

### 💵 Scalability and Cost
This project packages the Rust server as AWS Lambda functions where you pay for _only_ the milliseconds or server time when your code is executing. As opposed to other architectures that involve running a server 24/7, serverless functions do not incur a cost when the system is not in use, and there is no more headache of configuring load balancing correctly.

### Large Amounts of Data

- Rather than a "get all" method that, this project provides a "get single" and "get paginated list" which uses cursor pagination 

- Includes a "move data to lake" to lake function which offloads old documents from the mongo "application database" over to a mongo "data lake" for long-term storage and analytics purposes.


## Usage

This is a Rust project. Please first install `cargo` and `serverless`.

Running Tests:
```
cargo test
```

Running Locally (Note - not working for me...)
```
sls invoke local -f function_name
```

Deploying:
```
sls deploy
```

Note: You will need to first configure your aws cli before deploying:
```
aws configure
```

## Customize For Your Data
Modify constants defined in .env to your liking.

You may also want to update your resource name.

This must be done manually at the current time...

Do a project find-and-replace for these things:
- cat -> my_new_resource_name
- Cat -> MyNewResourceName
- CAT -> MY_NEW_RESOURCE_NAME

You can also add / remove fields on the `Cat` struct defined in: `./src/cat/cat.model.rs`


## REST Naming Conventions

We usually recommend using the plural form of the resource for which you are building this CRUD API.

For example, if each document in your collection represents a "cat", then the url endpoint should be "cats".


#### CREATE - Inserting a New Cat
POST to: `https://your_url/cats` with cat details


#### READ - Getting An Individual Cat
GET: `https://your_url/cats/123123123` where "123123123" is the document `_id` for the cat object to get.


#### READ - Getting Cats
GET: `https://your_url/cats/123123123` where "123123123" is the document `_id` for the cursor document. Returns up to 10 cats after the cursor doc.

 
#### UPDATE - Updating A Cat
POST: `https://your_url/cats/123123123` where "123123123" is the document `_id` for the document to update. Takes an object of fields to update and leaves existing fields on the document.


#### DELETE - Deleting A Cat
DELETE: `https://your_url/cats/123123123` where "123123123" is the document `_id` for the document to delete.


#### LAKE - Moving Old Cats To Data Lake
POST: `https://your_url/cats/move-stale` Copies docs older than X days (default 30) to mongo data lake and deletes them from the db collection.



## Benchmarks

// TODO - get some real data for these functions!!


## Contributing

Feel free to open issues / PRs if you have ideas on how to improve this project
