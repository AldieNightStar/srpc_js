# WS - SRPC JS - For browser

# Install
```html
<script type="application/javascript" src="https://aldienightstar.github.io/socketer_js/wsocketer.js"></script>
<script type="application/javascript" src="https://aldienightstar.github.io/srpc_js/srpc.js"></script>
```

# Server
```js
let server = srpc.newServer(8080, "MyPassword")
```

# Client
```js
// Can throw Erorr when name is busy or password is incorrect
let client = await srpc.newClient("ws://localhost:8080", "MyPassword", "NAME");

// Register new remote function
// sender - Caller name
// arg1, arg2, arg3 ... - Arguments (string | array | object)
// to send response to client - just return something by this function
client.funcs.someFunc = function(sender, arg1, arg2, arg3) {};
```

```js
// ===============================================
// ===============================================

// Let's open communication with "Service1"
let s1 = client.of("Service1")

// Call "Service1" functions
// Response can be (string | array | object)
let resp = await s1.call("someFunc", arg1, arg2, arg3 ...);
let resp = await s1.call( "func2"  , arg1, arg2, arg3 ...);
let resp = await s1.call( "func3"  , arg1, arg2, arg3 ...);

// ===============================================
// ===============================================

// Call "Service1" functions without "of" functions
// Response can be (string | array | object)
let resp = await client.callOf("Service1", "someFunc", arg1, arg2, arg3 ...);


// Get other client names from server
let list = await client.getOthers();

// Disconnect from server
client.close();
```

