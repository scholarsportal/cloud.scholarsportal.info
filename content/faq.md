+++
title = "FAQ"
+++

## 1. What technology does the OLRC Storage Cloud run on?

The OLRC Storage Cloud is an implementation of the Swift storage service of the OpenStack cloud services framework. OpenStack is the primary open source initiative to build cloud based services, including services for cloud-based virtual computing, cloud-based storage, and cloud based networking.

## 2. How is Swift storage different from standard server storage? 

Swift uses large farms of inexpensive disks connected together over the network and exposes these to end-users through an HTTP REST API, the Swift API. Swift accepts API calls from HTTP clients (e.g. browsers, web-based applications, command line tools such as curl, and desktop applications) to store, retrieve, delete or update files in the cloud. Standard server storage is directly attached to a server and is accessed via operating system calls on that server or from desktop clients via network shares assigned by server administrators.

## 3. When would I use the OLRC Storage Cloud based on Swift rather than standard server storage that my IT office might be able to provide for me? 

Several factors go into making that decision. Cost is one such factor, with cloud storage often being cheaper than server storage by a factor of more than 10x. Redundancy and data distribution is another factor, with a typical Swift configuration creating and managing from 3 to 5 replicas of any file stored in the cloud. Speed of access is a third consideration, with Swift storage designed to support store-once, read often use cases rather than applications where files are being constantly edited.

## 4. What would some typical use cases be for the OLRC Storage Cloud?

The classic use case for OLRC Cloud Storage is long-term maintenance of large volumes of digital objects of varying sizes which change infrequently (or not at all) over time, combined with requirements for broad geographic distribution of multiple replicas of each object. This is a description of many archival storage use cases typical of digital libraries, including managing large collections of text and image objects, digital video, static GIS files, research data files such as scientific instrument readings, and web archive files. It is also a great place to park large volumes of data that you might eventually ingest into a database or search index but need to keep around for a limited time while you work your way through processing the files. Finally, it is also a good place to keep a backup copy of active data you use outside the cloud if you don’t have adequate tape backup or anticipate the need to access individual files for validation and authenticity checking against the active copies.

## 5. What would be a very bad use of the OLRC Storage Cloud?

It would not make any sense to hold in the cloud a set of files that make up a relational database or search index, if the database or index were actively in use, including updates and large volumes of retrieval requests from a large number of clients. It would not make sense to hold in the cloud files that are being edited frequently, with multiple sub-second writes being a performance expectation.

## 6. What tools can I use to upload files to the OLRC Storage Cloud.

There are several tools that you can use to load data into the OLRC Storage Cloud. The storage protocol used by the OLRC Storage Cloud is is an HTTP REST API called “Swift”. Therefore, any Swift compatible client that supports OpenStack Keystone authentication should work. 

## 7. Where can I find a Swift compatible client that supports OpenStack Keystone authentication?

The canonical Swift client Python library includes command line tools that can be used to load and authenticate to OpenStack using Keystone authentication. Read more here:

https://swiftstack.com/docs/integration/python-swiftclient.html

## 8. What authentication credentials do I need to use to access the OLRC Storage Cloud?

Each subscribing institution will have an administrator who will be able to create local accounts to access the OLRC Cloud. Credentials include:

*TENANT_NAME
*USERNAME
*PASSWORD
*REGION_NAME [optional]

These are passed to OpenStack with each call to Swift, via HTTP headers. Normally, the client software you use handles this interaction, and values for each of these login credentials are stored by the software so you only need to enter then once. For example, when using the Python swift-client tool (see A7), you can store your credentials in a shell script for export as environment variables, which swift-client will access automatically:

*export OS_TENANT_NAME=xxxxxxx
*export OS_USERNAME=xxxxxxx
*export OS_PASSWORD=xxxxxxx
*export OS_AUTH_URL=https://olrc.scholarsportal.info:5000/v2.0
*export OS_REGION_NAME=RegionOne

Save these in a file and run 

“source ./filename” 

to activate the variables. Then run “swift stat” to test your connection to the cloud. 

## 9. What’s the best web-based tool for accessing the OLRC Storage Cloud?

Scholars Portal programmers developed a web-based interface for uploading and interacting with files in the OLRC Storage Cloud. The tool is called SwiftBrowser, and is available for use at this address:

https://olrc.scholarsportal.info/swiftbrowser/login/

## 10. What should I use for uploading if I have thousands of small files and uploading them through SwiftBrowser is just too tedious, or takes so long my connection times out?

Scholars Portal programmers developed a command line tool called BULKuploader which keeps track of large volumes of files and will restart loading if a network connection gets interrupted. BULKUploader is available at:

https://github.com/OLRC 

A third party tool called rclone supports a simple but powerful command line interface for synchronizing local folders and files with the OLRC Storage Cloud using Swift. It too supports automatic recovery after network failures and is available at this address:

http://rclone.org/ 

## 11. Isn’t it true that OpenStack Swift has a file size limit set for data uploads?

Not quite true. OpenStack imposes a 5GB limit on uploads of single files, but supports uploading of arbitrarily large files through a process called segmentation or chunking, whereby large files are broken into smaller segments and uploaded as a group. A manifest file is used by Swift to ensure that the segments are reassembled in the correct order when a request is made to download the file. No segmentation occurs on downloading — the user requests the file and Swift uses the manifest to deliver a single large file back to the user. 

## 12. Can an account holder create sub-accounts and assign these accounts to separate or shared containers? 

At the moment, all account creation is managed by Scholars Portal systems staff. By default, each partner library is given one account, and under that account multiple containers can be created. If a library wants several users to access the cloud for uploading, then Scholars Portal staff can create as many accounts as you need for distribution to your users.

In the future, we would like to add account management tools into the SwiftBrowser tool to allow a library administrator more control over creating sub-accounts and assigning these to containers.
 
## 13. In its first release, what services are included in the OLRC Storage Cloud?

At a hardware level, the OLRC Storage Cloud is a distributed storage network running over the ORION research network with dedicated bandwidth used to support the replication of objects stored between partner sites and the automatic restoration of data in the event of hardware failure at one or more of the partner sites. 

At a software level, the OLRC Storage Cloud provides end-user software interfaces and tools to support uploading and managing data in the cloud as well as machine-user APIs to support programmatic access to the cloud from third party applications such as Archivematica. 

At an organizational level, the OLRC cloud is an agreement between partner sites to collaborate in the purchase and management of storage infrastructure in order to provide for economical high-volume storage that is vendor agnostic and is not limited in use by expensive network charges.

## 14. Is the OLRC Storage Cloud a digital preservation system?

The OLRC Storage Cloud provides libraries with replicated and robust digital storage and manages the integrity of objects stored in the cloud at a bit level. Files that are stored in the cloud have a very high probability of coming out of the cloud unchanged over a long period of time.

But the OLRC cloud does not guarantee that files stored in the cloud are safe from deletion by authorized users; nor does it guarantee that a file loaded to the cloud is readable in the first place. And so a digital preservation system normally includes features that go beyond bit preservation, including format identification and normalization and metadata to capture descriptive information and provenance. These kinds of preservation tools operate on file objects at a much higher level than Swift. An OCUL library could make very good use of the OLRC Storage Cloud as part of a comprehensive digital preservation service. But the OLRC Storage Cloud (or any other storage service, for that matter), while being a necessary element for preservation is not sufficient. An OCUL library interested in building a preservation system on top of the OLRC Cloud should be looking at archival management tools (e.g. Archivematica) and using these for the preparation of well-formed archival information packages. Archivematica integrates with Swift through the Archivematica storage services layer.

## 15. How can I access files stored in the OLRC Storage Cloud? And how can I integrate these with discovery tools or other registry/catalogue services so that I can link my users from a metadata record to the associated file as stored in the OLRC Storage Cloud.

Access to files via URL is a fundamental feature of object storage systems. All objects in the OLRC Storage Cloud have an access URL. Normally, only authorized users can access files, but permissions can be set at the file or container level to support anonymous or IP protected use. Setting permissions for a container or file is currently something that Scholars Portal systems staff can do or that the container owner can do through command line tools. 

## 16. How is the OLRC Storage Cloud different from content management tools like Dataverse or the GeoPortal? Do these tools interact with the OLRC Storage Cloud and if so, at what level?

Dataverse and the GeoPortal are content management systems with database components and are designed for the management of active data files, gathered together into studies, as in Dataverse, or to form Map Services, as in the GeoPortal. In Dataverse, metadata for each study and file is created by the end-user at upload. In the GeoPortal, a GIS analyst combines source data files and processes them into a map service which is then associated with a metadata record stored in a database.
In both cases, both metadata and data are stored on block storage to support ongoing processing, and access to the metadata and data is mediated through the application. 

The OLRC Storage Cloud is an object storage system, with no database component, which provides direct access to objects through REST-based API calls (i.e. through HTTP calls made from any HTTP compliant client). Metadata can be captured for each file, but it is not indexed for rapid access, sorting or faceting in the way it is in Dataverse or the GeoPortal.

In summary, Dataverse and the GeoPortal are preferred tools for storing data when you are working with active data that you anticipate accessing on a frequent basis for analysis. The OLRC Cloud, in comparison, is a great place to store large volumes of content, or very large files, that will remain static through their lifecycles and that you access via simple URL. 

That doesn’t preclude you from managing those URLs in metadata records collected in a tool like Dataverse or the GeoPortal. Likewise, you may choose to archive active data from Dataverse or the GeoPortal into the OLRC Storage Cloud for preservation purposes, ideally through a normalization pipeline such as Archivematica. And one of the active projects for the OLRC now is to support the transfer of data from Dataverse to the OLRC Storage Cloud through Archivematica. The OLRC Storage Cloud is also an excellent choice for storing raw GIS data files before and after they are processed into map services for use in the GeoPortal. That will be a prime use of the cloud in Scholars Portal. 

## 17. What is the difference between object storage we have through the OLRC Storage Cloud and the kind of block storage that our campus IT unit can provide us, complete with a VM and domain name? Do we need both, and if so, in what circumstances would we use one over the other?

Block storage is the right way to go if you are thinking of setting up an application or anticipate heavy use (reading and writing) of the files you want to store. VMs are attached to block storage because block storage needs to be mounted to a computer before it can be accessed. You get to the files via the operating system you install on the VM and you set permissions on files the same way. The amount of block storage you can mount on a particular VM is defined largely by the operating system.

Object storage is a different beast. Access to files is via the Web, using REST APIs and HTTP commands. You would not use object storage to run a database; but it doesn’t make sense to use expensive block storage to hold large volumes of files that you don’t anticipate ever editing. That will probably be the primary use of object storage in a library context — as an online store of large volumes of read-only digital objects and as a more effective alternative to offline storage on tape or hard drives. If individual files or groups of files need to be processed, they can be moved easily from object storage to block storage for analysis (e.g. text mining of a web archive file, normalization for archiving) and then moved back to object storage after the analysis is finished.

## 18. How can we be sure that data we store in the OLRC Storage Cloud will remain free from bit rot or other systems related failures? Do we need to monitor our data to ensure its integrity?

The library doesn’t have to do anything to ensure the integrity of what is stored in the OLRC Storage Cloud. This is handled entirely by Openstack Swift.

When an object has been uploaded to swift, the following happens:

a. The replication processes make sure that there are always 3 copies of the object. Each copy is in a different zone (In our case, a school/physical location is a zone).

b. The auditor processes crawl the local server checking the integrity of the objects, containers, and accounts. If corruption is found (in the case of bit rot, for example), the file is quarantined, and replication will replace the bad file from another replica.

----

> In case you haven't found the answer for your question please feel free to contact us and we will be happy to help you.
