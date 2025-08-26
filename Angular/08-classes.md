
```ts
// Las clases son como moldes para que un objeto luzca de la misma manera

export class Person {
  public name: string;
  private address: string; // solo se puede usar en esta instancia de la clase


  constructor() {
    this.name = "Juan Pablo";
    this.address = "New York";
  }
}

const ironman = new Person();
console.log(ironman);
```

``` ts
// Las clases son como moldes para que un objeto luzca de la misma manera

export class Person {
  //   public name: string;
  //   private address: string;


  //   constructor(name: string, address: string) {
  //     this.name = name;
  //     this.address = address;
  //   }
  constructor(public name: string, private address: string = "No Address") {}

}
// Nueva clase que extiende de personas,
// Proriozar la composicion
// Confia en esto Ts, por eso transpila el codigo
export class Hero extends Person {

  constructor(
    public alterEgo: string,
    public age: number,
    public realName: string
  ) {
    super(realName, "New York");
  }
}


const ironman = new Hero("Ironman", 45, "Tony");

console.log(ironman);
```


// Varias herencias complica el codigo de manera estratosferica
## PRIORIZAR COMPOSICION SOBRE HERENCIA
```ts

```