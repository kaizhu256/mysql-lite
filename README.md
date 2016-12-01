mysql-lite
==========
this is the zero-dependency version of mysql v2.12.0

[![travis-ci.org build-status](https://api.travis-ci.org/kaizhu256/node-mysql-lite.svg)](https://travis-ci.org/kaizhu256/node-mysql-lite)

[![NPM](https://nodei.co/npm/mysql-lite.png?downloads=true)](https://www.npmjs.com/package/mysql-lite)

[![package-listing](https://kaizhu256.github.io/node-mysql-lite/build/screen-capture.gitLsTree.svg)](https://github.com/kaizhu256/node-mysql-lite)



# documentation
#### api-doc
- [https://kaizhu256.github.io/node-mysql-lite/build..beta..travis-ci.org/doc.api.html](https://kaizhu256.github.io/node-mysql-lite/build..beta..travis-ci.org/doc.api.html)

[![api-doc](https://kaizhu256.github.io/node-mysql-lite/build..beta..travis-ci.org/screen-capture.docApiCreate.browser._2Fhome_2Ftravis_2Fbuild_2Fkaizhu256_2Fnode-mysql-lite_2Ftmp_2Fbuild_2Fdoc.api.html.png)](https://kaizhu256.github.io/node-mysql-lite/build..beta..travis-ci.org/doc.api.html)

#### todo
- upgrade to mysql v2.12.1 when available
- add extra tests
- none

#### change since 9fe8c225
- npm publish 2016.11.1
- none

#### this package requires
- darwin or linux os



# build-status [![travis-ci.org build-status](https://api.travis-ci.org/kaizhu256/node-mysql-lite.svg)](https://travis-ci.org/kaizhu256/node-mysql-lite)
[![build commit status](https://kaizhu256.github.io/node-mysql-lite/build/build.badge.svg)](https://travis-ci.org/kaizhu256/node-mysql-lite)

| git-branch : | [master](https://github.com/kaizhu256/node-mysql-lite/tree/master) | [beta](https://github.com/kaizhu256/node-mysql-lite/tree/beta) | [alpha](https://github.com/kaizhu256/node-mysql-lite/tree/alpha)|
|--:|:--|:--|:--|
| test-report : | [![test-report](https://kaizhu256.github.io/node-mysql-lite/build..master..travis-ci.org/test-report.badge.svg)](https://kaizhu256.github.io/node-mysql-lite/build..master..travis-ci.org/test-report.html) | [![test-report](https://kaizhu256.github.io/node-mysql-lite/build..beta..travis-ci.org/test-report.badge.svg)](https://kaizhu256.github.io/node-mysql-lite/build..beta..travis-ci.org/test-report.html) | [![test-report](https://kaizhu256.github.io/node-mysql-lite/build..alpha..travis-ci.org/test-report.badge.svg)](https://kaizhu256.github.io/node-mysql-lite/build..alpha..travis-ci.org/test-report.html)|
| coverage : | [![istanbul coverage](https://kaizhu256.github.io/node-mysql-lite/build..master..travis-ci.org/coverage.badge.svg)](https://kaizhu256.github.io/node-mysql-lite/build..master..travis-ci.org/coverage.html/index.html) | [![istanbul coverage](https://kaizhu256.github.io/node-mysql-lite/build..beta..travis-ci.org/coverage.badge.svg)](https://kaizhu256.github.io/node-mysql-lite/build..beta..travis-ci.org/coverage.html/index.html) | [![istanbul coverage](https://kaizhu256.github.io/node-mysql-lite/build..alpha..travis-ci.org/coverage.badge.svg)](https://kaizhu256.github.io/node-mysql-lite/build..alpha..travis-ci.org/coverage.html/index.html)|
| build-artifacts : | [![build-artifacts](https://kaizhu256.github.io/node-mysql-lite/glyphicons_144_folder_open.png)](https://github.com/kaizhu256/node-mysql-lite/tree/gh-pages/build..master..travis-ci.org) | [![build-artifacts](https://kaizhu256.github.io/node-mysql-lite/glyphicons_144_folder_open.png)](https://github.com/kaizhu256/node-mysql-lite/tree/gh-pages/build..beta..travis-ci.org) | [![build-artifacts](https://kaizhu256.github.io/node-mysql-lite/glyphicons_144_folder_open.png)](https://github.com/kaizhu256/node-mysql-lite/tree/gh-pages/build..alpha..travis-ci.org)|

#### master branch
- stable branch
- HEAD should be tagged, npm-published package

#### beta branch
- semi-stable branch
- HEAD should be latest, npm-published package

#### alpha branch
- unstable branch
- HEAD is arbitrary
- commit history may be rewritten



# package.json
```json
{
    "package.json": true,
    "author": "kai zhu <kaizhu256@gmail.com>",
    "description": "{{packageJson.description}}",
    "devDependencies": {
        "electron-lite": "kaizhu256/node-electron-lite#alpha",
        "utility2": "kaizhu256/node-utility2#alpha"
    },
    "license": "MIT",
    "main": "lib.mysql",
    "name": "mysql-lite",
    "os": ["darwin", "linux"],
    "repository": {
        "type": "git",
        "url": "https://github.com/kaizhu256/node-mysql-lite.git"
    },
    "scripts": {
        "build-ci": "utility2 shRun shReadmeBuild",
        "postinstall": "\
for DIR in .bin electron-lite utility2; \
do \
    (if [ -d node_modules/$DIR ] && [ ! -d $DIR ]; then mv node_modules/$DIR .; fi); \
done; \
rm -fr node_modules && ln -s . node_modules",
        "start": "\
export PORT=${PORT:-8080} && \
export npm_config_mode_auto_restart=1 && \
utility2 shRun shIstanbulCover test.js",
        "test": "export PORT=$(utility2 shServerPortRandom) && utility2 test test.js"
    },
    "version": "2016.11.1"
}
```



# changelog of last 50 commits
[![screen-capture](https://kaizhu256.github.io/node-mysql-lite/build/screen-capture.gitLog.svg)](https://github.com/kaizhu256/node-mysql-lite/commits)



# internal build-script
- build.sh
```shell
# build.sh

# this shell script will run the build for this package

shBuildCiTestPre() {(set -e
# this function will run the pre-test build
    # test published-package
    (export MODE_BUILD=npmTestPublished &&
        shRunScreenCapture shNpmTestPublished) || return $?
)}

shBuild() {(set -e
# this function will run the main build
    # init env
    . node_modules/.bin/utility2 && shInit
    # cleanup github-gh-pages dir
    # export BUILD_GITHUB_UPLOAD_PRE_SH="rm -fr build"
    # init github-gh-pages commit-limit
    export COMMIT_LIMIT=16
    # if branch is alpha, beta, or master, then run default build
    if [ "$CI_BRANCH" = alpha ] ||
        [ "$CI_BRANCH" = beta ] ||
        [ "$CI_BRANCH" = master ]
    then
        shBuildCiDefault
    fi
)}
shBuild
```
