# Typescript project

## tsconfig file

```json
{
    "compilerOptions": {
        "target": "es6",
        "outDir": "app/js",
        "noEmitOnError": true,
        "noImplicitAny": true
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