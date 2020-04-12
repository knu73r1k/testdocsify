# A Test Repo

This repo is used to test Azure Web Apps deployment, using GitHub Actions. Deployment to a Azure WebApps container  targeted as `node.js` app / container.

## The use case

Deploy a GitHub repo, which contains markdown files and thus use `docsify`for serving it as a web site

To serve markdown files as a website using `docsify`, you need what's documented in the `index.html` file. You also need a web server to serve the files. In my use case - e.g. the `light-server`, hence the startup script in `package.json` file - `light-server -s . -p 8080"`.

For some odd reason, Azure Web Apps deployment scripts, does not fire off the `npm install` which would install the dependencies and serve files with `light-server`.

## Workaround

I struggeled with trigger a `npm install` to ensure dependencies in the `package.json` are installed. The workaround was to use the `.deployment` and `deploy.sh`files, which _Kudu_ is using. More on [Kudu here](https://github.com/projectkudu/kudu/wiki/Deployment).

## GitHub Issue

My issue related to this test repo is documented in [this GitHub issue](https://github.com/microsoft/Oryx/issues/545), which started out as a question to a configuration property. The issue is related to the [Oryx](https://github.com/microsoft/Oryx) repository, which is the build system behind Azure Web Apps containers.

## On a side note

If you deploy this repository using `PHP` as the target platform in Azure Web Apps, this works without any of the workaround. This because a web server just serves your files, starting with the `index.html`. 