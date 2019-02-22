# Typescript project

## tsconfig file

```json
{
    "compilerOptions": {
        "target": "es6",
        "outDir": "app/js",
        "noEmitOnError": true,
        "noImplicitAny": true,
        "removeComments": true
    },
    "include": [
        "app/ts/**/*"
    ]
}
```

This file is store de copile configs. In compilerOptions field we will indicate a copiler configs, when "target" is what js version will be copiled, and "outDir" is a directory that js files will e created. The "include" field indicate the origin directory os ts files.

## Optional configs

### noEmitOnError

The optional confg - **"noEmitOnError": true** - indicates that the js file can't be created if a ts file has a error.

### noImplictAny

This optional setting disables inplicit type Any. When we use then, we need to specify a type for all variables. Leave this option disabled if you are migrante from another linguage.

### removeComments

With this optional setting we can avoid that comments go to the production and impact the final size code.

## Run typescript project

We can change the file "packeage.json" add line ""compile": "tsc"" in script field, so we can copile the project with command:

>npm run compile

We also use a runtime option with "tsc -w", so we can make the same and use a edit start command in packeage.json, and run with:

> npm start

The packeage.json will seems like: 

```json
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

## Using typescript

Once using typescript we can type the variable in the following way:

```typescript
  private _data: Date,
  private _quantidade: number,  
  private _valor: number
```

### Dom elements

When we select a elemento from "DOM" we receive a generic type "Element". This type can representa a input, label h1 and so on. For access the value of a input we need use ".value", and ".contentText" for a h1 or label. Because this we often need make a cast to a more specifc type.

```typescript
this._inputValor = <HTMLInputElement> document.querySelector('#valor');
```

### conversions

Once we define a type like "number" or "Date", often we are need convert a received value to this types, for exemple:

```typescript
  new Date(this._inputData.value.replace(/-/g, ',')),
  parseInt(this._inputQuantidade.value),
  parseFloat(this._inputValor.value));
```

### Types

When we create a Array we can specify the type of datas that this array will receive:

```typescript
private _negociacoes: Array<Negociacao>;
```

We also can declarete the type of return of a function:

```typescript

    paraArray(): Negociacao[] {

        return [].concat(this._negociacoes);
    }
```

Or:

```typescript
    update(model: Negociacoes): void{
        this._elemento.innerHTML = this.template(model)
    }
```

### Generics

Typescript allows us use generic in a class, therefore we can "subscribe" a parameter for usin diferents types em different subclass:

```typescript
 class View<T> {
   //... omitted
 }
```

### Abstract

Typescript also allows use of abstract classes and methods.

### Class

```typescript
 abstrct class View<T> {
   //... omitted
 }
```

### Methods

```typescript
abstract template(model: T): string;
```

### Libs

Typescript can't undestand gloobal variables of external libs like JQuery. So, to resolve this we can use TypeScript definitons files (tsd). For exemple, https://www.npmjs.com/package/@types/jquery is a tsd for JQuery libs.
If the lib have no a tsd, we can use the "declare var strategy". when we create a variable declared like "any" to avoid that the code do't be copiled.

```typescript
declare var $: any;
protected _elemento: any;
```

### Namespaces

Naespaces in typescript allow us separate a code in packages, like JAVA or c#, also enables that pre-processor use autocomplete to sugest a class to help us.

```typescript
namespace Views {

    export abstract class View<T> {
      //...omitted
    }
}
```

And the chield classes

```typescript
namespace Views {

    export class MensagemView extends Views.View<string> {
      // ...omitted
    }
}
```

### Modules

The namespaces can't resolve the problem of inportation depence. To resolve this we need use module sistem of ES2015. In ES2015 each scrpt is a module, and we can "import" and "export" this artfacts.

```typescript
export abstract class View<T> {
  // ...omitted
}
```

and

```typescript
import { View } from './View';
export class NegociacoesView extends View<Negociacoes> {
  // ...omitted
}
```

For this to work we need add a lib like "System.js", to management modules. First we adjust "tsconfig.json" to use "System.js"

```json
{
    "compilerOptions": {
        "target": "es6",
        "outDir": "app/js",
        "noEmitOnError": true, 
        "noImplicitAny": true,
        "removeComments": true,
        "module": "system"
    },
    "include": [
        "app/ts/**/*"
    ]
}
```

So we add globaly the "System.js" and the first module. In HTML file.

```html
    <script src="lib/system.js"></script>
    <script>
         System.defaultJSExtensions = true;
        System.import('js/app.js').catch(err => console.error(err));
    </script>
```

This strategy above have a error, the "System.js" use server request to work. So we need run this code in a server. We can use the "lite-server".
>npm install lite-server@2.3.0 --save-dev

After install we can config "package.json" to run the server and the ts copiler concurrently and still have the benefit of "live-reload"

```json
{
  "name": "alurabank",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "compile": "tsc",
    "server": "lite-server --baseDir=app",
    "start": "concurrently \"npm run watch\" \"npm run server\""
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "@types/jquery": "^2.0.42",
    "lite-server": "^2.3.0",
    "typescript": "^2.3.2"
  }
}
```

We can improve the modules importation with barrel strategy. First we create in each folder a index file that export the modules.

```typescript
// app/ts/views/NegocicaoesView.ts
export * from './View'
export * from './MensagemView'
export * from './NegociacoesView'
```

So we can import the modules.

```typescript
// app/ts/controllers/NegociacaoController.ts
import { NegociacoesView, MensagemView } from '../views/index';
```