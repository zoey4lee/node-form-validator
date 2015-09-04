#  [![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Dependency Status][daviddm-image]][daviddm-url]

> Validator for http request, json.


## Install

```sh
$ npm install --save node-form-validator
```


## Configurations

### Format

A configuration is an object with fieldNames and attributes describing the corresponding fieldName.

The following is a very simple example for node-form-valiator configuration

```js
var conf = {
  fieldName: {
    type: 'string'
    required: true,
    minLength: 1,
    maxLength: 100
  }
}
```
#### Attributes

There a currently 8 attributes available.

- <code>type</code>
    string, required for every fields to be validated
- <code>matches</code>
    string, if this attribute is specified, then there must be an another field to be matched with
- <code>alias</code>
    string, If this attribute is specified, then the <code>name</code> field must be companied for it will be translated into this alias.    
- <code>name</code> string, must be specifed when <code>alias</code> or <code>matches</code> enabled
- <code>required</code> boolean.
    * true: when this field must be specified
    * false: default
- <code>minLength</code> integer, minimum length for a string, only valid when type is <code>string</code> or <code>text</code>
- <code>maxLength</code> integer, maximum length for a string, only valid when type is <code>string</code> or <code>text</code>
- <code>locale</code> string, must be locale strings, like <code>zh-CN</code>, <code>zh-HK</code>, <code>en-US</code>, <code>en-GB</code>

## Supported types

```js
  'email'
  'url'
  'fqdn'
  'ip'
  'alpha'
  'numeric'
  'alphanumeric'
  'base64'
  'hexadecimal'
  'hexcolor'
  'int'
  'float'
  'uuid'
  'date'
  'json'
  'creditcard'
  'isbn'
  'phone'
  'ascii'
  'multibyte'
  'time'
  'string': no more than 256 chars
  'text': no more than 65536 chars
```

## Usage

### Define configuration

    //Validate
    var conf = {
      password: {
        type: 'string',
        minLength: 3,
        maxLength: 64,
        required: true
      },

      comfirm: {
        type: 'string',
        matches: 'password',
        required: true
      },
      phone: {
        type: 'phone',
        required: true,
        locale: 'zh-CN'  
      },
      echostr: {
        type: 'string',
        required: true
      }
    };

### Validation

```js
var validator = require('node-form-validator');
var error = {};
```


- validate http requests

```js
function(req, res) {
  var dataToBeExtracted = {}
  //Errors reported
  var error = {};
  if (validator.v(req, conf, dataToBeExtracted, error)) {
  // Do something for validation passed
  } else {
  // Do something for validation failed
  }
}
```

- validate json objects

```js
  var dataToBeExtracted = {}
  //Errors reported
  var error = {};
  if (validator.validate(conf, dataToBeExtracted, error)) {
  // Do something for validation passed
  } else {
  // Do something for validation failed
  }
```

- extraction from json

```js
  var extractedData = validator.json.extract(conf, dataToBeExtracted));
```


## License

MIT © [calidion](blog.3gcnbeta.com)


[npm-image]: https://badge.fury.io/js/node-form-validator.svg
[npm-url]: https://npmjs.org/package/node-form-validator
[travis-image]: https://travis-ci.org/JSSDKCN/node-form-validator.svg?branch=master
[travis-url]: https://travis-ci.org/JSSDKCN/node-form-validator
[daviddm-image]: https://david-dm.org/JSSDKCN/node-form-validator.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/JSSDKCN/node-form-validator
