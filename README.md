# web-ext-plugin-cjs

A webpack plugin for running web-ext for CommonJS.

This is a fork of https://github.com/hiikezoe/web-ext-webpack-plugin, maintained for CRA-based projects which do not support ES Module syntax (yet). 

## Basic usage

```bash
$ npm install --save-dev web-ext-plugin-cjs

# Or for yarn
$ yarn add -D web-ext-plugin-cjs
```

**webpack.config.mjs**

```js
import WebExtPlugin from 'web-ext-plugin-cjs';

module.exports = {
  plugins: [new WebExtPlugin({ sourceDir: 'extension-dist' })],
};
```

Running `webpack` by itself will build the extension, effectively running
`web-ext build` on the output of your Webpack build.

To run the extension in a browser (including automatic reloading when using
Firefox), i.e. to run `web-ext run`, you will need to start Webpack in watch
mode using `webpack -w`.

## Options

- `artifactsDir` (optional) - The folder where artifacts are built stored.
  Defaults to `<sourceDir>/web-ext-artifacts`.
  You typically won't need to alter this.

- `browserConsole` (optional) - A boolean indicating if the browser console
  should be shown on load.

  Defaults to false.

- `buildPackage` (optional) - A boolean indicating if a zip file of the
  extension should be generated.

  The name of the .zip file is taken from the name field in the extension
  manifest unless `outputFilename` is set.

  Defaults to false.

- `chromiumBinary` (optional) - A path to a specific version of a Chromium
  browser to run. The value is an absolute path to the browser executable or an
  alias string.

- `chromiumProfile` (optional) - A path to a custom Chromium profile to use.

- `firefox` (optional) - A path to a specific version of Firefox to run.
  The value is an absolute path to the Firefox executable or an alias string.

- `firefoxPreview` (optional) - Turn on developer preview features in Firefox.
  This option accepts multiple values, although it currently only supports the
  `mv3` value, which is also the default value.
  The mv3 value allows developers to test their extensions with Firefox
  Manifest Version 3 support (without having to manually flipping the related
  preferences).

- `firefoxProfile` (optional) - A specific Firefox profile to use.
  This may be either a profile name or the path to a profile directory.
  If this is not set a new profile is generated each time.
- `keepProfileChanges` (optional) - A boolean value indicating if the profile
  specified by `firefoxProfile`.

  Defaults to false.

  See the notes for the [`--keep-profile-changes`
  flag](https://extensionworkshop.com/documentation/develop/web-ext-command-reference/#web-ext-run)
  from the `web-ext run` documentation.
  Specifically, this should not be used together with a profile you later use
  for browsing.
  It is, however, useful if you want to force the profile in a specific location
  to be written to (e.g. for testing out-of-disk space situations).

- `outputFilename` (optional) - The name of the .zip file to write when
  `buildPackage` is true.

  If this is not set the name of the .zip file is taken from the name field in
  the extension manifest.

- `overwriteDest` (optional) - A boolean value indicating if the package built
  when `buildPackage` is true, should overwrite an existing package at the same
  location.

  Without this option, web-ext will exit in error if the destination file
  already exists.

  Defaults to false.

- `profileCreateIfMissing` (optional) - A boolean value indicating if the
  profile specified by `firefoxProfile` should be created if it does not
  exist.

  Note that if this is specified, `firefoxProfile` is treated as meaning a
  directory path (not a profile name).

  Defaults to false.

- `runLint` (optional) - A boolean indicating if `web-ext lint` should
  be run as part of building the extension.

  Defaults to true.

- `selfHosted` (optional) - If `true` declares that your extension will be
  self-hosted and disables lint messages related to hosting on
  addons.mozilla.org.

  Defaults to `false`.

- `sourceDir` (optional) - The folder where webpack is building your extension
  to.
  Typically this will be where you have configured `output.path` to point to.
  Relative paths will be resolved relative to the `webpack.config.js` file.

  Defaults to the same folder as the `webpack.config.js` file.

- `startUrl` (optional) - A URL or array of URLs to load on startup.

- `target` (optional) - One of `firefox-desktop`, `firefox-android`, or
  `chromium` or an array of such values.

  Defaults to `firefox-desktop`.

  See the documentation for the `--target` option of [`web-ext run`](https://extensionworkshop.com/documentation/develop/web-ext-command-reference/#web-ext-run).
