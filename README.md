# Blockly for Node.js and Browser via CommonJS module

JCOA: Modified to link my blockly version
https://stackoverflow.com/questions/913701/changing-remote-repository-for-a-git-submodule

![Build](https://travis-ci.org/mo4islona/node-blockly.svg?branch=master)


Supports `JavaScript`, `PHP`, `Dart`, `Lua` and `Python` generators.

## Update to new blockly source:
- Add new repository in github, example node-blockpy-blockly
- Import and set the URL of this repository
- Change the URL on .gitmodules to point to another blockly repository
- Clone the new repository and cd to it (git clone ...)
- npm install
- git submodule sync
- git submodule update --init --recursive --remote
- gulp build
Now update the repository with the new generated files
- git add -A
- git commit -m "Changed blockly to a new source"
- git push origin master

## Install
```
npm install node-blockly
```
## Usage
**Node.js**

All generators
```js
var Blockly = require('node-blockly');
```
Or you may use standalone generators to decrease memory usage
```js 
var Blockly = require('node-blockly/lua');
```

**Browser**

All generators
```js
var Blockly = require('node-blockly/browser');
```

## Example

```js
var Blockly = require('node-blockly');

var xmlText = `<xml xmlns="http://www.w3.org/1999/xhtml">
        <block type="variables_set">
            <field name="VAR">blockly</field>
            <value name="VALUE">
                <block type="text">
                    <field name="TEXT">Hello Node.js!</field>
                </block>
            </value>
        </block>
    </xml>`;

try {
    var xml = Blockly.Xml.textToDom(xmlText);
}
catch (e) {
    console.log(e);
    return
}

var workspace = new Blockly.Workspace();
Blockly.Xml.domToWorkspace(xml, workspace);
var code = Blockly.JavaScript.workspaceToCode(workspace);

console.log(code)  
```
Compiled result

```js
var blockly; 

blockly = 'Hello Node.js!';
```
