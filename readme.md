# React-Express-Typescript ###

Typescript playground

## Setup
1. Add typescript and its development libraries
```
yarn add typescript ts-node nodemon -D
```
2. Make a source dirctory and entry point
```
mkdir src
touch index.ts
```
3. Typescript configuration with `tsconfig.json` (you can create tsconfig.js manual or by cli `tsc --init`)
```
{
  "compilerOptions": {
    "target": "es2017", 
    "module": "commonjs",
    "outDir": "./dist",
    "strict": true,
    "noImplicitThis": false,
    "baseUrl": "./",
    "paths": {
      "*": ["node_modules/*"]
    },
    "allowSyntheticDefaultImports": true,
    "esModuleInterop": true,
    "experimentalDecorators": true,
      },
  "include": [
    "src/**/*"
  ],
  "exclude": [
    "node_modules", "**/*.test.ts", "**/*.spec.ts"
  ]
}
```

4. Configuration of nodemon in `package.json`
```
...
"nodemonConfig": {
    "ignore": [
      "**/*.test.ts",
      "**/*.spec.ts",
      ".git",
      "node_modules"
    ],
    "watch": [
      "src"
    ],
    "exec": "ts-node src/index.ts",
    "ext": "ts"
  },
...
```

At this moment, you should be fine to run `nodemon`, it would auto run as '`ts-node src/index`'. For the objective as playground, I decide to as script as `play`, so that I can just run '`yarn play`' to enable try some typescript codes
```
...
"scripts": {
    "play": "nodemon",
...
```

5. [Optional] Add eslint to standardlize your codeing style, trust me, it will give you lots more than you thougth
```
yarn add eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser -D
```

5. [Optional] Configuration of eslint (you can create .eslintrc.js manual or by cli `eslint --init`)
```
module.exports = {
  parser: "@typescript-eslint/parser", 
  extends: [
    'plugin:@typescript-eslint/recommended',
  ],
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: 'module'
  }
};
```
6. [Optional] Add prettier for eslint rules
```
yarn add prettier eslint-config-prettier eslint-plugin-prettier -D
```

7. [Optional] Configuration of prettier rules
```
module.exports = {
  semi: true,
  trailingComma: 'all',
  singleQuote: true,
  printWidth: 120,
  tabWidth: 2,
};
```
At this moment, you should be able to test your playground with eslint by 
```
node node_modules/eslint/bin/eslint.js src/**
```
But I want to run it as a script, I add following script to `package.json`
```
...
"eslint": "node node_modules/eslint/bin/eslint.js src/**",
...
```
Now, '`yarn eslint`' would do eslint for me/ (CI)
