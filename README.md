# Getting Started
## What is a CustomInstanceStore?

By default, the only way to use long-running workflows (i.e. waiting for email approval) in Windows Workflow Foundation is to connect it to a SQL Server so it can save the state of the instances. Want it to save the workflow state to an XML file? To a MySQL database? That is not so easy.

CustomInstanceStore is an abstraction over InstanceStore that makes it easy to create persistence providers for Windows Workflow Foundation.


## What types of providers are included in this library?

- XML
- MemoryCache (useful for testing)
- Neo4j (separate library)


## Installation

In Nuget:

    package-install CustomInstanceStore

	package-install CustomInstanceStore.Neo4j


## What versions of WF does this support?

It should work on both 4.0 and 4.5 versions of Workflow Foundation.


## Is there a demo application?

Check out the [GraphDocs project](https://github.com/mattmeisinger/graph-docs). Please note that it requires Neo4j to be running locally.


## How can I contribute?

Browse the open issues, fork the repo, and submit a pull request!