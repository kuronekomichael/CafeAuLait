# Cafe Au Lait
Cafe Au Lait is a Node.js [Remember the Milk](rememberthemilk.com) library written in CoffeeScript.

## Installation
You can install Cafe Au Lait via NPM:
`npm install cafe-au-lait` (or similar in your package.json file).

You can also clone/download the repo; all that's required is RememberTheMilk.coffee/.js and the npm dependencies in the node_modules directory.

## Getting set up
```
RememberTheMilk = require('cafe-au-lait');
rtm = new RememberTheMilk(api_key, secret_key)
```


## Authentication
Initial authentication with the RTM api is a bit complex. For more info, see https://www.rememberthemilk.com/services/api/authentication.rtm.

Currently, Cafe Au Lait only supports authenticating as a desktop application. Here's an example of a simple CoffeeScript command-line application that authenticates.

```
RememberTheMilk = require('cafe-au-lait');
rtm = new RememberTheMilk(api_key, secret_key)
rtm.getAuthUrl (url) ->
  console.log "Before continuing, you need to authenticate with Remember The Milk."
  console.log "Go to the following URL, allow access, and then press any key in this terminal window:"
  console.log url
  
  stdin.resume()
  stdin.on 'data', ->
    rtm.getAuthToken (token) ->
      # At this point, the user is authenticated and can perform any action
```

If you have a token persisted from a previous request, you can load it into the RTM object by passing in a token in the constructor. It will be used for all future API requests.

`rtm = new RememberTheMilk(api_key, secret_key, token)`

You can also manually set it after creation:

```
rtm = new RememberTheMilk(api_key, secret_key)
rtm.token = 'a valid token'
```

## Performing API actions
The `get` method allows you to perform any API actions listed on https://www.rememberthemilk.com/services/api/methods/.

```
RememberTheMilk = require('cafe-au-lait');
rtm = new RememberTheMilk(api_key, secret_key)
rtm.token = 'a valid token'
rtm.get 'rtm.lists.getList', (response) ->
  console.log response
  # => { stat: 'ok',
  # lists:
  # { list:
  #    [ { id: 'list id',
  #     name: 'Inbox',
  #     deleted: '0',
  #     locked: '1',
  #     archived: '0',
  #     position: '-1',
  #     smart: '0',
  #     sort_order: '0' }, ...]
  #   }
  # }
```

## Warning
Consider this alpha software; use at your own risk. In particular, there is very little (read: no) error handling code. 

## Contributing
If you want to fork this and jam on it, feel free to shoot me a pull request. I'll happily respond to any questions you may have as well.

There's basic test coverage via jasmine-node. To run the tests, execute `npm test` from the root directory.

## License
Cafe Au Lait is licensed under the MIT License
(C) 2013 Michael Walker

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
