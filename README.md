# Serverless Geolocation

A bundle of serverless functions designed to allow user geolocation and actions based on that detection.

For more info, see [Geo-fencing Users With Lambda @ Edge and CloudFront](https://medium.com/@alfonso.gober.jr/geo-fencing-users-with-lambda-edge-and-cloudfront-2eb32b531f51)

## Quick Start

### Install

```
git clone git@github.com:alfonsogoberjr/serverless-geolocation.git
cd serverless-geolocation && npm install
```

### Deploy

```
serverless deploy --stage dev
```

## Functions

### edgeRedirect

Lambda @ Edge function that redirects users to countrycode.yourdomain.com

For example, a user in Shanghai will be redirected to cn.yourdomain.com, and a user in Amsterdam will be redirected to nl.yourdomain.com.

### countryLookup

Standard Lambda-Proxy API-Gateway integration that performs a lookup using MaxMind's GeoIP data (open-source). 

```
serverless invoke local -f countryLookup --data '{ "requestContext": { "identity": { "sourceIp": "185.104.185.86" } } }' --stage dev
```

## License

[Creative Commons Attribution-ShareAlike 4.0 International License](LICENSE.txt)
