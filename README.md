# ZaHub community of practice

## Moving from Karma to Jest & Angular testing library

### Step 1: Uninstall Karma & Jasmine
```
npm uninstall karma karma-chrome-launcher karma-coverage-istanbul-reporter karma-jasmine karma-jasmine-html-reporter jasmine-core jasmine-spec-reporter karma-coverage
```

### Step 2: Remove Karma & Jasmine configuration files
delete the following files
```
karma.config.js
src/test.ts
```
### step 3: Remove configuration references in
 `tsconfig.spec.json`
 ```
{
    ...,
  "files": [
    "src/test.ts", <- delete
    ...
    ]
}
```
`angular.json`
```
  ...,
  "test": {} <- delete contents, but leave the key
  ....
```

`tsconfig.spec.json`
```  ...,
  "compilerOptions": {
    ...,
    "types": [
      "jasmine", <- delete
      ...
    ]
  }
```
## Installing and configuring Jest & Angular testing library
### step 1: Install jest & angular testing library
```
npm i -D @types/jest jest jest-preset-angular ts-jest @angular-builders/jest @testing-library/angular

```

### step 2: Create jest configuration files
`jest.configure.js`
```
module.exports = {
    preset: 'jest-preset-angular',
    setupFilesAfterEnv: [
        '<rootDir>/jest.setup.ts'
    ]
};
```

`jest.setup.ts`
```
import 'jest-preset-angular';
```
### step 3: update existing configutation files
`tsconfig.spec.json`
```
{
  ...,
  "compilerOptions": {
    ...,
    "types": [
      "jest", <- new
      ...
    ]
  }
}
```

`tsconfig.json`
```
tsconfig.json
{
  ...,
  "compilerOptions": {
    ...,
    "esModuleInterop": true, <- new
    "emitDecoratorMetadata": true, <- new
    ...
  },
  ...
}
```
`package.json`
```
{
  ...,
  "scripts": {
    ...,
    "test": "jest --detectOpenHandles --config ./jest.config.js", <- new
    "test:watch": "jest -o --watch --config ./jest.config.js", <- new
    ...
  },
  ...
}
```
`angular.json`
```
{
  ...,
  "test": {
    "builder": "@angular-builders/jest:run" <- new
  }
  ....
}
```
