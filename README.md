Sproingg!
=========

What is Sproingg?
-----------------

Sproingg is an experiment at layering interpersonal communication on top of CouchDB's replication protocol.
Sproingg attempts to use a single simple substrate (CouchDB replication over HTTP) for a number of different modes of interpersonal communication, synchronous and asynchronous, individual, small group and large group. (HTTPS is outside scope for now)

Aside from using CouchDB replication to move structured data (message documents) Sproingg attempts to tackle the problem of endpoint addressing in the context of an HTTP based messaging system.


Does Sproingg work over vanilla CouchDB or does it need extensions?
-------------------------------------------------------------------

The goal is to work on vanilla CouchDB with some specific configuration for databases, some mandatory user(s), specific views and a CouchApp to embody all or large parts of it all (TBD).

To separate CouchDB's being used as Sproingg endpoints from regular CouchDB's the only difference (experimental) is to run the CouchDB to listen on a special port 3939.

How do you express the address of a Sproingg endpoint?
------------------------------------------------------

A Sproingg endpoint is a CouchDB host with a set of mandatory databases, one of which is sphead (sproingg head, kinda like postmaster in email). Only admin users are allowed to access sphead db.  

* A typical Sproingg host has a base URL of the form http://mydomain.com:3939/sphead, alternately a URL of the form.  Note that :3939 is not required but /sphead is required. Hence given any arbitrary known CouchDB installation, if it has an sphead database then it is assumed to be a Sproingg endpoint.  

A CouchDB instance may continue to serve database duties while serving Sproingg requests at the same time.

How are Sproingg addresses discovered?
----------------------------------------

Initial list of Sproingg hosts will be created at sproingg.com/info

How does one initiate a Sproingg session?
-------------------------------------------

Sproingg sessions are *currently* loosely based on SMTP.  This may change.
The sender host starts with an initial request to inquire whether the recipient host supports Sproingg i.e has an /sphead endpoint.
A positive response from the responding host is followed by a second request from the sender host to inquire if a specific named recipient exists in the _user db.
Assuming we have reached so far the Sproingg sender initiates a CouchDB replication pushing a Sproingg message on to the recipient hosts message queue via some filtered replication (TBD) that is expected to be present in a Sproingg host.
All of the above to be made specific in terms of endpoints, update handlers etc

What does a Sproingg message look like?
-----------------------------------------

A Sproingg message is a JSON imitation of an email MIME multipart object as follows

<pre>
	{
	   _id: uuid,
	   _rev: uuid,
	    headers: {
	 	       from: string,
	 	       to: string,
                       ...
		     },
	    body: UTF-8 string,
	    _attachments: {
			     mime :[
			             attachment1: { stuff that looks like MIME subpart },
			             attachment2: { stuff that looks like MIME subpart },
			             ...
                                   ]
		           }

	}
</pre>	

What does a Sproingg message queue look like?
-----------------------------------------------
It's a database with each document a Sproingg message.
A message queue is probably optimally implemented using node.js + redis for reasons related to the number of writes, the frequency of deletes and the need for parallelism and async processing of each message as it comes in.
It's possible also that the message queue could be an Erlang implementation.

What does a Sproingg user database look like?
-----------------------------------------------

For now its exactly the user db in a Sproingg host.  When a host is used for both Sproinggy and non-Sproinggy purposes the user db will need to be managed with a lot more care to avoid auth leakage.

What does a Sproingg inbox look like? 
------------------------------------

It is a database owned by the inbox owner - only the CouchDB processes can write to it aside from the user-owner.

Why the name Sproingg?
---------------------

Sproingg is surprising, spontaneous, unexpected and fun all of which are suggested by the sound "Sproingg!".
It is required to use an exclamation mark as in "Sproingg!" as the mere "Sproingg" does not catch the spirit of it.
When speaking the word Sproingg! an extended 'nggg' sound as well as wide eyes and the expression of a jack-in-the-box are suggested.

Sproingg sprung out of Couch like a ... spring, making the loud sound "Sproingg!!" in the middle of the night.
No one knew what had happened till it .. well dawned on them in the morning.


Does Sproingg have an acronymal (yes I did make up that word) interpretation?
-----------------------------------------------------------------------------

You had to go there did you? Oh well. Here goes.

SPROINGG: **SP**ecial **R**eplication **O**riented **I**nter**N**et **G**ee**G**aw
