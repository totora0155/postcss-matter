# postcss-matter

[![npm version](https://badge.fury.io/js/postcss-matter.svg)](https://badge.fury.io/js/postcss-matter)
[![Build Status](https://travis-ci.org/totora0155/postcss-matter.svg?branch=master)](https://travis-ci.org/totora0155/postcss-matter)
[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/sindresorhus/xo)

<p><img width="20" src="https://camo.githubusercontent.com/2ec260a9d4d3dcc109be800af0b29a8471ad5967/687474703a2f2f706f73746373732e6769746875622e696f2f706f73746373732f6c6f676f2e737667"> <a href="https://github.com/postcss/postcss">PostCSS</a> plugin that to add matter property</p>

---

## Install

```
npm i postcss-matter
```

## Usage

Define matters using the `@matter` atrule.  
Then use they.

```css
@matter {
  default-a {
    color: inherit;
    text-decoration: none;
    cursor: pointer;
  }
}

@matter namespace {
  default-input {
    box-sizing: border-box;
    border: 1px solid #333;
  }
}

a.that {
  matter: default-a;
}

a.this {
  matter: default-a;
}

.input {
  matter: namespace-default-input;
}

.btn {
  matter: default-button;
}

.btn--small {
  matter: default-button;
  font-size: .85em;
}

@matter {
  default-button {
    padding: .5em 1em;
    background: #e42829;
  }
}

```

## Transform

```javascript
const fs = require('fs');
const postcss = require('postcss');
const matter = require('postcss-matter'):
const beautify = require('cssbeautify');

const css = fs.readFileSync('./sample.css', 'utf-8');

postcss([matter])
  .process(css)
  .then(result => console.log(beautify(result.css, {indent: '  '})));

```

## Output

like this.

```css
a.that,
a.this {
  color: inherit;
  text-decoration: none;
  cursor: pointer;
}

.input {
  box-sizing: border-box;
  border: 1px solid #333;
}

.btn {
  padding: .5em 1em;
  background: #e42829;
}

.btn--small {
  padding: .5em 1em;
  background: #e42829;
  font-size: .85em;
}

```

## Syntax

### AtRule

```css
@matter <namespace-name> {
  <matter-name> {
    declaration;
    ...
  }
}
```

### Declaration

```css
<selector> {
  matter: <defined matter-name>;
}
```

## Options

- `isolateLength`   
  For example,
  ```css
  @matter {
    that {
      color: #000;
      font-size: 15px;
      line-height: 1.7;
    }
  }
  .a {
    matter: that;
  }
  .b {
    matter: that;
  }
  ```
  That's now `isolateLength: 3`, you will get this.
  ```css
  .a,
  .b {
    color: #000;
    font-size: 15px;
    line-height: 1.7
  }
  ```
  When that's `isolateLength: 4`, get it.
  ```css
  .a {
    color: #000;
    font-size: 15px;
    line-height: 1.7;
  }

  .b {
    color: #000;
    font-size: 15px;
    line-height: 1.7;
  }
  ```
  `3` by default.

## Run to example

**1** Close this

```
git clone git@github.com:totora0155/postcss-matter.git
```

**2** Change directory
```
cd postcss-matter
```

**3** Install modules
```
npm install
```

**4** Run to script
```
cd examples && node postcss.js
```

## Change log

|version|log|
|:-:|:--|
|0.0.1|Release!|