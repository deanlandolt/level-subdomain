# level-subdomain

Augment a sublevel to treat its contents as a collection of models.

```js
var subdomain = require('level-subdomain')

var root = subdomain(db, dbOpts)

root.subdomain('some-ns', schema)
```

A `subdomain` represents a collection with an associated data model. Like sublevels, subdomains can be nested, and a subdomain may allocate additional subdomains within itself to house e.g. secondary index data. Combined together, a root subdomain can be created which represents the domain model of an application.

A `subdomain` is described by a `level-manifest-services`-style object. This is a JSON-serializable format extending the format defined by `level-manifest` with some services-related additional keys. JSON-Schema is used to descibe the data model of records within a subdomain. Methods may also be annotated with additional metadata to define their behavior when exposed over HTTP, either via a REST-style JSON API or via a JSON-RPC endpoint.


## Model Schema

A schema is a blend of json-schema and level-manifest. You define your model structures in json-schema, and the underlying interface on level-manifest. Object properties are defined in the `properties` key, while `level-manifest`-style interfaces are defined in the `methods` key


## HTTP Endpoints

We also extend the `level-manifest` method definition format to allow HTTP metadata to be embedded, allowing methods to be exposed as HTTP envpoints, either via a REST-style JSON API or via JSON-RPC. Typical HTTP verbs and REST conentions are mapped onto the standard levelup endpoints, but arbtrary manifest methods may be exposed as HTTP endpoints with some additional metadata. are mapped Arbitrary endpoints to be described (see [level-manifest-services](https://github.com/deanlandolt/level-manifest-services) for more details):

```js
methods: {
  verifyAuth: {
    type: 'async',
    http: {
      method: 'POST',
      path: 'verify'
    }
  }
}
```


