#programing #backend #javascript
[[JavaScript]]
## setup

download node.js (via nvm — recommended)

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | sh
```

install the latest lts version

```bash
nvm install --lts
```

check node version

```bash
node --version
```

check npm version

```bash
npm --version
```

update node via nvm

```bash
nvm install --lts
nvm use --lts
```

---

## running code

run a file

```bash
node <file_name>.js
```

open the interactive repl

```bash
node
```

exit the repl

```bash
.exit
```

---

## modules

node uses commonjs by default

import a built-in module

```javascript
const fs = require('fs');
const path = require('path');
const http = require('http');
```

import your own file

```javascript
const myModule = require('./myFile');
```

export from a file

```javascript
module.exports = myFunction;
// or export multiple things
module.exports = { myFunction, myVariable };
```

use esm (modern syntax) by adding `"type": "module"` to `package.json`, then

```javascript
import fs from 'fs';
import { myFunction } from './myFile.js';

export const myFunction = () => {};
export default myFunction;
```

---

## useful built-ins

read a file

```javascript
const fs = require('fs');
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

read a file (sync)

```javascript
const data = fs.readFileSync('file.txt', 'utf8');
```

write a file

```javascript
fs.writeFile('file.txt', 'hello', (err) => {
  if (err) throw err;
});
```

join paths safely

```javascript
const path = require('path');
const full = path.join(__dirname, 'folder', 'file.txt');
```

get current file and directory

```javascript
console.log(__filename); // full path to this file
console.log(__dirname);  // directory of this file
```

---

## http server

create a basic server

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('hello world');
});

server.listen(3000, () => {
  console.log('server running on http://localhost:3000');
});
```

---

## environment variables

access env variables

```javascript
console.log(process.env.PORT);
```

set them inline when running

```bash
PORT=4000 node server.js
```

or use a `.env` file with the `dotenv` package

```javascript
require('dotenv').config();
console.log(process.env.PORT);
```

---

## process

exit the process

```javascript
process.exit(0); // 0 = success, 1 = error
```

read command line arguments

```javascript
const args = process.argv.slice(2);
console.log(args);
```
