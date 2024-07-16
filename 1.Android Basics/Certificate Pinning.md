

SSL Certificate pinning is where an app has a known list of valid SSL certificates for a domain (or a set of domains).

Then, when making HTTPS connections from the device, it ensures that the certificates from the server match what they are set to in the application. 

If the cert from the server doesn't match the list of pre-approved certificates, the device drops the connection and throws an SSL error.