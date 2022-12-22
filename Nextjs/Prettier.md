A code formatter to keep the same style across the entire application
- [Website](https://prettier.io/)
- [Documentation](https://prettier.io/docs/en/index.html)

## Installation
Seach for prettier in visual studio code and add the extenction, then add the follwing code into the `package.json`

```json
"prettier": {
        "bracketSpacing": true,
        "printWidth": 100,
        "tabWidth": 4,
        "useTabs": true,
        "singleQuote": true,
        "semi": false,
        "arrowParens": "avoid",
        "bracketSameLine": false
    },
```