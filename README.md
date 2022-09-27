# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.
# topics-ui

## Context

Our grand Q2 revenue-boosting plan is to build a shiny new dashboard 
(cloud-hosted, of course) to aggregate curated content from one of our
internal APIs. This content is divided into topics. For a demo to the 
president, you've been asked to provide an implementation of a single 
topic page.

### Task

Create an application consisting of

1. A single page app (SPA) UI client that displays a table with content for the 
   topic *'Aggregation'*. The table should display, for each topic member (i.e. 
   'row'), 
   the following fields:
   
  * The annotation title
  * The document title
  * The document jurisdiction
  * The document tags
  * The document html content of the html node with id `html-node-id`
      
2. A UI server that serves the SPA UI resources, and an API for the SPA 
   UI for topic data. This means it must interact with the (supplied) internal 
   API to retrieve content for these endpoints. 

See [the Internal API Server Reference section](#internal-api-server-reference) 
section for how to run the server, and its endpoints and schemata. We would
advise doing this first, so you can get an idea of what functionality is 
available to you.

Additionally, please also document any important design decisions that you've made in a 
markdown file. A skeleton `DESIGN.md` file has been provided.

#### Constraints and Assumptions

In producing your solution, we expect you to carefully consider the following
constraints and assumptions: 

* In our hypothetical cloud-hosting setup, the internal API server can only be 
  accessed by services on the same 'network'. For this task, this means the UI 
  browser client is unable to access the internal API server. 
  So interactions with the internal API server must go through your server.
* For a given topic, multiple members may reference the same `document-uuid`
* Retrieving certain documents from the internal API can be very slow (20 
  seconds or worse), and the more concurrent requests for the same document, the 
  slower the API gets. At 5 concurrent requests for a document, requests for that 
  document will start failing
* Documents are _immutable_ and uniquely identified by `document-uuid`: 
  for a given `document-uuid`, the same `html` response will always be returned
* Topics are _mutable_: Content may be added or removed from topics over time. 
  In other words, the response of `GET /annotations?topic=<topic>` may vary.
  Although it might seem that the response is always the same, this cannot be
  assumed.
* You may use whatever libraries you wish.

## Internal API Server Reference

The internal API HTTP server can be started on port `8080` by running

``` sh
java -jar internal-api.jar
```

from the project root. Note that this requires _java 11_ to be available 
on your machine.

For development, the slowness of the documents endpoint of the internal api 
described in [the constraints and assumptions section](#constraints-and-assumptions) 
may be inconvenient. The slowness can be disabled by running the server like so:

``` sh
INTERNAL_API_SLOW_RESPONSES=false java -jar internal-api.jar
```

Note that your solution will be judged using the _slow_ server.

#### Endpoints and schemata
The available endpoints, their descriptions, and schemata can be viewed at
[](http://localhost:8080) when the server is running. Additionally, below are 
some example requests and responses:

##### `/api/annotations`
* [request](examples/annotations/request.json)
* [response](examples/annotations/response.json)

##### `/api/documents`
* [request](examples/documents/request.json)
* [response](examples/documents/response.json)

##### `/api/extract-html-node`
* [request](examples/extract-html-node/request.json)
* [response](examples/extract-html-node/response.json)

## What we're looking for
* The app should be relatively performant, and ideally responsive
* We'd like to understand why you've made the design decisions that you have, 
  and the tradeoffs involved. In particular, what constraints and assumptions
  directed your choices? For example, if you chose to execute certain http calls
  in parallel or in serial, then we'd like to hear why. We'd prefer a partial
  solution with a comprehensive discussion of what you'd do and why/why not,
  over a complete solution with scant discussion
* If you didn't end up implementing everything you wanted to (which is fine,
  there's always more to do!), we'd be interested to know what those leftover
  parts are, and how you'd implement them. For example, if you
  ended up rendering the entire document html for each topic member rather than
  extracting the individual node, we'd like to hear how you'd go about rendering
  the single node
* If you find something unclear, don't be afraid to ask. Part of our day-to-day 
  involves interacting with stakeholders to clarify requirements, so 
  inquisitiveness is a virtue.

## Submission checklist
* Instructions for running the project (including any dependency prerequisites)
* Your UI and server source code
* Your design decisions markdown file