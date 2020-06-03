# Express.js

_Node_ is a runtime environment for running JavaScript.

_HTTP_ is a _protocol_ \(a set of rules\) that talks about sending HTML \(and now other kinds of data\) back and forth across the network.

### Node & the Network

We can use node to run javascript in response to a newtork request.

### Node & Express

Specifically, we'll use a web framework called Express in order to create a dynamic web server that interacts with a database.

By the end of this unit, we'll have designed a 3-tier application similar to this.

![3-Tier Express Application](../.gitbook/assets/3-tier-application.jpg)

## File Server vs. Application Server

We'll be dealing with 2 kinds of server for doing HTTP:

1. File Server - depending on a request to the computer, sends back a specific file on the filesystem.
   * Simple logic - if file exists, send back. Else, send back an error.
   * Don't have to write it ourselves \(has already been written before\) - See here if you want to know how one might be written in node:[https://developer.mozilla.org/en-US/docs/Learn/Server-side/Node\_server\_without\_framework](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Node_server_without_framework)
2. Application Server
   * _dynamically_ responds to requests and serves back HTML \(or other\) based on the request
   * Uses express.js framework to handle shuttling requests to our js code.
   * the js code we write inside the express files _is_ the logic that determines what gets sent back in the response.

