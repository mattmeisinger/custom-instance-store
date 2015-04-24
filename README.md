# Getting Started
## What is a CustomInstanceStore?

CustomInstanceStore is an abstraction over InstanceStore that makes it easy to create persistence providers for Windows Workflow Foundation.

By default, the only way to use long-running workflows in Windows Workflow Foundation is to connect it to a SQL Server. For instance, in an email approval workflow, it will save the state of the workflow instance to SQL Server, then load it back when the approval bookmark is triggered in the workflow. 

Want it to save the workflow state to an XML file? To a MySQL database? That is not so easy.

CustomInstanceStore solves this.


## Installation

NuGet:

    package-install CustomInstanceStore


## Example Usage

To implement the abstract class `CustomInstanceStoreBase`, just override the `Save()` and `Load()` methods. They data key is a combination of a Store ID and an Instance ID.

Here is an example implementation that simply saves the instance data to the filesystem:

    public class XMLFileInstanceStore : CustomInstanceStore.CustomInstanceStoreBase
    {
        string _basePath;

        /// <summary>
        /// Create store that persists instance state to XML file on the filesystem with a path of:
        ///    {basePath}\{storeId}\{instance}
        /// </summary>
        public XMLFileInstanceStore(string basePath, Guid storeId)
            : base(storeId)
        {
            this._basePath = basePath;
        }

        public override void Save(Guid instanceId, Guid storeId, XmlDocument doc)
        {
            var filename = getFilePath(instanceId, storeId);
            var directoryName = new FileInfo(filename).Directory.FullName;
            Directory.CreateDirectory(directoryName);
            doc.Save(filename);
        }
        public override XmlDocument Load(Guid instanceId, Guid storeId)
        {
            var filename = getFilePath(instanceId, storeId);
            var xmlDoc = new XmlDocument();
            xmlDoc.Load(filename);
            return xmlDoc;
        }
        private string getFilePath(Guid instanceId, Guid storeId)
        {
            return Path.Combine(_basePath, storeId.ToString(), instanceId.ToString() + ".xml");
        }
    }

Then just use your new custom InstanceStore class instead of `SqlWorkflowInstanceStore` in your application.

    var app = new WorkflowApplication(new MyActivityDefinition());
    var storeId = new Guid("0bfcc3a5-3c77-421b-b575-73533563a1f3"); // May be the same for all workflows in your application
    app.InstanceStore = new XMLFileInstanceStore(@"c:\MyApp\WorkflowData", storeId);

See [this MSDN article](https://msdn.microsoft.com/en-us/library/ee342461.aspx) for general information on using persistence with Workflow Foundation.


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