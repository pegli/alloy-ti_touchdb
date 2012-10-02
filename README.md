alloy-ti_touchdb
================

**alloy-ti_touchdb** is a persistence adapter which allows you to use 
[TiTouchDB](https://github.com/pegli/ti_touchdb) to store model objects
within [Alloy](https://github.com/appcelerator/alloy), the MVC application
framework for [Appcelerator Titanium](http://www.appcelerator.com/platform).
Why the heck would you need that?  Well...

* Alloy makes it dead simple to save your application's data by using
  [Backbone](http://backbonejs.org/) model objects to relieve you
  of the burden of writing a bunch of persistence code.  See the
  [Alloy README](https://github.com/appcelerator/alloy/blob/master/README.md#working-with-models--collections)
  for an example of how to interact with models.
* TouchDB is a lightweight [Apache CouchDB](http://couchdb.apache.org/)-compatible
  database engine suitable for embedding into mobile or desktop apps.
  TouchDB can sync data between a mobile device and CouchDB servers, providing
  a mobile, offline copy of the data while the user is not connected to the
  network and a synchronized copy when the network is available.
* TiTouchDB is a Titanium module which wraps the [TouchDB-iOS](http://labs.couchbase.com/TouchDB-iOS/)
  and [TouchDB-Android](https://github.com/couchbaselabs/TouchDB-Android)
  libraries, providing cross-platform support for TouchDB in Titanium.

What you get with alloy-ti_touchdb is an MVC framework that painlessly syncs
your app's data to and from your server.

Current Status
--------------

* 2012-10-02 - Initial release
