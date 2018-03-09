#Proposal

Backwards compatibility is a major issue for TC-39 and has restricted the names the committee has been able to use for features. The most recent example of this is the Array.prototype.flatten/smoosh (I prefer 😘) fiasco. This proposal provides a mechanism to list a series of sources for the source of a module. If one of the sources fails to load then another may be used instead. The straw man syntax is as follows:

import ... from “Array.prototype.flatten” else “https://myPolyFill.net/Array/prototype/flatten.js”;

Where the “Array.prototype.flatten” is some embedder or TC-39 module that puts the prototype method on the Array prototype. If the user is on an old version of their JavaScriptEngine then they will fallback to the polypill as “Array.prototype.flatten” will not resolve to a valid module. This proposal provides a mechanism for any embedder to enable an otherwise incompatible feature via the module system on an opt-in basis.

#Alternatives

Provide a list of modules instead and the system may choose whichever version it wants i.e.:

import ... from [“Array.prototype.flatten”, “https://myPolyFill.net/Array/prototype/flatten.js”, "https://myCDN.net/Array/prototype/flatten.js"];

This allows the system to choose one to use myCDN’s version of the script if it already has it in the browser cache and doesn’t have the native version.

