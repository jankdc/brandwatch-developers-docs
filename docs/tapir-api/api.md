---
title: "API"
excerpt: ""
---
# @vizia/tapir
tapir - a framework for building pipelines and composing bundles

### api

#### modules

  - [@vizia/tapir](#tapir)
    - [@vizia/tapir/bundle](#bundle)
    - [@vizia/tapir/sources](#sources)
      - [@vizia/tapir/sources/array](#arrayarr)
      - [@vizia/tapir/sources/http](#httpurl)
    - [@vizia/tapir/destinations](#destinations)
      - [@vizia/tapir/destinations/drain](#drain)
      - [@vizia/tapir/destinations/dom](#dom)
      - [@vizia/tapir/destinations/log](#log)
    - [@vizia/tapir/transforms](#transforms)
      - [@vizia/tapir/transforms/concat](#concat)
      - [@vizia/tapir/transforms/json](#json)
      - [@vizia/tapir/transforms/map](#map)
    - [@vizia/tapir/util](#util)
      - [@vizia/tapir/util/compose](#compose)
      - [@vizia/tapir/util/pick](#pick)
      - [@vizia/tapir/util/wrap](#wrap)

---

### tapir

###### @vizia/tapir

`tapir` is the top level export, it is an alias for the [`bundle`](#bundle)
function. It will pull in every module of the tapir library, you can access sub
modules with object notation e.g.

[block:code]
{
    "codes": [
        {
            "code": "const tapir = require('@vizia/tapir')\ntapir.util.compose(g, f) // etc...\n",
            "language": "javascript"
        }
    ]
}
[/block]

---

#### bundle()

###### @vizia/tapir/bundle

This function is used to create your bundle to be used by vizia.

[block:code]
{
    "codes": [
        {
            "code": "const createBundle = require('@vizia/tapir/bundle')\nconst bundle = createBundle()\n",
            "language": "javascript"
        }
    ]
}
[/block]

##### `bundle.set(prop, value)`

Adds a property to the bundles internal config object, this is merged with the
config passed into `load` before being distributed to any of the pipes in the
bundle.

returns `bundle`

[block:code]
{
    "codes": [
        {
            "code": "bundle.set('chartType', 'bar')\n",
            "language": "javascript"
        }
    ]
}
[/block]

##### `bundle.config(fn)`

Adds a function parsing config, `fn` will be called with the config passed into
`load` and the return value will be used instead of the original config.

returns `bundle`

[block:code]
{
    "codes": [
        {
            "code": "bundle.config(config => {\n  return {\n    secret: config.meta.secret,\n    color: config.colour || config.color\n  }\n})\n",
            "language": "javascript"
        }
    ]
}
[/block]

##### `bundle.use(pipe)`

Adds `pipe` to the internal pipeline of the bundle. pipes are added in the order
they are `use`d, so order matters.

returns `bundle`

[block:code]
{
    "codes": [
        {
            "code": "bundle.use(http('http://example.com'))\n",
            "language": "javascript"
        }
    ]
}
[/block]

##### `bundle.use(fn)`

Wraps `fn` in the [map](#map) transform and adds it to the internal pipeline.

returns `bundle`

[block:code]
{
    "codes": [
        {
            "code": "bundle.use(data => data.value)\n",
            "language": "javascript"
        }
    ]
}
[/block]

##### `bundle.use({create: fn})`

When called with an object that has a `create` method, create will be called
with the final state of the config after `load` and the return value of `create`
(a pipe) will be added to the bundle, it will be added at the point use was
called, _not_ to the end.

returns `bundle`

```javascript
bundle.use({
  create: function (config) {
    return http(`https://api.example.com/endpoint?limit=${config.limit}`)
  }
})
```

---

#### sources

###### @vizia/tapir/sources

Exports an object containing containing all of the sources, equivalent of

`require('@vizia/tapir').sources`

[block:code]
{
    "codes": [
        {
            "code": "const sources = require('@vizia/tapit/sources')\nsources.http('http://example.com') // etc...\n",
            "language": "javascript"
        }
    ]
}
[/block]

#### array(arr)

###### @vizia/tapir/sources/array

Returns a pipe that outputs each item in the array once

[block:code]
{
    "codes": [
        {
            "code": "const source = array([1, 2, 3, 4])\n",
            "language": "javascript"
        }
    ]
}
[/block]

#### http(url)

###### @vizia/tapir/sources/http

Returns a pipe that outputs data from a GET request to `url`

[block:code]
{
    "codes": [
        {
            "code": "const source = http('proto://host:port/path')\n",
            "language": "javascript"
        }
    ]
}
[/block]

---

#### destinations

###### @vizia/tapir/destinations

Exports an object containing containing all of the destinations, equivalent of
`require('@vizia/tapir').destinations`

[block:code]
{
    "codes": [
        {
            "code": "const destinations = require('@vizia/tapit/sources')\ndestinations.log // etc...\n",
            "language": "javascript"
        }
    ]
}
[/block]

#### drain(fn [, done])

###### @vizia/tapir/destinations/drain

Returns a destination that will recursively drain from upstream, calling fn with
every new piece of data, and calling done when the upstream ends or errors

[block:code]
{
    "codes": [
        {
            "code": "const dest = drain(data => console.log(data), err => console.log(err || 'done!'))\n",
            "language": "javascript"
        }
    ]
}
[/block]

#### log

###### @vizia/tapir/destinations/log

A destination that logs all data, useful for debugging.

[block:code]
{
    "codes": [
        {
            "code": "const dest = require('@vizia/tapir/destinations/log')\n",
            "language": "javascript"
        }
    ]
}
[/block]

#### dom

###### @vizia/tapir/destinations/dom

A destination for writing to the DOM.

```javascript
const dom = require('@vizia/tapir/destinations/dom')
const destination = dom('.some-selector', {
  onData: function onData (data, next) {
    this.element.innerHTML += `<span> ${data.text} </span>`
    done()
  },
  onEnd: function onEnd (data) {
    console.log('Got all the data')
  }
})
```

##### options

[block:code]
{
    "codes": [
        {
            "code": "{\n  // function to call on creation, defaults to noop\n  init: function init () {},\n\n  // function that gets called on each new piece of data, must call done when finished processing. defaults to noop\n  onData: function (data, done) { done() },\n\n  // function that gets called when all of upstream data has been written. defaults to noop\n  onEnd: function (data) {},\n\n  // sets the destination to appendMode. defaults to false\n  appendMode: false,\n\n  // how much of a tail to keep when in appendMode. defaults to Infinity if appendMode is true\n  tailLength: Infinity,\n\n  // set the stream into objectMode. defaults to true\n  objectMode: true\n}\n",
            "language": "javascript"
        }
    ]
}
[/block]

##### appendMode

By default dom destinations are not in appendMode. This means that on each
new piece of data, the this.data property is set to the new data. appendMode
however will append each new piece of data to the this.data property, which will
be an array.

appendMode also supports a tailLength property, by default this is Infinity,
meaning our data array can grow to any length. When a tail length is set, the
data array will never be longer than the tailLength, and will remove the oldest
pieces of data as necessary

---

#### transforms

###### @vizia/tapir/transforms

Exports an object containing containing all of the transforms, equivalent of
`require('@vizia/tapir').transforms`

[block:code]
{
    "codes": [
        {
            "code": "const transforms = require('@vizia/tapit/sources')\ntransforms.json('*') // etc...\n",
            "language": "javascript"
        }
    ]
}
[/block]

#### concat

###### @vizia/tapir/transforms/concat

concat will consume all of the upstream data and push downstream a single array
contaaining all the upstream data.

[block:code]
{
    "codes": [
        {
            "code": "const concat = require('@vizia/tapir/transforms/concat')\nbundle.use(concat)\n",
            "language": "javascript"
        }
    ]
}
[/block]

#### json([path])

###### @vizia/tapir/transforms/json

Creates a parse transform that reads in stringified JSON and outputs objects.

[block:code]
{
    "codes": [
        {
            "code": "const parse = json('items.*')\n",
            "language": "javascript"
        }
    ]
}
[/block]

#### map(fn)

###### @vizia/tapir/transforms/map

Creates a transform that works like Array#map. runs fn over each piece of
upstream data and sends the return value downstream

[block:code]
{
    "codes": [
        {
            "code": "const addName = map(name => {\n  return {\n    name: name\n  }\n})\n",
            "language": "javascript"
        }
    ]
}
[/block]