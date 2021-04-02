## Nodejs Module Require
### the use of require.main, require.resolve, require.resolve.paths

1. require.main
  ```
  Accessing the main module#
  When a file is run directly from Node.js, require.main is set to its module. That means that it is possible to determine whether a file has been run directly by testing require.main === module.
  For a file foo.js, this will be true if run via node foo.js, but false if run by require('./foo').
  ```

2. require.resolve(request[, options])
  ```
  request <string> The module path to resolve.
  options <Object>
      paths <string[]> Paths to resolve module location from. If present, these paths are used instead of the default resolution paths, with the exception of GLOBAL_FOLDERS like $HOME/.node_modules, which are always included. Each of these paths is used as a starting point for the module resolution algorithm, meaning that the node_modules hierarchy is checked from this location.
  Returns: <string>
  Use the internal require() machinery to look up the location of a module, but rather than loading the module, just return the resolved filename.

  If the module can not be found, a MODULE_NOT_FOUND error is thrown.
  ```
  ```
  require.resolve.paths(request)#
    request <string> The module path whose lookup paths are being retrieved.
    Returns: <string[]> | <null>
    Returns an array containing the paths searched during resolution of request or null if the request string references a core module, for example http or fs.
  ```

### References
- https://nodejs.org/dist/latest-v14.x/docs/api/modules.html#modules_require_main
- https://nodejs.org/dist/latest-v14.x/docs/api/modules.html#modules_require_resolve_request_options
