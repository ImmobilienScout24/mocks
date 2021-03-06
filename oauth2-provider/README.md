# OAuth2 Authorization Server Mock

Supports Implicit,  Client Credentials and Password Grants.

## Usage

With node

    git checkout https://github.com/zalando-stups/mocks/tree/master/oauth2-provider
    cd oauth2-provider/src
    node server.js

With Docker

    docker run -it -p 3000:3000 -e CLIENTS=c1=s1 -e USERS=u1=p1 stups/mock-oauth2-provider

### Accepted environment variables

* `CLIENTS`: Comma-separated list of accepted client IDs and secrets, e.g. `"client1=secret1,client2=secret2"`.
* `USERS`: Needed for the `password` grant. Same format as `CLIENTS`.
* `DEFAULT_REALM`: Default realm to use if none was specified (default is "employees").

## API

See [swagger.yml](swagger.yml).

Example usage to generate a new access token:


    $ cat > request.json << "EOF"
    {
        "grant_type": "password",
        "username": "my-username",
        "password": "my-password",
        "scope": "uid sales_order.read_all"
    }
    EOF

    $ curl -X POST -u my-client-id:my-client-secret -d @request.json -H Content-Type:application/json "http://localhost:3000/access_token?realm=services"

## Building

    docker build -t stups/mock-oauth2-provider .
