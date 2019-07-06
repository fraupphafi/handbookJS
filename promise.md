# Promise #

Promise – это специальный объект, который содержит своё состояние. Вначале pending («ожидание»), затем – одно из: fulfilled («выполнено успешно») или rejected («выполнено с ошибкой»).

Синтаксис создания Promise:
```
var promise = new Promise(function(resolve, reject) {
  // Эта функция будет вызвана автоматически

  // В ней можно делать любые асинхронные операции,
  // А когда они завершатся — нужно вызвать одно из:
  // resolve(результат) при успешном выполнении
  // reject(ошибка) при ошибке
})
```

Синхронный throw – то же самое, что reject
`throw new Error("o_O");`

Универсальный метод для навешивания обработчиков:
`promise.then(onFulfilled, onRejected)`
- `onFulfilled` – функция, которая будет вызвана с результатом при resolve.
- `onRejected` – функция, которая будет вызвана с ошибкой при reject.


**Promise после reject/resolve – неизменны**

## «Чейнинг» (chaining) ##
Асинхронные цепочки из промисов

```
httpGet(...)
  .then(...)
  .then(...)
  .then(...)
```
**Если очередной then вернул промис, то далее по цепочке будет передан не сам этот промис, а его результат.**

`.catch(error)` - обработчик на ошибку 