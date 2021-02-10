# A sample nextjs app to demonstrate the effectiveness of a PR

Sample was made following the instructions listed here: https://github.com/vercel/next.js/tree/canary/examples/with-next-page-transitions

The pull request in question removes the restriction that prohibits us from using `.` as a `basePath`. Over at CERN, we need to be able to host multiple versions of exactly the same statically exported web site, on the same domain. Think like this:

https://department.cern.ch/group/service1/

https://department.cern.ch/group/service2/

https://department.cern.ch/group/service3/

... we have about 10 different services.

A static export is about 100MB. Exporting and deploying all 10 versions with the only difference of `basePath` adds up to 10GB of websites and seems very inefficient. Therefore, we suggest to lift this restriction: https://github.com/vercel/next.js/blob/canary/packages/next/next-server/server/config.ts#L222-L226 and allow a `.` to be a valid `basePath` value. This ensures that all static dependencies are taken using relative paths.

A small adjustment was made to this example: hrefs were changed to contain `.html` suffix to ensure correct routing.

# How to run:

``` bash
# Export a static version of the webpage (to out/ directory)
npm run build

# Serve it with your favourite web server
python -m SimpleHTTPServer
```

Now navigate to `localhost:8000/out/index.html`. Navigate to back and forth between pages to ensure that prefix `out` remains in the url, and static files load correctly.

