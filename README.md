# Getting Started
## What is a CustomInstanceStore?

CustomInstanceStore is an abstraction over InstanceStore that makes it easy to create persistence providers for Windows Workflow Foundation.

By default, the only way to use long-running workflows in Windows Workflow Foundation is to connect it to a SQL Server. For instance, in an email approval workflow, it will save the state of the workflow instance to SQL Server, then load it back when the approval bookmark is triggered in the workflow. 

Want it to save the workflow state to an XML file? To a MySQL database? That is not so easy.

CustomInstanceStore solves this.


## Installation

NuGet:

    package-install CustomInstanceStore


## What types of providers are included in this library?

- XML
- MemoryCache (useful for testing)


## Other libraries

- [Neo4j](https://github.com/mattmeisinger/custom-instance-store-neo4j)


## What versions of WF does this support?

It should work on both 4.0 and 4.5 versions of Workflow Foundation.


## Is there a demo application?

Check out the [GraphDocs project](https://github.com/mattmeisinger/graph-docs). Please note that it requires Neo4j to be running locally.


## How can I contribute?

Browse the open issues, fork the repo, and submit a pull request!