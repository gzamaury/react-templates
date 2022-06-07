# Create React App preset for Storybook

One-line [Create React App](https://github.com/facebook/create-react-app) configuration for Storybook.

This preset is designed to use alongside [`@storybook/react`](https://github.com/storybookjs/storybook/tree/master/app/react).

## Compatibility

This version (4.x) of `@storybook/preset-create-react-app` is compatibly with Create React App version 5 and above. Earlier versions are compatible with earlier version of the preset.

## Basic usage

**Note: you don't need to do this manually** if you used `npx -p @storybook/cli sb init` on a create-react-app, everything should properly setup already ✅.

First, install this preset to your project.

```sh
# Yarn
yarn add -D @storybook/preset-create-react-app

# npm
npm install -D @storybook/preset-create-react-app
```

Once installed, add this preset to the appropriate file:

- `./.storybook/main.js` (for Storybook 5.3.0 and newer)

  ```js
  module.exports = {
    addons: ["@storybook/preset-create-react-app"],
  };
  ```

- `./.storybook/presets.js` (for all Storybook versions)

  ```js
  module.exports = ["@storybook/preset-create-react-app"];
  ```

## Advanced usage

### Usage with Docs

When working with Storybook Docs, simply add the following config to your `main.js` file.

```js
module.exports = {
  addons: [
    "@storybook/preset-create-react-app",
    {
      name: "@storybook/addon-docs",
      options: {
        configureJSX: true,
      },
    },
  ],
};
```

### CRA overrides

This preset uses CRA's Webpack/Babel configurations, so that Storybook's behavior matches your app's behavior.

However, there may be some cases where you'd rather override CRA's default behavior. If that is something you need, you can use the `craOverrides` object.

| Option               | Default          | Behaviour | Type       | Description                                                                                                        |
| -------------------- | ---------------- | --------- | ---------- | ------------------------------------------------------------------------------------------------------------------ |
| `fileLoaderExcludes` | `['ejs', 'mdx']` | Extends   | `string[]` | Excludes file types (by extension) from CRA's `file-loader` configuration. The defaults are required by Storybook. |

Here's how you might configure this preset to ignore PDF files so they can be processed by another preset or loader:

```js
module.exports = {
  addons: [
    {
      name: "@storybook/preset-create-react-app",
      options: {
        craOverrides: {
          fileLoaderExcludes: ["pdf"],
        },
      },
    },
  ],
};
```

### Custom `react-scripts` packages

In most cases, this preset will find your `react-scripts` package, even if it's a fork of the offical `react-scripts`.

In the event that it doesn't, you can set the package's name with `scriptsPackageName`.

```js
module.exports = {
  addons: [
    {
      name: "@storybook/preset-create-react-app",
      options: {
        scriptsPackageName: "@my/react-scripts",
      },
    },
  ],
};
```

### Warning for forks of 'react-scripts'

One of the tasks that this preset does is inject the storybook config directory (the default is `.storybook`)
into the `includes` key of the webpack babel-loader config that react-scripts (or your fork) provides. This is
nice because then any components/code you've defined in your storybook config directory will be run through the
babel-loader as well.

The potential gotcha exists if you have tweaked the Conditions of the webpack babel-loader rule in your fork of
react-scripts. This preset will make the `include` condition an array (if not already), and inject the storybook
config directory. If you have changed the conditions to utilize an `exclude`, then BOTH conditions will need to
be true (which isn't likely going to work as expected).

The steps to remedy this would be to follow the steps for customizing the webpack config within the storybook
side of things. [Details for storybook custom webpack config](https://storybook.js.org/docs/configurations/custom-webpack-config/)
You'll have access to all of the rules in `config.module.rules`. You'll need to find the offending rule,
and customize it how you need it to be to be compatible with your fork.

See [Webpack Rule Conditions](https://webpack.js.org/configuration/module/#rule-conditions) for more details
concerning the conditions.

## Resources

- [Walkthrough to set up Storybook Docs with CRA & typescript](https://gist.github.com/shilman/bc9cbedb2a7efb5ec6710337cbd20c0c)
- [Example projects (used for testing this preset)](https://github.com/storybookjs/presets/tree/master/examples)

#

#

# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)
