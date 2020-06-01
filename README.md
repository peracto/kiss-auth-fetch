# KISS Auth Fetch   
A Simple NodeJs module to append Authorisation header to fetch pipeline

##Purpose

To simplify the process of appending a Authorisation header into a fetch operation.
Rather than append the Authorisation header to each API call, configure the fetcher process to perform this automagically.

##Usage

The module returns a factory function. 

```js
const kissAuthFetch = require('kiss-auth-fetch')

const authFetch = authFetchFactory({
        auth:  Promise.resolve('Bearer xxxxxx/yyyyyy')
    })

// use authFetch as FetchAPI
```

By default, the module assumes that the Fetch API is exposed on the global context. If this is not the case or want to pipeline an alternate to the Fetch API, then define this in the 'fetch' property ...

```js
const kissAuthFetch = require('kiss-auth-fetch')
const nodeFetch = require('none-fetch')

const authFetch = authFetchFactory({
        fetch: nodeFetch,
        auth:  Promise.resolve('Bearer xxxxxx/yyyyyy')
    })

```

##Advanced Usage

```js
const kissAuthFetch = require('kiss-auth-fetch')

const authFetch = authFetchFactory({
        async auth() {
            const key = await getKeyFromDatabase()
            return 'Bearer ' + signJwt('xxxx', key) 
        }       
    })

// use authFetch as FetchAPI
```





