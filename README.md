# Proposal

Backwards compatibility is a major issue for TC-39 and has restricted the names the committee has been able to use for features. The most recent example of this is the Array.prototype.flatten/smoosh (I prefer 😘) [fiasco](https://github.com/tc39/proposal-flatMap/pull/56). This proposal provides a mechanism to list a series of sources for the source of a module. If one of the sources fails to load then another may be used instead. The straw man syntax is as follows:

```js
import “std:Array.prototype.flatten” else “https://myPolyFill.net/Array/prototype/flatten.js”;
```

Where the “Array.prototype.flatten” is some embedder or TC-39 module that puts the prototype method on the Array prototype. If the user is on an old version of their JavaScriptEngine then they will fallback to the polypill as “Array.prototype.flatten” will not resolve to a valid module. This proposal provides a mechanism for any embedder to enable an otherwise incompatible feature via the module system on an opt-in basis.

# Alternatives

Provide a list of modules instead and the system may choose whichever version it wants i.e.:

```js
import [“std:Array.prototype.flatten”, “https://myPolyFill.net/Array/prototype/flatten.js”, "https://myCDN.net/Array/prototype/flatten.js"];
```

This allows the system to choose one to use myCDN’s version of the script if it already has it in the browser cache and doesn’t have the native version. Additionally, this could still be used even non-native modules since the browser

# Extensions

There is also the question of Sub-Resource Intergrity (SRI) with respect to ES6 modules. There is currently no way to use modules and SRI (Note: I need to triple check that this is true). There could also be syntax for specifing the attributes of the expected module. For example:

```js
import ["std:Array.prototype.flatten", “https://myPolyFill.net/Array/prototype/flatten.js”, "https://myCDN.net/Array/prototype/flatten.js"] with { integrity="some #" };
```

The exact location of the `with { integrity="some #" }` could either be on each import or for everything.

# Limitations

This proposal does not solve the problem for loading builtin modules for non-modules. For that problem one solution could be  to allow some builtin modules to be run as either module or non-module code. Then, at least for the case of html, there could be a new script tag attribute, say "native", referencing the builtin module. Obviously, this would require some coordination with W3C.

# Related Proposals

The Layered Features proposal:
https://github.com/drufball/layered-apis/
