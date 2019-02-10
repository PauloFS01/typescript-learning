# Typescript project

## tsconfig file

```json
{
    "compilerOptions": {
        "target": "es6",
        "outDir": "app/js"
    },
    "include": [
        "app/ts/**/*"
    ]
}
```
>This file is store de copile configs. In compilerOptions field we will indicate a copiler configs, when "target" is what js version will be copiled, and "outDir" is a directory that js files will e created. The "include" field indicate the origin directory os ts files. The optional confg ""noEmitOnError": true" indicates that the js file can't be created if a ts file has a error.

## Run typescript project

We can change the file "packeage.json" add line ""compile": "tsc"" in script field, so we can copile the project with command:

>npm run compile

We also use a runtime option with "tsc -w", so we can make the same and use a edit start command in packeage.json, and run with:

> npm start

The packeage.json will seems like: 

```jason
{
  "name": "alurabank",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "compile": "tsc",
    "start": "tsc -w"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "typescript": "^2.3.2"
  }
}
```