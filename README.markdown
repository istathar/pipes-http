An HTTP client
==============

An HTTP client library for Haskell for the Pipes ecosystem

A common case in writing RESTful web services is needing to make onward calls
to further servers. This package is intended to make this easy to do.

Example
-------

The underlying API is very simple:

```haskell
main :: IO ()
main = do
    c <- openConnection "www.example.com" 80
    
    q <- buildRequest $ do
        http GET "/"
        setAccept "text/html"
    
    sendRequest c q emptyBody
    
    receiveResponse c (\p i -> do
	...)
    
    closeConnection c
```

There are also convenience functions for the common case of making
straight-forward GET and POST requests; for instance:

```haskell
    get "http://www.example.com/" (\_ i -> ...)
```

will _{ahem}_ stream the response body to stdout. Perhaps more
interesting (though less streams-oriented), is simply getting the
response as a ByteString using one of the pre-defined handlers:

```haskell
    x' <- get "https://secure.example.com/" concatHandler
```

See the documentation in
[Network.Http.Client](http://research.operationaldynamics.com/projects/pipes-http/doc/Network-Http-Client.html)
for further examples and details of usage of the API.

Change Log
---------

Recent API changes:

* _v0.1.0_  
	Initial fork from **http-streams**.

AfC

