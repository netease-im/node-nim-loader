# Node NIM Loader

Package for loading native files in Node and Electron applications. The project is inspired by the [node-addon-loader](https://github.com/ushu/node-addon-loader) and  [node-native-ext-loader](https://github.com/smt116/node-native-ext-loader). It works in the similar way but **allows to build path at runtime**.

## Installation

Add the package to the development dependencies:

```bash
# using npm:
$ npm install node-nim-loader --save-dev

# using yarn:
$ yarn add --dev node-nim-loader
```

## Usage

Update rules entry in the Webpack configuration file:

```js
module: {
  rules: [
    {
      test: /\.node$/,
      loader: "node-nim-loader"
    }
  ];
}
```

## Options

Options are configurable using `options` hash:

```js
module: {
  rules: [
    {
      test: /\.node$/,
      loader: "node-nim-loader",
      options: {
        rewritePath: path.resolve(__dirname, "dist")
      }
    }
  ];
}
```

### `basePath` (default: `[]`)

It allows adjusting path to the native module. The array will be concatenated with the resource name and then used in the runtime. For example, when the compile application lives inside `app.asar/renderer` subdirectory (Electron package), the path to the native module can be adjusted by using `basePath: ['app.asar', 'renderer']`.

Note that `basePath` is ignored when `rewritePath` option is used.

### `rewritePath` (default: `undefined`)

It allows to set an absolute paths to native files.

Note that it needs to remain `undefined` if you are building a package with embedded files. This way, the compiled application will work no matter of its location. This is important when building Electron applications that can be placed in any directory by the end user.

### `emit` (default: `true`)

Specifies whether the imported `.node` file will be copied to the output directory.

## Releasing a new version

1.  Bump version number in the `package.json` and `CHANGELOG.md` files.
1.  Run `npm install` to update `package-lock.json` file.
1.  Commit changes (include changes)
1.  Add a new tag (use `-a` and include changes)
1.  Push commits and tag
1.  Run `npm publish`
