### 0.9.1 (2014-09-17)


#### Features

* **grunt-espower:** update espower to 0.9.1 ([8c6761ae](https://github.com/twada/grunt-espower/commit/8c6761ae88f88070b132b0252185b64f03dd7299))


## 0.9.0 (2014-08-28)


#### Features


* **grunt-espower:** [support multistage sourcemap by @vvakame](https://github.com/twada/grunt-espower/pull/2)


## 0.8.0 (2014-08-12)


#### Features

* **grunt-espower:** update espower-source to 0.8.0 ([55110fa4](https://github.com/twada/grunt-espower/commit/55110fa4bffab62045d207d0460eaa864cc9fa8e))


#### Breaking Changes

If you already customize instrumentation pattern using `powerAssertVariableName` and `targetMethods`, you need to migarte. To migrate, change your code from the following:

```javascript
grunt.initConfig({
  espower: {
    demo: {
      options :{
        powerAssertVariableName: 'yourAssert',
        targetMethods: {
            oneArg: [
                'okay'
            ],
            twoArgs: [
                'equal',
                'customEqual'
            ]
        }
      },
      files: [
        {
          expand: true,        // Enable dynamic expansion.
          cwd: 'demo/',        // Src matches are relative to this path.
          src: ['**/*.js'],    // Actual pattern(s) to match.
          dest: 'espowered_demo/',  // Destination path prefix.
          ext: '.js'           // Dest filepaths will have this extension.
        }
      ]
    },
  },
})
```

To:

```javascript
grunt.initConfig({
  espower: {
    demo: {
      options :{
        patterns: [
            'yourAssert(value, [message])',
            'yourAssert.okay(value, [message])',
            'yourAssert.equal(actual, expected, [message])',
            'yourAssert.customEqual(actual, expected, [message])'
        ]
      },
      files: [
        {
          expand: true,        // Enable dynamic expansion.
          cwd: 'demo/',        // Src matches are relative to this path.
          src: ['**/*.js'],    // Actual pattern(s) to match.
          dest: 'espowered_demo/',  // Destination path prefix.
          ext: '.js'           // Dest filepaths will have this extension.
        }
      ]
    },
  },
})
```