# vue-sync

> Synchronizes the state of vue components with other places.
> Currently there are plans for different synchronization strategies:
>
> 1. [x] Browser URL 
> 2. [ ] Browser local storage
> 3. [ ] Server API / websockets
> 4. [ ] WebRTC

## Install

    $ npm install vue-sync
  
## Usage

General usage

    VueSync = require('vue-sync')
    Vue.use(VueSync)
    
    new Vue({
      data: {
        someKey: 'someValue'
      },
      sync: {
        someKey: syncStrategy
      }
    })

### Sync Strategies

#### Browser URL

Sync state with browser URL

    sync = VueSync.locationStrategy()
    
    new Vue({
      data: {
        currentPage: 'users'
      },
      sync: {
        currentPage: sync('page')
      }
    })
    
`locationStrategy(parameterName, noHistory = false)`

* `parameterName`: (String) The parameter in the browser URL to use to sync with the Vue key. In the above example, the strategy will sync the value of `currentPage` with an URL that might look something like `http://somedomain.com/somesite/?page=users`
* `noHistory`: (Boolean) Whether or not a browser history entry should be created every time the value changes. This enables or prevents the user to change Vue state using the navigation buttons of the browser.


#### Local Storage

Sync state with local storage

> Coming soon

#### Server API

Sync state with a backend API

    serverSync = VueSync.websocketStrategy('ws://localhost:8000')
    
    new Vue({
      data: {
        currentPage: 'users',
        users: [{name: 'Stefan'}, {name: 'John'}]
      },
      sync: {
        users: serverSync()
      }
    })

The current implementation of `websocketStrategy` simply sends a JSON message of the format `[key, value]` to the server whenever the state changes. Similarily, when the client receives a message of the form `[key, value]` from the server, the state is updated in the client. A very simple example server can be found here `https://github.com/buhrmi/editor/blob/master/server.js` as a starting point.

#### WebRTC

Sync state with other browsers (WebRTC)

> Coming soon
