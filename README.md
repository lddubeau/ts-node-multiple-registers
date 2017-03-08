1. `npm install`

2. `gulp`

This fails with:

```
$ gulp
[08:58:44] Requiring external module ts-node/register

/home/ldd/src/git-repos/ts-node-multiple-registers/node_modules/ts-node/src/index.ts:319
          throw new TSError(formatDiagnostics(diagnosticList, cwd, ts, lineOffset))
                ^
TSError: ⨯ Unable to compile TypeScript
gulptasks/task.ts (2,23): Cannot find name 'exports'. (2304)
gulptasks/task.ts (3,1): Cannot find name 'exports'. (2304)
    at getOutput (/home/ldd/src/git-repos/ts-node-multiple-registers/node_modules/ts-node/src/index.ts:319:17)
    at /home/ldd/src/git-repos/ts-node-multiple-registers/node_modules/ts-node/src/index.ts:350:18
    at Object.compile (/home/ldd/src/git-repos/ts-node-multiple-registers/node_modules/ts-node/src/index.ts:483:19)
    at Module.m._compile (/home/ldd/src/git-repos/ts-node-multiple-registers/node_modules/ts-node/src/index.ts:413:44)
    at Module.m._compile (/home/ldd/src/git-repos/ts-node-multiple-registers/node_modules/ts-node/src/index.ts:413:23)
    at Module._extensions..js (module.js:579:10)
    at require.extensions.(anonymous function) (/home/ldd/src/git-repos/ts-node-multiple-registers/node_modules/ts-node/src/index.ts:416:12)
    at Object.require.extensions.(anonymous function) [as .ts] (/home/ldd/src/git-repos/ts-node-multiple-registers/node_modules/ts-node/src/index.ts:416:12)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)
    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/home/ldd/src/git-repos/ts-node-multiple-registers/gulpfile.ts:2:1)
    at Module._compile (module.js:570:32)
    at Module.m._compile (/home/ldd/src/git-repos/ts-node-multiple-registers/node_modules/ts-node/src/index.ts:413:23)
```

Commenting out the lines that use `karma` in `gulpfile.ts` makes the code run fine. (Gulp complains that there's no `default` task but there's no compilation error.)

Commenting out the registration of `ts-node` in Karma's source also makes the problem go away.

The `externals.d.ts` file is there to give `karma` some TypeScript definition without having to rely on `@types`. (Emphasizing the "minimal" in "Minimal, Complete and Verifiable Example".)
