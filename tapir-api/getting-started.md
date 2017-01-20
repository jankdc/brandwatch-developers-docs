---
title: "Getting Started with Tapir"
excerpt: "This page will help you get started with Tapir. You'll be up and running in a jiffy!"
---
Install tapir via npm
```shell
npm install --save vizia/tapir#v3.x
```
Make a simple bundle
```javascript
const tapir = require('@vizia/tapir')
const log = require('@vizia/tapir/destinations/log')

const bundle = tapir()

const people = [
  {
    name: 'donny'
  },
  {
    name: 'donson'
  }
]

bundle.source(people)

bundle.use(person => person.name)

bundle.use(log)

module.exports = bundle
```