# api documentation for  [gulp-install (v1.1.0)](https://github.com/slushjs/gulp-install)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-install.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-install) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-install.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-install)
#### Automatically install npm, bower, tsd, and pip packages/dependencies if the relative configurations are found in the gulp file stream respectively

[![NPM](https://nodei.co/npm/gulp-install.png?downloads=true)](https://www.npmjs.com/package/gulp-install)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-install/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp-install_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-install/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-install/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-install/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Joakim Carlstein",
        "email": "joakim@klei.se"
    },
    "bugs": {
        "url": "https://github.com/slushjs/gulp-install/issues"
    },
    "dependencies": {
        "dargs": "^5.1.0",
        "gulp-util": "^3.0.7",
        "lodash.groupby": "^4.6.0",
        "p-queue": "^1.0.0",
        "through2": "^2.0.3",
        "which": "^1.2.14"
    },
    "description": "Automatically install npm, bower, tsd, and pip packages/dependencies if the relative configurations are found in the gulp file stream respectively",
    "devDependencies": {
        "chai": "^3.2.0",
        "mocha": "^3.2.0",
        "standard-version": "^4.0.0",
        "xo": "^0.18.0"
    },
    "directories": {},
    "dist": {
        "shasum": "9386b46cb4669b47257b6adf4e3ea2e83c928a1a",
        "tarball": "https://registry.npmjs.org/gulp-install/-/gulp-install-1.1.0.tgz"
    },
    "gitHead": "f2696f84ab05a314c2fd79aa3563889505fb2008",
    "homepage": "https://github.com/slushjs/gulp-install",
    "keywords": [
        "gulpplugin",
        "bower",
        "npm",
        "install"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "joakimbeng",
            "email": "joakim@klei.se"
        }
    ],
    "name": "gulp-install",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/slushjs/gulp-install.git"
    },
    "scripts": {
        "test": "NODE_ENV=test mocha -R spec"
    },
    "version": "1.1.0",
    "xo": {
        "space": true
    }
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-install](#apidoc.module.gulp-install)
1.  object <span class="apidocSignatureSpan">gulp-install.</span>command_runner

#### [module gulp-install.command_runner](#apidoc.module.gulp-install.command_runner)
1.  [function <span class="apidocSignatureSpan">gulp-install.command_runner.</span>run (command)](#apidoc.element.gulp-install.command_runner.run)



# <a name="apidoc.module.gulp-install"></a>[module gulp-install](#apidoc.module.gulp-install)



# <a name="apidoc.module.gulp-install.command_runner"></a>[module gulp-install.command_runner](#apidoc.module.gulp-install.command_runner)

#### <a name="apidoc.element.gulp-install.command_runner.run"></a>[function <span class="apidocSignatureSpan">gulp-install.command_runner.</span>run (command)](#apidoc.element.gulp-install.command_runner.run)
- description and source-code
```javascript
run = function (command) {
  return new Promise((resolve, reject) => {
    which(command.cmd, (err, cmdpath) => {
      if (err) {
        return reject(new Error('Can't install! "${command.cmd}" doesn't seem to be installed.'));
      }
      const cmd = spawn(quoteIfNecessary(cmdpath), command.args, {shell: true, stdio: 'inherit', cwd: command.cwd || process.cwd
()});
      cmd.on('close', code => {
        if (code !== 0) {
          return reject(new Error('"${command.cmd}" exited with non-zero code ${code}'));
        }
        resolve();
      });
    });
  });
}
```
- example usage
```shell
...
        log('Skipping install.', 'Run '' + gutil.colors.yellow(formatCommands(toRun)) + '' manually');
        return cb();
      }
      const groupedCommands = groupBy(toRun, 'cmd');
      Promise.all(Object.keys(groupedCommands).map(cmd => {
        const commands = groupedCommands[cmd];
        const queue = new PQueue({concurrency: 1});
        return Promise.all(commands.map(command => queue.add(() => logFailure(command)(commandRunner.run(command)))));
      }))
      .then(() => done())
      .then(() => cb(), cb); // eslint-disable-line promise/no-callback-in-promise
    }
  );
};
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
