# Angular commands:-

```
npm uninstall -g @angular/cli
npm cache clean --force

npm install -g bar
npm install -g angular/cli@3.41
npm install lodash@4.17.4

```
npm install lodash --save --save-exact - installs the latest version and saves the exact version in the dependencies in the package.json.


npm install lodash --save-dev --save-exact - installs the latest version and saves the exact version in the devDependencies map in the package.json.


npm install lodash --save - installs the latest version and saves the semantic range in the dependencies in the package.json. E.g. "lodash": "^4.17.4".


Caveats
Specifying --save-exact alone is not sufficient. You need to define either --save or --save-dev and --save-exact. For example,

npm install mocha --save-dev --save-exact or npm install lodash --save --save-exact

--save, --save-exact, --save-dev obviously don’t work together with the -g flag which installs the module globally.


To fix this install the specific typescript version 3.1.6
```
npm i typescript@3.1.6 --save-dev --save-exact
```

