<h1 align="center">
  <br>
  tooling
  <br>
</h1>

<p align="center"><a href="https://www.npmjs.com/package/@google/dscc-gen"><img src="https://img.shields.io/npm/v/@google/dscc-gen.svg" alt="npm Version"></a> <a href="https://npmcharts.com/compare/@google/dscc-gen?minimal=true"><img src="https://img.shields.io/npm/dw/@google/dscc-gen.svg" alt="npm Downloads"></a> <a href="http://packagequality.com/#?package=%40google%2Fdscc-gen"><img src="http://npm.packagequality.com/shield/%40google%2Fdscc-gen.svg" alt="Package Quality"></a> <a href="https://github.com/google/clasp"><img src="https://img.shields.io/badge/built%20with-clasp-4285f4.svg" alt="Built with Clasp"></a></p>

Tooling for [Data Studio Developer Features]

## /!\ WARNING /!\
* you NEED to install YARN before using this.
* contains a hack to bypass bucket ACL checks, as for now I DON'T have access to any public bucket. And it seems I won't sadly (so won't be able to officialy use those toolings ...)
* I have tested all the usage below with the YARN package manager instead of the NPM one. NPM did work if manually linking the modified package, but did break on every single "npm install" or "npm link" command, and it seems that YARN works just fine (yarn install does not break a link already there, and yarn link does not delete packages already there). 
* ~~still use "npm run xxx" for every viz usage, as my fix doesn't work with yarn (I declare global variables based on NPM's injected variables, which are not the same as yarn it seems).~~

## USAGE :
1. git clone this repository
```
git clone https://github.com/aschor/datastudio-tooling.git
git checkout fix_to_work
#cd datastudio-tooling  #not needed anymore
#export TOOLING=$PWD    #not needed anymore
```
2. build dscc-scripts and link it
```
cd dscc-scripts
yarn
yarn build
yarn install
yarn link
```
3. build dscc-gen and link it
```
cd ../dscc-gen
yarn
yarn build
yarn install
yarn link @google/dscc-scripts
yarn link #makes the command globaly available
```
4. create your vizualisation :
```
cd WHEREVER_YOU_STORE_YOUR_DATA
dscc-gen viz #enter your answers here
cd $YOUR_VIZ_PROJECT_NAME
#npm install
#rm -rf node_modules/@google/dscc-scripts
#ln -s $TOOLING/packages/dscc-scripts -t node_modules/@google/
#yarn install
yarn link @google/dscc-scripts
yarn run start  #or :
#yarn run update_message
```

## What's in this repo

[ds-component]:
+ A helper library for [community visualization] development.

[dscc-scripts]:
+ Scripts to simplify deployment of Data Studio developer projects.

[dscc-gen]:
+ An opinionated templating tool to bootstrap community connectors or community visualizations.

Review the README for each package to learn more.

## Developer notes
- The top-level `package.json` and `yarn.lock` exist to make sure that yarn is
  available in our travis environment.

[Data Studio Developer Features]: https://developers.google.com/datastudio/
[ds-component]: ./packages/ds-component/
[dscc-scripts]: ./packages/dscc-scripts/
[dscc-gen]: ./packages/dscc-gen/
[community visualization]: https://developers.google.com/datastudio/visualization
