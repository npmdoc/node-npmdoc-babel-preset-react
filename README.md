# api documentation for  [babel-preset-react (v6.23.0)](https://babeljs.io/)  [![npm package](https://img.shields.io/npm/v/npmdoc-babel-preset-react.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-babel-preset-react) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-babel-preset-react.svg)](https://travis-ci.org/npmdoc/node-npmdoc-babel-preset-react)
#### Babel preset for all React plugins.

[![NPM](https://nodei.co/npm/babel-preset-react.png?downloads=true)](https://www.npmjs.com/package/babel-preset-react)

[![apidoc](https://npmdoc.github.io/node-npmdoc-babel-preset-react/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-babel-preset-react_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-babel-preset-react/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-babel-preset-react/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-babel-preset-react/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Sebastian McKenzie",
        "email": "sebmck@gmail.com"
    },
    "dependencies": {
        "babel-plugin-syntax-jsx": "^6.3.13",
        "babel-plugin-transform-react-display-name": "^6.23.0",
        "babel-plugin-transform-react-jsx": "^6.23.0",
        "babel-plugin-transform-react-jsx-self": "^6.22.0",
        "babel-plugin-transform-react-jsx-source": "^6.22.0",
        "babel-preset-flow": "^6.23.0"
    },
    "description": "Babel preset for all React plugins.",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "eb7cee4de98a3f94502c28565332da9819455195",
        "tarball": "https://registry.npmjs.org/babel-preset-react/-/babel-preset-react-6.23.0.tgz"
    },
    "homepage": "https://babeljs.io/",
    "license": "MIT",
    "main": "lib/index.js",
    "maintainers": [
        {
            "name": "amasad",
            "email": "amjad.masad@gmail.com"
        },
        {
            "name": "hzoo",
            "email": "hi@henryzoo.com"
        },
        {
            "name": "jmm",
            "email": "npm-public@jessemccarthy.net"
        },
        {
            "name": "loganfsmyth",
            "email": "loganfsmyth@gmail.com"
        },
        {
            "name": "sebmck",
            "email": "sebmck@gmail.com"
        },
        {
            "name": "thejameskyle",
            "email": "me@thejameskyle.com"
        }
    ],
    "name": "babel-preset-react",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "https://github.com/babel/babel/tree/master/packages/babel-preset-react"
    },
    "scripts": {},
    "version": "6.23.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module babel-preset-react](#apidoc.module.babel-preset-react)
1.  object <span class="apidocSignatureSpan">babel-preset-react.</span>env
1.  object <span class="apidocSignatureSpan">babel-preset-react.</span>plugins
1.  object <span class="apidocSignatureSpan">babel-preset-react.</span>presets

#### [module babel-preset-react.plugins](#apidoc.module.babel-preset-react.plugins)
1.  [function <span class="apidocSignatureSpan">babel-preset-react.plugins.</span>0 (_ref)](#apidoc.element.babel-preset-react.plugins.0)
1.  [function <span class="apidocSignatureSpan">babel-preset-react.plugins.</span>1 ()](#apidoc.element.babel-preset-react.plugins.1)
1.  [function <span class="apidocSignatureSpan">babel-preset-react.plugins.</span>2 (_ref)](#apidoc.element.babel-preset-react.plugins.2)



# <a name="apidoc.module.babel-preset-react"></a>[module babel-preset-react](#apidoc.module.babel-preset-react)



# <a name="apidoc.module.babel-preset-react.plugins"></a>[module babel-preset-react.plugins](#apidoc.module.babel-preset-react.plugins)

#### <a name="apidoc.element.babel-preset-react.plugins.0"></a>[function <span class="apidocSignatureSpan">babel-preset-react.plugins.</span>0 (_ref)](#apidoc.element.babel-preset-react.plugins.0)
- description and source-code
```javascript
0 = function (_ref) {
  var t = _ref.types;

  var JSX_ANNOTATION_REGEX = /\*?\s*@jsx\s+([^\s]+)/;

  var visitor = (0, _babelHelperBuilderReactJsx2.default)({
    pre: function pre(state) {
      var tagName = state.tagName;
      var args = state.args;
      if (t.react.isCompatTag(tagName)) {
        args.push(t.stringLiteral(tagName));
      } else {
        args.push(state.tagExpr);
      }
    },
    post: function post(state, pass) {
      state.callee = pass.get("jsxIdentifier")();
    }
  });

  visitor.Program = function (path, state) {
    var file = state.file;

    var id = state.opts.pragma || "React.createElement";

    for (var _iterator = file.ast.comments, _isArray = Array.isArray(_iterator), _i = 0, _iterator = _isArray ? _iterator : (0,
_getIterator3.default)(_iterator);;) {
      var _ref2;

      if (_isArray) {
        if (_i >= _iterator.length) break;
        _ref2 = _iterator[_i++];
      } else {
        _i = _iterator.next();
        if (_i.done) break;
        _ref2 = _i.value;
      }

      var comment = _ref2;

      var matches = JSX_ANNOTATION_REGEX.exec(comment.value);
      if (matches) {
        id = matches[1];
        if (id === "React.DOM") {
          throw file.buildCodeFrameError(comment, "The @jsx React.DOM pragma has been deprecated as of React 0.12");
        } else {
          break;
        }
      }
    }

    state.set("jsxIdentifier", function () {
      return id.split(".").map(function (name) {
        return t.identifier(name);
      }).reduce(function (object, property) {
        return t.memberExpression(object, property);
      });
    });
  };

  return {
    inherits: _babelPluginSyntaxJsx2.default,
    visitor: visitor
  };
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.babel-preset-react.plugins.1"></a>[function <span class="apidocSignatureSpan">babel-preset-react.plugins.</span>1 ()](#apidoc.element.babel-preset-react.plugins.1)
- description and source-code
```javascript
1 = function () {
  return {
    manipulateOptions: function manipulateOptions(opts, parserOpts) {
      parserOpts.plugins.push("jsx");
    }
  };
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.babel-preset-react.plugins.2"></a>[function <span class="apidocSignatureSpan">babel-preset-react.plugins.</span>2 (_ref)](#apidoc.element.babel-preset-react.plugins.2)
- description and source-code
```javascript
2 = function (_ref) {
  var t = _ref.types;

  function addDisplayName(id, call) {
    var props = call.arguments[0].properties;
    var safe = true;

    for (var i = 0; i < props.length; i++) {
      var prop = props[i];
      var key = t.toComputedKey(prop);
      if (t.isLiteral(key, { value: "displayName" })) {
        safe = false;
        break;
      }
    }

    if (safe) {
      props.unshift(t.objectProperty(t.identifier("displayName"), t.stringLiteral(id)));
    }
  }

  var isCreateClassCallExpression = t.buildMatchMemberExpression("React.createClass");

  function isCreateClass(node) {
    if (!node || !t.isCallExpression(node)) return false;

    if (!isCreateClassCallExpression(node.callee)) return false;

    var args = node.arguments;
    if (args.length !== 1) return false;

    var first = args[0];
    if (!t.isObjectExpression(first)) return false;

    return true;
  }

  return {
    visitor: {
      ExportDefaultDeclaration: function ExportDefaultDeclaration(_ref2, state) {
        var node = _ref2.node;

        if (isCreateClass(node.declaration)) {
          var displayName = state.file.opts.basename;

          if (displayName === "index") {
            displayName = _path2.default.basename(_path2.default.dirname(state.file.opts.filename));
          }

          addDisplayName(displayName, node.declaration);
        }
      },
      CallExpression: function CallExpression(path) {
        var node = path.node;

        if (!isCreateClass(node)) return;

        var id = void 0;

        path.find(function (path) {
          if (path.isAssignmentExpression()) {
            id = path.node.left;
          } else if (path.isObjectProperty()) {
            id = path.node.key;
          } else if (path.isVariableDeclarator()) {
            id = path.node.id;
          } else if (path.isStatement()) {
            return true;
          }

          if (id) return true;
        });

        if (!id) return;

        if (t.isMemberExpression(id)) {
          id = id.property;
        }

        if (t.isIdentifier(id)) {
          addDisplayName(id.name, node);
        }
      }
    }
  };
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
