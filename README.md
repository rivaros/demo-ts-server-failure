### This is demo project to show failure in VSCode TS Server when working with linked node-module packages in monorepo:


1. Clone project


2. Run `npm i`
This will also symlink `ext-library` into node_modules


3. Open `src\index.ts` in VSCode editor, note that `'ext-library/dist/index.js'` is correctly resolved with TS Server, you can ctrl-click to go into `ext-library/src/index.ts`

4. To be on safe side run `TypeScript: Restart TS Server` once from VSCode menu

5. Now run `npm run build:library`

5. Check `src\index.ts` again. `ext-library/dist/index.js` stops resolving. You need to restart TS Server again


### Route of issue

The route of issue is cleaning command `rm -rf ext-library/dist`
It has same behavior when using `tsc --build --clean` when working with projects

TS Server somehow looses connection to the linked library, though it is the same folder `ext-library` still linked in `node_modules`
