<!-- https://medium.com/jstack-eu/using-mobx-decorators-in-create-react-app-v3-27f7b1afa1c7
 -->

Installing Mobx
First we want to install the mobx dependencies:
<!-- npm install mobx mobx-react -->
Mobx: state management library itself
Mobx-react: bindings to make sure it works perfectly in React
Enabling decorators
To enable decorators in CRA, we will need two dependencies:
customize-cra: makes sure we can tweak the CRA webpack config
react-app-rewired: needed by customize-cra, it will leverage this dependency under the hood
Install these dependencies:
<!-- npm install --dev customize-cra react-app-rewired -->
Next step is to make sure react-app-rewired is used, add following scripts to the package.json:
// instead of react-scripts start
<!-- "start": "react-app-rewired start", -->
// instead of react-scripts build
<!-- "build": "react-app-rewired build" -->
Now we need to add config-overrides.js in the base project to enable the decorator support within CRA.
<!-- const {addDecoratorsLegacy, useEslintRc, override} = require('customize-cra');

module.exports = override(
    addDecoratorsLegacy(),
    useEslintRc('./.eslintrc')
); -->
The final step is to make sure that our Eslint support decorators. Add following content to a new .eslintrc file (in the base project folder)
<!-- {
  "extends": "react-app",
  "parserOptions": {
    "ecmaFeatures": {
      "legacyDecorators": true
    }
  }
} -->
Testing if it works!
Check if decorators are working by adding an example store:
import {createContext} from 'react';
import {observable} from 'mobx';

class ExampleStore {
    @observable name = 'test';
}

export default new ExampleStore();