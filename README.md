# python.node

Call python code from node.js.


## Usage

```javascript
var python = require('python.node');
var os = python.import('os');

var path = require('path');

assert(os.path.basename(os.getcwd()) == path.basename(process.cwd()));
```


## Feature

```python
def test():
	try:
		## do samething
	except Exception as e:
		raise e
	return 'done'
```

```javascript
PYMODULE.test.async = true;
PYMODULE.test(function (result, error) {
	if (!error)
		console.log(result);
});
```
If you need to pass keyword args, make the last argument an object with a sub-object `kwArgs` containing them:
```javascript
PYMODULE.test("positionalArg", "anotherPositionalArg", { kwArgs: { arg1: "foo", arg2: 42} } );
```
## Build

### Mac

```bash
# for Node.js
node-gyp rebuild --arch=[ia32/x64] --target=x.y.z 
# target nodejs version, eg: 0.10.28
```

```bash
# for node-webkit
nw-gyp rebuild --arch=[ia32/x64] --target=x.y.z 
# target node-webkit version, eg: 0.8.6
```

### Windows

```bash
# for Node.js
cd python.node\src
cl /O2 /MT /LD -Febinding.node binding.cc py_object_wrapper.cc utils.cc <NODE_GYP_ROOT>\.node-gyp\<NODEJS_VERSION>\<NODEJS_ARCH>\node.lib <PYTHON_ROOT>\Python27\libs\python27.lib /I<NODE_GYP_ROOT>\.node-gyp\<NODEJS_VERSION>\src /I<NODE_GYP_ROOT>\.node-gyp\<NODEJS_VERSION>\deps\uv\include /I<NODE_GYP_ROOT>\.node-gyp\<NODEJS_VERSION>\deps\v8\include /I<PYTHON_ROOT>\Python27\include
copy binding.node <NODE_MODULES_ROOT>\python.js\compiled\<NODEJS_VERSION>\win32\<NODEJS_ARCH>
```

```bash
# for node-webkit
cd python.node\src
cl /O2 /MT /LD -Febinding.node binding.cc py_object_wrapper.cc utils.cc <NW_GYP_ROOT>\.nw-gyp\<NODE_WEBKIT_VERSION>\<NODE_WEBKIT_ARCH>\nw.lib <PYTHON_ROOT>\Python27\libs\python27.lib /I<NW_GYP_ROOT>\.nw-gyp\<NODE_WEBKIT_VERSION>\src /I<NW_GYP_ROOT>\.nw-gyp\<NODE_WEBKIT_VERSION>\deps\uv\include /I<NW_GYP_ROOT>\.nw-gyp\<NODE_WEBKIT_VERSION>\deps\v8\include /I<PYTHON_ROOT>\Python27\include
copy binding.node <NODE_MODULES_ROOT>\python.js\compiled\<NODEJS_VERSION>\win32\<NODE_WEBKIT_ARCH>
```


## Install

```bash
npm install python.node
```

or

```bash
npm install <protocol>://<user>@<domain>/<projects>/python.node.git
# eg: npm install git+ssh://git@example.com/projects/python.node.git
```

## Electron Install

```bash
npm install python.node
cd node_modules\python.node
npm run rebuild
```

## Test

```bash
node test/jstest.js
```


## Thanks

* [Jean-S??bastien Tremblay](https://github.com/JeanSebTr/node-python)
* [Chris Dickinson](https://github.com/chrisdickinson/node-python)
