Crear un proyecto vite para trabajar con typescript:
 ```bash
npm create vite@latest 
 ```

Vite corre sobre node en estos momentos

## Tipos básicos
```ts
const name: string = "Strider";
let hpPoints: number | "FULL" = 95
const isAlive: boolean = true;

hpPoints = "FULL";

console.log({
  name,
  hpPoints,
  isAlive,
});

export {};
```
