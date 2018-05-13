# Serverless Geolocation

A bundle of serverless functions designed to allow user geolocation and actions based on that detection.

This service consists of two functions:

### edgeRedirect

Lambda @ Edge function that redirects users to countrycode.yourdomain.com

For example, a user in Shanghai will be redirected to cn.yourdomain.com, and a user in Amsterdam will be redirected to nl.yourdomain.com.

### countryLookup

Standard Lambda-Proxy API-Gateway integration that performs a lookup using MaxMind's GeoIP data (open-source). 

```
serverless invoke local -f countryLookup --data '{ "requestContext": { "identity": { "sourceIp": "185.104.185.86" } } }' --stage dev
```

# License

[Creative Commons Attribution-ShareAlike 4.0 International License](LICENSE.txt)
