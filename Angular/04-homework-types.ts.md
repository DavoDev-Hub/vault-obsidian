cuando tenemos una interfaz dentro de otra interfaz es mejor crear una aparte,
es mejor practica para la escalabilidad
```ts
interface SuperHero {
  name: string;
  age: number;
  address: Address;
  // {
  //    calle: string;
  //    pais: string;
  //    ciudad: string;
  //  };
  showAddress: () => string;
}

interface Address {
  street: string;
  country: string;
  city: string;
}

const superHeroe: SuperHero = {
  name: "Spiderman",
  age: 30,
  address: {
    street: "Main St",
    country: "USA",
    city: "NY",
  },
  showAddress() {
    return this.name + ", " + this.address.city + ", " + this.address.country;
  },
};

const address = superHeroe.showAddress();
console.log(address);

export {};

```