This is just like an XSS on a traditional web app, here inputs ends up on web view.
Finding these instances can be tricky, but looking for instances of the `loadUrl` or `evaluatejavascript` methods would be a good start. Trace backwards from these calls to determine if the parameters come from an insecure source. 

