### Keycloak Admin Client

An client for connecting to the Keycloak Admin REST API - http://www.keycloak.org/docs-api/3.2/rest-api/index.html

## Installation

```
npm install keycloak-admin-client -S
```

## Usage

```js
'use strict';

const adminClient = require('./');

const settings = {
  baseUrl: 'http://127.0.0.1:8080/auth',
  username: 'admin',
  password: 'admin',
  grant_type: 'password',
  client_id: 'admin-cli'
};

adminClient(settings)
  .then((client) => {
  console.log('client', client);
  client.realms.find()
    .then((realms) => {
    console.log('realms', realms);
    });
  })
  .catch((err) => {
    console.log('Error', err);
  });
```

## Development & Testing

To run the tests, you'll need to have a keycloak server running. No worries!
This is all taken care of for you. Just run `./scripts/start-server.sh`.
If you don't already have a server downloaded, this script will download one
for you, start it, initialize the admin user, and then restart.

Then just run the tests.

```
make test
```

To stop the server, run `./scripts/stop-server.sh`.


### Notable Changes from 0.1.0 to 0.2.0

The API has been changed to logically group up(namespace) functionality.

For example,  the 0.1.0 way of getting a list of all realms was by calling the `client.realms` function.

Now in 0.2.0, you would do something like this: `client.realms.find`

`find` can also be used to get 1 realm by passing in the realmName: `client.realms.find('master')`

The other methods have been renamed too, for example, instead of calling `client.updateRealm` you would now call `client.realms.update`

## Contributing

Please read the [contributing guide](./CONTRIBUTING.md)

## Reporting security vulnerabilities

If you've found a security vulnerability, please look at the [instructions on how to properly report it](http://www.keycloak.org/security.html)

