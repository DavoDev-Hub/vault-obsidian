Quién se ejecuta primero?
```js
setTimeout(cb1, 0);
Promise.resolve().then( cb2 );
process.nextTick( cb3 );
fs.readFile( 'file.txt', cb4 );
setImmediate( cb5 )
```
Es el event loop el que lo va a saber

Hay un problema muy grande que node tuvo que resolver, js por defecto es blocking y single threaded, la mayor parte del js es blocking

```js
while (true){
	// procedimiento
}

moreWork(); // <- Nunca se ejecutará
```

### componentes de Node
- Dependencias externas
- Características de C++
- Librerías de JS que se conectan con C++ desde nuestro código

#### libuv 
Su role principal es manejar todas las operaciones asíncronas

#### Ejecución de codigo
- Cuando ejecutamos el node, node crea una funcion global, Global() -> main()
	- Primero despues de barrer todo el archivo y leer referencias
	- Node agarra la primer linea y la pone en el Call Stack, la registra y la elimina
	- asi con todas las demas lineas
	- Cuando todo termina el extatus code es 0
- Hay funciones que se guardan en el libuv, el demas codigo se corre y queda pendiente lo de libuv, para despues mandarlo al call stack y ejecutarlo despues de que el programa haya finalizado las demas lineas


#### Event loop

Sigue ciertas reglas
1. Callbacks en el microtask se ejecutan primero
2. Todos los callbacks dentro del timer queue se ejecutan
3. Callbacks en el microtask queue (si hay) se ejecutan despues de los callback timers, primero tareas en el nextTick queue y luego tareas en el promise queue
4. Callbacks de I/O se ejecutan
5. Callbacks en el microtask queue se ejecutan ( si hay), y luego promise queue (si hay)
6. Todos los callbacks en el check queue se ejecutan
7. Callbacks en  el microtask se ejecutan despues de cada callback en el check queue. (Siguiendo el mismo orden anterior, nextTick y luego promise)
8. Todos los callbacks en el close queue son ejecutados
9. Por ultima vez en el mismo ciclo, los microtask queues son ejecutados de la misma forma, nextTick y luego promise queue


