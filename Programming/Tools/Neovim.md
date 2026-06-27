#programing #devtools

## setup

install neovim

```bash
sudo pacman -S neovim
````

check version

```bash
nvim --version
```

open a file

```bash
nvim <file_name>
```

open neovim with no file

```bash
nvim
```

---

## modes

|mode|how to enter|
|---|---|
|normal|`Esc`|
|insert|`i`|
|visual|`v`|
|command|`:`|

---

## navigation

|key|action|
|---|---|
|`h j k l`|left / down / up / right|
|`w`|jump forward one word|
|`b`|jump back one word|
|`0`|start of line|
|`$`|end of line|
|`gg`|top of file|
|`G`|bottom of file|
|`Ctrl+d`|scroll down half page|
|`Ctrl+u`|scroll up half page|

---

## editing

| key      | action                        |
| -------- | ----------------------------- |
| `i`      | insert before cursor          |
| `a`      | insert after cursor           |
| `o`      | new line below and insert     |
| `O`      | new line above and insert     |
| `x`      | delete character under cursor |
| `dd`     | delete line                   |
| `yy`     | copy line                     |
| `p`      | paste after cursor            |
| `u`      | undo                          |
| `Ctrl+r` | redo                          |
| `ciw`    | change inner word             |
| `di"`    | delete inside quotes          |

---

## search & replace

search

```
/<text>
```

navigate results

```
n   → next
N   → previous
```

replace in file

```
:%s/<old>/<new>/g
```

replace with confirmation

```
:%s/<old>/<new>/gc
```

---

## files & buffers

save

```
:w
```

quit

```
:q
```

save and quit

```
:wq
```

force quit without saving

```
:q!
```

open a file

```
:e <file_name>
```

---

## splits

split horizontally

```
:sp <file_name>
```

split vertically

```
:vsp <file_name>
```

navigate splits

```
Ctrl+w + h j k l
```

---

## config

config file location

```
~/.config/nvim/init.lua
```

or for vimscript

```
~/.config/nvim/init.vim
```