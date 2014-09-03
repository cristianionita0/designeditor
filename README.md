Appzip
======

Couchdb application installer

Appzip allows you to publish (load) into CouchDB applicaitons (couchapps) from a zip file.


How to install
==============

Download files or just app.zip (unzip it after download).
In a terminal, automatic install:

<pre><code>
./push2couch.sh
</code></pre>

Or install manually:
* createa new CouchDB database appzip
* create new design document _design/appzip
* attach all files from archive (except *.zip)

Access url: http://localhost:5984/appzip/_design/appzip/index.html and you should see the web interface.

Usage
=====

If you have CouchDB administrator user declared (no admin party) enter the user name and password in the first fields.
Then choose your zip file. You will see on the page the content of the zip file displayed.
Click on *Push Application to CouchDB*.
If everything is ok then the message *Succesfully imported Application to CouchDB!* is displayed.
Access your published application, relax and have fun!

Structure of zip file
=====================

There are a couple of rules that must be respected:

1. In the root of your zip a file named *manifest.json* must be present. The structure of the file is:

  {
	  "database":["database_name"]
  }
  
  The *database* attibute contains a list of strings with database names

2. For each database_name a folder and file structure must be implemented. The database folder is at top level:

Directory and file structure:

<pre>
[database_name]
  |
  |_ [document_name]
  |    |
  |    |_[design_document_structure]
           |
           |_ doc_attributes.js
  .
  .
  .
</pre>


Design document folder and file structure structure

<pre>
attachements
views
 |_ map
 |_ reduce
lists
shows
updates
filters
rewrites
validate_doc_update
fulltext
</pre>

doc_attributes.json file structure

A JSON containing all atributes of the document. If no _id is provided then a new "data" document is create. In order to create a design_doc use "_id": "_design/[design_document_name]. Defult language is javascript if not provided.

<pre>
{
 "_id":"[design_document_name]",
 "language":"javascript",
 ["attribute"]:[value]
}
</pre>

3. Zip all these files and push them to CouchDB and you will have your application

A good example is designeditor, it is distributed as an appzip CouchDB application.
