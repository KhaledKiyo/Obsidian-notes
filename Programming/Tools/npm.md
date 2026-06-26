#programing #devtools #javascript
[[Node.js]]
## setup

npm comes bundled with node.js. check version

```bash
npm --version
```

update npm itself

```bash
npm install -g npm@latest
```

---

## project

create a new `package.json`

```bash
npm init
```

create it without the prompts

```bash
npm init -y
```

---

## installing packages

install a package and save to `dependencies`

```bash
npm install <package>
```

install a dev-only package and save to `devDependencies`

```bash
npm install <package> --save-dev
```

install a package globally

```bash
npm install -g <package>
```

install all packages from an existing `package.json`

```bash
npm install
```

---

## removing packages

remove a package

```bash
npm uninstall <package>
```

remove a global package

```bash
npm uninstall -g <package>
```

---

## updating packages

check outdated packages

```bash
npm outdated
```

update all packages

```bash
npm update
```

update a specific package

```bash
npm update <package>
```

---

## running scripts

scripts are defined in `package.json` under `"scripts"`

```json
"scripts": {
  "start": "node index.js",
  "dev": "nodemon index.js",
  "build": "tsc"
}
```

run a script

```bash
npm run <script_name>
```

`start` and `test` are special — no `run` needed

```bash
npm start
npm test
```

---

## package.json

key fields

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {},
  "dependencies": {},
  "devDependencies": {}
}
```

---

## package-lock.json

auto-generated, locks exact versions of every installed package.
commit it to git — never edit it manually.

---

## misc

list installed packages

```bash
npm list
```

list globally installed packages

```bash
npm list -g --depth=0
```

search for a package

```bash
npm search <name>
```

view info about a package

```bash
npm info <package>
```

clear the cache

```bash
npm cache clean --force
```
