# Plug'n'Play approach seems not to work

Occurred on WSL (**Ubuntu 24.04.2 LTS**)
```bash
$ node -v
v18.19.1

$ npm -v
11.4.2

$ pnpm -v
10.12.4
```
Also on **Windows 10 IoT Enterprise LTSC 21H2 build 19044.5965**
```bash
> node -v
v24.3.0

> npm -v
11.4.2

> pnpm -v
10.12.4
```

I'm basically failing at the simpliest thing...

```bash
pnpm init
pnpm create @eslint/config@latest
```

However, this is because I am using **Plug'n'Play**:
```bash
pnpm config set node-linker pnp
pnpm config set symlink false
```
I am aware it is recommended to set the `node-linker` to `hoisted`. However, is it **needed**?

I added these *phantom dependecies* manually:
- eslint-scope
- estraverse
- esrecurse
- eslint-visitor-keys
- espree
- acorn
- acorn-jsx
- @eslint/eslintrc

And eventually got:
```
Oops! Something went wrong! :(

ESLint: 9.30.0

Error: require() of ES Module /mnt/d/EslintTest/node_modules/.pnpm/@eslint+eslintrc@3.3.1/node_modules/@eslint/eslintrc/universal.js from /mnt/d/EslintTest/node_modules/.pnpm/eslint@9.30.0/node_modules/eslint/lib/linter/linter.js not supported.
Instead change the require of universal.js in /mnt/d/EslintTest/node_modules/.pnpm/eslint@9.30.0/node_modules/eslint/lib/linter/linter.js to a dynamic import() which is available in all CommonJS modules.
    at require$$0.Module._extensions..js (/mnt/d/EslintTest/.pnp.cjs:8210:17)
    at Module.load (node:internal/modules/cjs/loader:1197:32)
    at Module._load (node:internal/modules/cjs/loader:1013:12)
    at require$$0.Module._load (/mnt/d/EslintTest/.pnp.cjs:8061:31)
    at Module.require (node:internal/modules/cjs/loader:1225:19)
    at require (node:internal/modules/helpers:177:18)
    at Object.<anonymous> (/mnt/d/EslintTest/node_modules/.pnpm/eslint@9.30.0/node_modules/eslint/lib/linter/linter.js:25:6)
    at Module._compile (node:internal/modules/cjs/loader:1356:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1414:10)
    at require$$0.Module._extensions..js (/mnt/d/EslintTest/.pnp.cjs:8214:35)
```

## The config used to initialize project
✔ What do you want to lint? · __**javascript**__, __**json**__, __**css**__
✔ How would you like to use ESLint? · __**problems**__
✔ What type of modules does your project use? · __**esm**__
✔ Which framework does your project use?  __**react**__
✔ Does your project use TypeScript? · no / __**yes**__
✔ Where does your code run? · __**browser**__, __**node**__
The config that you've selected requires the following dependencies:

eslint, @eslint/js, globals, typescript-eslint, eslint-plugin-react, @eslint/json, @eslint/css
✔ Would you like to install them now? · No / __**Yes**__
✔ Which package manager do you want to use? · __**pnpm**__

## How to run?
```
pnpm lint
```