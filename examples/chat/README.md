## What we need
- socket-request-server
- socket-request-client

## prepare project folder
create a new folder and name it socketchat then go into that folder and create the "src" directory

## setting up package.json
open a command terminal and type ```npm init```

## install dependencies
```sh
npm install --save socket-request-server socket-request-client
```

## install devdependencies
```sh
npm install --save rollup
```

## configure package.json
add ```js rollup: rollup -c,``` to scripts (abover, under or replacing test ...)

## rollup.config.js
```js
export default {
  input: ['src/client.js', 'src/server.js'],
  output: {
    dir: './',
    format: 'cjs',
    experimentalCodeSplitting: true
  },
  treeshake: true
}
```

## server.js
Create a server.js file in your sources folder (src)
```js
import server from 'socket-request-server';

const api = server({port: 6000, address: '127.0.0.1', protocol: 'my-protocol'}, {
  hello: (params, request) => {
    request.send('hello world')
  }, 
  sayHi: (params, request) => {
    console.log(params.name, params.lastname)
    
    request.send(`Hi, ${params.name} ${params.lastname}!`)
  }
})
```

## client.js
Create a client.js file in your sources folder (src)
```js
import clientConnection from 'socket-request-client';

(async () => {
  const connection = await clientConnection({port: 6000, address: '127.0.0.1', protocol: 'my-protocol'})
  
  const world = await connection.request({url: 'hello'});
  
  console.log(world) // logs 'hello world'
  const hi = await connection.request({url: 'sayHi', params: {name: 'John', lastname: 'Doe'}})
  console.log(hi) // logs Hi, John Doe!
})()
```

## build
```sh
npm run rollup
```

## run
```sh
node server.js

node client.js
```
