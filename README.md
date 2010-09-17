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


How do you express the address of a Sproingg endpoint?
------------------------------------------------------

A Sproingg endpoint is a CouchDB host with a set of mandatory databases, one of which is sproingg. Only admin users are allowed to access sproingg db.  

* A typical Sproingg host has a base URL of the form http://mydomain.com:3939/sproingg.  Note that :3939 is not required but /sproingg is required. Hence given any arbitrary known CouchDB installation, if it has an sproingg database then it is assumed to be a Sproingg endpoint.  

A CouchDB instance may continue to serve database duties while serving Sproingg requests at the same time.

How are Sproingg addresses discovered?
----------------------------------------

An initial list of Sproingg hosts will be created at sproingg.com/info (or maybe sproingg.couchone.com/info)

What does a Sproingg message look like?
-----------------------------------------

Any JSON document can be "sproingg enabled" easily by adding a "sproingg" attribute to it.
Sproingg enabled documents acquire full "sproingginess" and become routable by including a "sproingg" attribute.

A Sproingg attribute (which will get attached to a document) is of the following form:-

<pre>
sproingg:	{
	 	       	from: string,
	 	       	to: string,
	           	date: ISO date string,	
	                      ...
	              [ other  optional headers ]
					      ...	               
			}	
</pre>
	
Right now, we are not focusing on gatewaying to email.  Sproingg is NOT email in JSON over HTTP.
Sproingg is an experiment in p2p messaging over HTTP using CouchDB replication.

What does a Sproingg message queue look like?
-----------------------------------------------
It's a database with each document a Sproingg message.
A message queue is probably optimally implemented using node.js + redis for reasons related to the number of writes, the frequency of deletes and the need for parallelism and async processing of each message as it comes in.
It's possible also that the message queue could be an Erlang implementation.
But for now it's just a couchdb database called Outbox.

What does a Sproingg user db look like?
---------------------------------------

*For now* we assume that a Sproingg user has their own Couch instance in which there is only one user and they have admin rights to all the db's in the instance.  So the user db maybe unnecessary or has a single user who has the _admin role.

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
