# Setting Up Jest for Testing In Angular 8
This short piece will show you step-by-step how to setup Jest with angular project.
I'll be using yarn you can replace with npm as appropriate.

#### Remove Karma and related files
- Remove karma and related dependencies
    ```
    yarn remove karma karma-chrome-launcher karma-coverage-istanbul-reporter karma-jasmine karma-jasmine-html-reporter
    ```
    
- In the file `angular.json` remove the "test" part shown below cos we won't be needing it
    ```
        ...
        "test": {
            ...
        }
        ...
    ```
-  remove the files `karma.conf.js` in *root folder* and `test.ts` in *src/ folder*

-  In the file `tsconfig.app.json` remove "src/test.ts" as that no longer exist

-  In the file `tsconfig.spec.json` 
       - replace the `"jasmine"` value of "types" array with `jest` 
       - remove the `"src/test.ts"` value of "files" array

#### Install Jest
- We'll add jest along with its preset for Angular applications as stated in the [ReadMe](https://github.com/thymikee/jest-preset-angular/blob/master/README.md)

    ```
    yarn add -D jest jest-preset-angular @types/jest
    # or
    npm install -D jest jest-preset-angular @types/jest
    ```
- Let us add jest configuration to `package.json`

    ```
    ...
    "jest": {
        "preset": "jest-preset-angular",
        "setupFilesAfterEnv": [
          "<rootDir>/setupJest.ts"
        ],
        "testPathIgnorePatterns": [
          "<rootDir>/node_modules/",
          "<rootDir>/dist/",
          "<rootDir>/src/test.ts"
        ],
        "globals": {
          "ts-jest": {
            "tsConfig": "<rootDir>/tsconfig.spec.json",
            "stringifyContentPathRegex": "\\.html$",
            "astTransformers": [
              "<rootDir>/node_modules/jest-preset-angular/InlineHtmlStripStylesTransformer"
            ]
          }
        }
    },
    ...
    ```
- Create file `setupJest.ts` in the root folder then add

    ```
    import 'jest-preset-angular';
    ```
