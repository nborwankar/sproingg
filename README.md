Sproingg!
=========

What is Sproingg?
-----------------

Sproingg is an experiment at layering interpersonal communication on top of CouchDB's replication protocol.
Sproingg attempts to use a single simple substrate (CouchDB replication over HTTP) for a number of different modes of interpersonal communication, synchronous and asynchronous, individual, small group and large group.

Aside from using CouchDB replication to move structured data (message documents) Sproingg attempts to tackle the problem of endpoint addressing in the context of an HTTP based messaging system.


Why the name Sproingg?
---------------------

Sproingg sprung out of Couch like a ... spring, making the sound "sproingg!!"
Sproingg is surprising, spontaneous, unexpected and fun all of which are suggested by the sound "Sproingg!".




* Does Sproingg work over vanilla CouchDB or does it need extensions?

The goal is to work on vanilla CouchDB with some specific configuration for databases, some mandatory user(s), specific views and a CouchApp to embody all or large parts of it all (TBD).

To separate CouchDB's being used as Sproingg endpoints from regular CouchDB's the only difference (experimental) is to run the CouchDB to listen on a special port 3939.

* How do you express the address of a Sproingg endpoint?

A Sproingg endpoint is a CouchDB host with a set of mandatory databases, one of which is headsp (headsproingg). Only admin users are allowed to access 


* How are such addresses discovered?
* How does on initiate a Sproingg session?
* What does a Sproingg message look like?
* What does a Sproingg message queue look like?
* What does a Sproingg user data look like?
* What does a Sproingg 

* What does 


