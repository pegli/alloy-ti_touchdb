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

Installation
------------

1. Create an Alloy project as per the [Alloy documentation](https://github.com/appcelerator/alloy/blob/master/README.md).
1. Follow the instructions for adding the [TiTouchDB](https://github.com/pegli/ti_touchdb/wiki) module to your project.
1. Clone this repo and copy the `alloy/sync/titouchdb.js` file to your project's `app/lib` directory.

Creating a Model
----------------

Create a new model using `alloy generate model MODELNAME titouchdb`.  This will create a new file named
`models/MODELNAME.js` that looks like this:

```javascript
exports.definition = {
  config: {
		"adapter": {
			"type": "titouchdb",
			"collection_name": "MODELNAME"
		}
	},		

	extendModel: function(Model) {		
		_.extend(Model.prototype, {
		}); // end extend
		return Model;
	},
	
	extendCollection: function(Collection) {		
		_.extend(Collection.prototype, {
		}); // end extend
		return Collection;
	}
}
```

Collections in alloy-ti_touchdb map to [TouchDB views](http://guide.couchdb.org/draft/views.html).
Each model is associated with a design document that holds one or more views used to fetch collections
of the model.  In order to fetch collections in Alloy, you must specify the design doc name by adding
a property named `design_doc` to the `adapter` object in the model source file.  You can optionally
specify the default view to use to fetch collections by adding a `views` property to the `adapter`
object as well:

```javascript
  config: {
    "adapter": {
      "type": "titouchdb",
      "collection_name": "MODELNAME",
      "design_doc": "myddoc",
      "views": ["default", "by_name"]
    }
  },
```

Optional adapter properties are:

* **modelname** (String)  adds a property to all new documents named `modelname` with the provided
  value.  This is useful to differentiate document types within the TouchDB database.  The property
  name "modelname" was chosen for compatibility with [Spine](http://spinejs.com/)'s persistence mechanism.
* **view_options** (Object) add global options for view queries.  Currently supports `prefetch`, `limit`, 
  `skip`, `descending`, and `group_level`.  See the [TiTouchDB docs](https://github.com/pegli/ti_touchdb/blob/master/mobile/noarch/documentation/index.md)
  for information about these parameters.


