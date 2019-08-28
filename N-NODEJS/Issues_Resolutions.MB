# Issues - Resolutions NPM

### Issue -  error code UNABLE_TO_GET_ISSUER_CERT_LOCALLY

```
-- error log
35 verbose node v10.16.3
36 verbose npm  v6.9.0
37 error code UNABLE_TO_GET_ISSUER_CERT_LOCALLY
38 error errno UNABLE_TO_GET_ISSUER_CERT_LOCALLY
39 error request to https://registry.npmjs.org/client-sessions failed, reason: unable to get local issuer certificate
```
<b>Solution</b>
A quick solution from the internet search was npm config set strict-ssl false, luckily it worked. But as a part of my work environment, I am restricted to set the strict-ssl flag to false.

Later I found a safe and working solution,
```
npm config set registry http://registry.npmjs.org/  
```
this worked perfectly and I got a success message Happy Hacking! by not setting the strict-ssl flag to false.
