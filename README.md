# babel-preset-react-app-no-regenerator
Babel Preset like react-app from create-react-app without using Regenerator.  

###### react-app babel preset used in create-react-app forces you to use regenerator which compiles generator functions down to es5. This results in a poor debugging experience with source maps. Modern browsers support generator functions thus in development I want to use browser's implementation to debug.

We can combine with babel-preset-env to manage which version of modern browser I want to target in development.

1. we need to set `NODE_ENV` environment variable:

  * OSX: `export NODE_ENV=development`
  * Windows: `SET NODE_ENV=development`

2. `yarn add babel-preset-react-app-no-regenerator && yarn add babel-preset-env`

3. make the following adjustments to package.json file

````
"babel" : {
  "env": {
    "development" : {
      "presets": [
        "react-app-no-regenerator",
        [
          "env",
          {
            "targets": {
              "browsers": [
                "last 2 Chrome versions"
              ]
            },
            "exclude": ["transform-regenerator"],
            "modules": false,
            "loose": true,
            "debug": true
          }
        ]
      ]
    },
    "production" : {
        "presets": [
          "react-app",
          [
            "env",
            {
              "targets": {
                "browsers": ["ie >= 9"]
              },
              "modules": false,
              "loose": true
            }
          ]
        ]
      }
    }
  }
````
