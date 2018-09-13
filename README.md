# :cloud: Trust Ray :cloud:

API for the Trust Ethereum Wallet.

## Features

* Parsing entire blockchain
* Retrieving transactions with operations field for ERC20 contract actions
* Retrieving ERC20 token balances
* Push notification service (not yet implemented)

## API [wiki](https://github.com/TrustWallet/trust-ray/wiki/API)


## Deploy on Heroku
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://www.heroku.com/deploy/?template=https://github.com/TrustWallet/trust-wallet-backend)

## Locally (without docker)
* Install required modules:
  ```$ npm install```
* Compile TypeScript:
  ```$ npm run build```
* Start the app:
   ```$ node dist/server.js```
* Run tests:
   ```$ npm run build && npm test```

## Use Nginx
* Install required modules:
  ```$ npm install```
* Compile TypeScript:
  ```$ npm run build```
* Install nodejs: https://nodejs.org/en/
* Install pm2:
  ```$ npm install pm2 -g```
* Start the app:
   ```$ pm2 start dist/server.js```
* Install nginx
* Config nginx
```
map $http_upgrade $connection_upgrade {
        default upgrade;
        ''      close;
}

upstream websocket {
        server 127.0.0.1:8000;
}

server {
    server_name <your_domain>;

    client_max_body_size 0;
    chunked_transfer_encoding on;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade; #for websockets
        proxy_set_header Connection $connection_upgrade;
        proxy_set_header X-Forwarded-For $remote_addr;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_redirect off;

        proxy_connect_timeout       600s;
        proxy_send_timeout          600s;
        proxy_read_timeout          600s;
    }
}
```

## Docker containers
Install docker and docker-compose.

Set in *~/.bashrc*
```export COMPOSE_FILE=docker-compose.yml:docker-compose.dev.yml```

Set in .env
```MONGODB_URI=mongodb://mongodb:27017/trust-wallet```

Dev tool:

* Run build for npm install and build
```./trust build```

* Start app in docker
```./trust run```

* Stop docker containers
```./trust stop```

* App logs
```./trust logs```

## Authors

* [Philipp Rieger](https://github.com/rip32700)
* [Michael Scoff](https://github.com/michaelScoff)
* [Mykola Radchenko](https://github.com/kolya182)


## Contributing

We intend for this project to be an educational resource: we are excited to
share our wins, mistakes, and methodology of iOS development as we work
in the open. Our primary focus is to continue improving the app for our users in
line with our roadmap.

The best way to submit feedback and report bugs is to open a GitHub issue.
Please be sure to include your operating system, device, version number, and
steps to reproduce reported bugs. Keep in mind that all participants will be
expected to follow our code of conduct.

## Code of Conduct

We aim to share our knowledge and findings as we work daily to improve our
product, for our community, in a safe and open space. We work as we live, as
kind and considerate human beings who learn and grow from giving and receiving
positive, constructive feedback. We reserve the right to delete or ban any
behavior violating this base foundation of respect.
