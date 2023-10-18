# Authentication

1. basic authentication
   - send username and password encoded with Base64 in HTTP header
   - e.g.
     - `Authorization: Basic bG9sOnNlY3VyZQ==`
1. Bearer authentication
    - or called token authentication
    - give access to the bearer of this token
    - e.g.
      - `Authorization: Bearer <token>`

1. API key
    - put API key on query string of URL, or aurthoization header
    - machine generate string for the credentials and the API access token
    - not secure
2. 
