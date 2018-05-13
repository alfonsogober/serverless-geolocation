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

After a few minutes, you should see

```
Serverless: Packaging service...
Serverless: Excluding development dependencies...
Serverless: Uploading CloudFormation file to S3...
Serverless: Uploading artifacts...
Serverless: Uploading service .zip file to S3 (1.66 MB)...
Serverless: Validating template...
Serverless: Updating Stack...
Serverless: Checking Stack update progress...
....................
Serverless: Stack update finished...
Service Information
service: geolocation
stage: dev
region: us-east-1
stack: geolocation-dev
api keys:
  dev-geolocation-apikey: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
endpoints:
  GET - https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/dev/
functions:
  edgeRedirect: geolocation-dev-edgeRedirect
  countryLookup: geolocation-dev-countryLookup
```

Save the apikey and the GET URL somewhere; you’ll need it to access your lookup endpoint.

You should be able to curl your new endpoint now:

```
curl -H "X-Api-Key:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/dev/
```

You should see

```
{"iso_code":"US","is_in_european_union":false}
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
