- implicit grants is one such vulnerability, with this the application will request an access token from the OAuth provider which will be  send back as the part of the  url this can lead to token leak issues 
- if you see a response type=token in an OAuth url, that is an implicit grant and is always considered to be a bad idea.
- Instead, use the standard Auth authorisation flow, via response_type=code.
