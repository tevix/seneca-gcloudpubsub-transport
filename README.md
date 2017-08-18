# seneca-gcloudpubsub-transport

Seneca GCLOUD Pub/Sub transport.

[Seneca](http://senecajs.org/) is a microservices framework and [Google Cloud Pub/Sub](https://cloud.google.com/pubsub/docs/overview) brings the scalability, flexibility, and reliability of enterprise message-oriented middleware to the cloud.

This transport sends request to a topic and wait for results in another queue in Google Cloud Pub/Sub

## Installation

```bash
npm install seneca-gcloudpubsub-transport --save
```

## Usage

**You are going to need credentials file to run this from your local machine**

```javascript
// server.js

require('seneca')({log:"debug"})
    .use('gcloudpubsub-transport')
    .add('role:foo,cmd:two', function (args, done) { done(null, { bar: args.bar }) })
    .listen({type:'gcloud', 
    		 topicPrefix: 'test', 
    		 projectId:'putYourProjectIdHere' 
    		 keyFilename: '/path/to/your/keyfilename.json'});
```

```javascript
// client.js

let seneca = require('seneca')({ log: "debug" });


seneca.use('gcloudpubsub-transport');
var client = seneca.client({type:'gcloud', 
             					  topicPrefix: 'test', 
	             				  projectId:'putYourProjectIdHere' 
             					  keyFilename: '/path/to/your/keyfilename.json'});
client.act('role:foo,cmd:two', { bar: 'hello from gcloud' }, function (err, response) {
    if (err) {
        console.log(err);
    }
    else {
        console.log(response);
    }
});




```

```bash
node server.js
node client.js
```

## License

Licensed under The MIT License (MIT)  
For the full copyright and license information, please view the LICENSE.txt file.

[npm-url]: http://npmjs.org/package/seneca-nats-transport
[npm-image]: https://badge.fury.io/js/seneca-nats-transport.svg

[travis-url]: https://travis-ci.org/devfacet/seneca-nats-transport
[travis-image]: https://travis-ci.org/devfacet/seneca-nats-transport.svg?branch=master

[coverage-url]: https://coveralls.io/github/devfacet/seneca-nats-transport?branch=master
[coverage-image]: https://coveralls.io/repos/github/devfacet/seneca-nats-transport/badge.svg?branch=master
