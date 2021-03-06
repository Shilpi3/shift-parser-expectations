# Shift Parser Expectations


## About

This module provides [Shift format ASTs](https://github.com/shapesecurity/shift-spec) and metadata for the passing (i.e. syntactically valid) tests in [test262-parser-tests](https://github.com/tc39/test262-parser-tests).


## Status

[Stable](http://nodejs.org/api/documentation.html#documentation_stability_index).


## Installation

```sh
npm install shift-parser-expectations
```


## Usage

```js
const file = '0a2fc93b6a63bbd3.js';
const src = fs.readFileSync('node_modules/test262-parser-tests/pass/' + file, 'utf8');
const expectation = fs.readFileSync('node_modules/shift-parser-expectations/expectations/' + file + '-tree.json');

const treeWithLocations = parse('src');
assert.deepEquals(treeWithLocations, JSON.parse(expectation));
```

Every file `f` in `test262-parser-tests/pass/` has two corresponding files in `expectations/` in this module: one named `f-tree.json` and one named `f-comments.json`.

The `tree` file holds a JSON encoding of Shift AST for the source text in `f`, with keys ordered according to [the order](https://github.com/shapesecurity/shift-spec/blob/es2017/attribute-order.conf) in the Shift specification, with the first key for a node being an additional 'type' property holding the string name of the node's type and the last key being an additional 'loc' property holding location information for the node.

The `comments` file holds a JSON encoding of an array of the comments in the source text in `f` in source order, including location information.


## Development

The expectations are generated by running `node generate-expectations`, which uses [shift-parser](https://github.com/shapesecurity/shift-parser-js). It is expected that you will use an in-development version of that project to update expectations files (using `npm link shift-parser`), so this project's `package.json` does not include `shift-parser` even as a dev dependency.

## Contributing

* Open a Github issue with a description of your desired change. If one exists already, leave a message stating that you are working on it with the date you expect it to be complete.
* Fork this repo, and clone the forked repo.
* Install dependencies with `npm install`.
* Build and test in your environment with `npm run build && npm test`.
* Create a feature branch. Make your changes. Add tests.
* Build and test in your environment with `npm run build && npm test`.
* Make a commit that includes the text "fixes #*XX*" where *XX* is the Github issue.
* Open a Pull Request on Github.


## License

    Copyright 2017 Shape Security, Inc.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
