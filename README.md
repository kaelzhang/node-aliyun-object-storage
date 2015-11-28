[![Build Status](https://travis-ci.org/kaelzhang/node-aliyun-object-storage.svg?branch=master)](https://travis-ci.org/kaelzhang/node-aliyun-object-storage)
<!-- optional npm version
[![NPM version](https://badge.fury.io/js/aliyun-object-storage.svg)](http://badge.fury.io/js/aliyun-object-storage)
-->
<!-- optional npm downloads
[![npm module downloads per month](http://img.shields.io/npm/dm/aliyun-object-storage.svg)](https://www.npmjs.org/package/aliyun-object-storage)
-->
<!-- optional dependency status
[![Dependency Status](https://david-dm.org/kaelzhang/node-aliyun-object-storage.svg)](https://david-dm.org/kaelzhang/node-aliyun-object-storage)
-->

# aliyun-object-storage

An easy-to-use stream-enabled client for Aliyun OSS (Object Storage Service).

## Install

```sh
$ npm install aliyun-object-storage --save
```

## Usage

```js
var oss = require('aliyun-object-storage')(bucket_name, options);
```

- **bucket_name** `String=` aliyun oss bucket name
- **options**
  - **secret** `String` aliyun access key secret
  - **id** `String` aliyun access key id

`oss` is an duplex stream (both readable and writable stream), so that you could write your image uploading server as:

```js
http.createServer(function(req, res){
  req.pipe(oss).pipe(res);
}).listen(8888);
```

#### Upload an object

```js
fs.createReadStream('/path/to/a.png').pipe(oss);
```

#### Download an object

```js
oss(file).pipe(fs.createWriteStream('/path/to/a.png'));
```

#### oss.upload(filename, callback);

```js
oss.upload('/path/to/a.png', function (err, response, filename){
  
});
```

#### oss.download(filename, callback);

#### <strike>oss.create(bucket_name, callback)<strike>

No, creating bucket using api is really silly, because the max number of buckets is limited. 

Go login into your Aliyun dashboard, and create it your own.


## License

MIT
