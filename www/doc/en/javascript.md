module **javascript**
---------------------

The module **javascript** allows interaction with the objects defined in
Javascript programs and libraries present in the same page as the Brython
program.

**javascript**.`import_js(`_url[, alias]_`)`
> Imports the Javascript module at specified _url_ and adds _alias_ to the
> local namespace.
>
> If _alias_ is missing, the module name is computed from the url;
> for instance, for `import_js('js_test.js')` the alias is _js_test_.
>
> The module must define the name `$module`, an objet whose attributes make
> the namespace of the imported module.

> Example: if Javascript script at _js_test.js_ is

<blockquote>
```xml
var $module = {
    x: 1
}
```
</blockquote>

> then a Python script can use it this way:

<blockquote>
```python
import javascript

javascript.import_js("js_test.js", alias="js_module")
assert js_module.x == 1
```
</blockquote>

**javascript**.`import_modules(`_refs, callback_`)`
> imports the [Javascript modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
> whose urls are in the list `refs`. When they have all been imported,
> function `callback` is called with the module as arguments. `callback()`
> thus takes as many arguments as there are urls in `refs`.

> For instance if module **`exporter.js`** is

<blockquote>
```
const x = 1

export {x}
```
</blockquote>

> it can be used in a Python script with

<blockquote>
```python
import javascript

def main(module):
    assert module.x == 1

javascript.import_modules(
    ['/path/to/exporter.js'],
    main)
```
</blockquote>

> See [in the gallery](/gallery/three_webgl_interactive_cubes.html) a use case 
> with the modules of three.js.

**javascript**.`py2js(`_src_`)`
> Returns the Javascript code generated by Brython from the Python source code _src_.

**javascript**.`this()`
> Returns the Brython object matching the value of the Javascript object `this`. It
> may be useful when using Javascript frameworks, eg when a callback function uses
> the value of `this`.

The module also allows using objects defined by the Javascript language.
Please refer to the documentation of these objects.

**javascript**.`Date` [doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
> Constructor of date / time objects.

<blockquote>
```python
from javascript import Date

date = Date.new(2012, 6, 10)
print(date.toDateString())
```
</blockquote>

**javascript**.`JSON` [doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)
> Object to convert to and from JSON objects. It exposes two functions:

>> `stringify`: serialize simple objects (dictionaries, lists, tuples,
>> integers, reals, strings)

>> `parse`: conversion of a JSON-formatted string into a simple object

**javascript**.`Math` [doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)
> Object for mathematical functions and constants.

**javascript**.`NULL`
> the Javascript object `null`. Can be used to test if a Javascript
> object is `null`.

**javascript**.`Number` [doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
> Constructor for objects of type "number".

**javascript**.`RegExp` [doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
> Constructor of "regular expression" objects, using the Javascript-specific
> syntax, which doesn't fully match that of Python.
> The method `exec()` of instances of this class can be applied to Python
> strings:
<blockquote>
```python
from javascript import RegExp

re = RegExp.new(r"^test(\d+)$")
print(re.exec("test44"))
```
</blockquote>

**javascript**.`String` [doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
> Constructor of Javascript objects of type "string". Must be used to call
> methods that accept Javascript regular expressions as parameters:
<blockquote>
```python
from javascript import RegExp, String

re = RegExp.new(r"^test(\d+)$")
print(String.new("test33").search(re))
```
</blockquote>

**javascript**.`UNDEFINED`
> the Javascript object `undefined`. Can be used to test if a Javascript
> object is `undefined`.