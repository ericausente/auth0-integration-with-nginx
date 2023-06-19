# auth0-integration-with-nginx

Auth0 Setup for Nginx OpenID Connect

To set up Auth0 for Nginx OpenID Connect, follow these steps:

Start by referring to the following link for Auth0 setup instructions:
Auth0 Setup Guide
https://github.com/nginx-openid-connect/nginx-oidc-auth0/blob/main/docs/01-Auth0-Setup.md


Take note of the following information from the Auth0 Identity Provider (IDP):
- Domain: dev-12345tm2i6gz0pj.us.auth0.com
- Client ID: YYYYYYYYYYYYYYYYYYY
- Client Secret: e1245hfd-eWCPBIh_yGCK-X-jlLTy__ZjxuIneazzM5iDSJKs8sdhahdkjhsd

Note the following URLs from Auth0 for future reference:
- OAuth Authorization URL: https://dev-12345tm2i6gz0pj.us.auth0.com/authorize
- Device Authorization URL: https://dev-12345tm2i6gz0pj.us.auth0.com/oauth/device/code
- OAuth Token URL: https://dev-12345tm2i6gz0pj.us.auth0.com/oauth/token
- User Info URL: https://dev-12345tm2i6gz0pj.us.auth0.com/userinfo
- OpenID Configuration URL: https://dev-12345tm2i6gz0pj.us.auth0.co/.well-known/openid-configuration
- JSON Web Key URL: https://dev-12345tm2i6gz0pj.us.auth0.com/.well-known/openid-configuration

After setting up Auth0, configure Nginx Plus by following the instructions provided in the main NGINX documentation:

NGINX Auth0 Single Sign-On Deployment Guide
https://docs.nginx.com/nginx/deployment-guides/single-sign-on/auth0/

Clone the Nginx OpenID Connect repository by executing the following command in your home directory:
```
git clone https://github.com/nginxinc/nginx-openid-connect.git
```

Run the following command in your home directory to configure Nginx OpenID Connect:

```
./nginx-openid-connect/configure.sh \
    --auth_jwt_key request \
    --client_id XXXXXXXXnAq5yqVrb5nE1UpPpQennZW \
    --client_secret e1245hfd-eWCPBIh_yGCK-X-jlLTy__ZjxuIneazzM5iDSJKs8sdhahdkjhsd \
    https://dev-12345tm2i6gz0pj.us.auth0.com/.well-known/openid-configuration
```

Edit your frontend.conf file and point the upstream to the backend servers. 
Additionally, modify the listener from the default port 8010 to port 80.

Add the following code snippets to your configuration (don't forget to add the semicolon, as the documentation might be incomplete):

```
location = /_jwks_uri {
    ...
    proxy_set_header Accept-Encoding "gzip";
}

location = /_token {
    ...
    proxy_set_header Accept-Encoding "gzip";
}
```

Copy the following files to the conf.d directory of your Nginx configuration:
- frontend.conf
- openid_connect.js
- openid_connect.server_conf
- openid_connect_configuration.conf

