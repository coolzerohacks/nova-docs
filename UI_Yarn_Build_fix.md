🛠️ Nova UI Build Fix Log

    Diagnosed Registry Errors

        Yarn 1.22 was failing with info There appears to be trouble with the npm registry

        Confirmed DNS, curl, and node access were functional

        Isolated problem to Yarn and Node fetch behavior inside and outside Docker

    Upgraded Yarn to v4 Using Corepack

        Installed corepack globally

        Ran:

corepack enable
corepack prepare yarn@stable --activate

Exported Corepack Yarn path:

    export PATH="$(corepack where yarn)/bin:$PATH"

Reset Yarn Registry

    Set Yarn to use reliable NPM registry:

    yarn config set npmRegistryServer https://registry.npmjs.org

Migrated to Yarn 4 in Docker

    Updated Dockerfile:

        Enabled Corepack

        Set registry and nodeLinker node-modules

        Replaced yarn global with local dev install of serve

        Removed yarn add in Dockerfile; handled all deps via package.json

Fixed Build Errors

    Added missing dependency rollup:

yarn add -D rollup

Disabled Plug’n’Play in Docker:

    RUN yarn config set nodeLinker node-modules

Final Cleanup

    Verified Docker image builds cleanly

    UI successfully runs in container via serve
