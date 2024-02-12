# Documentation: Fixing Internet Identity Local Deployment Issue on Chrome

## Overview

This document aims to assist developers encountering a specific issue when integrating Internet Identity with their applications, particularly those using Next.js or similar frameworks. The issue manifests as a blank white screen and a console error in Google Chrome, but not in Firefox.

## Problem Description

When deploying Internet Identity locally, you may encounter an error in Chrome (but not Firefox) characterized by a blank white screen and the following console error:

```
GET http://127.0.0.1:4943/spa.js net::ERR_ABORTED 400 (Bad Request)
```

This issue is caused by using an incorrect URL format for accessing the Internet Identity service locally:
```
http://127.0.0.1:4943/?canisterId=bd3sg-teaaa-aaaaa-qaaba-cai
```

## Solution

The solution to this problem involves changing the URL format used to access the Internet Identity service when working locally. The correct URL format is as follows:
```
http://<II_CANISTER_ID>.localhost:4943/
```
For example, for the canister ID `bd3sg-teaaa-aaaaa-qaaba-cai`, the URL would be:
```
http://bd3sg-teaaa-aaaaa-qaaba-cai.localhost:4943/
```

### Steps to Implement the Fix

1. **Make the Internet Identity URL Available in the Build Process**: Modify your application's build process to use different Internet Identity URLs depending on the deployment environment—locally or on the mainnet.
    - **Locally**: Use the URL format `http://<II_CANISTER_ID>.localhost:4943/`.
    - **On Mainnet**: Use the URL `https://identity.ic0.app`.

2. **Adjust for Browser Compatibility**: Note that Safari and some other browsers do not support subdomains on localhost. For these browsers, you can use the original format `http://localhost:4943/?canisterId=<II_CANISTER_ID>`. However, this is not compatible with Chrome.

3. **Modify the IDENTITY_PROVIDER URL**: In your application, locate where you are instantiating the `IDENTITY_PROVIDER` URL. Replace it with the correct URL format based on your deployment environment. This step is crucial for ensuring that your application communicates correctly with the Internet Identity service.

    - For projects using webpack, this might involve editing the `webpack.config.js` file. However, for Next.js or similar frameworks, this configuration will be located in a different part of your project structure, likely where environment variables or project settings are defined.

## Conclusion

Following the above steps should resolve the issue with Internet Identity local deployment on Chrome, enabling your application to integrate seamlessly with Internet Identity across different browsers and environments. Remember to test your application in multiple browsers to ensure compatibility and a smooth user experience.