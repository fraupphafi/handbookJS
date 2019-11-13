# async/await

**MDN:**
- [async function](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Statements/async_function)


Заметки:
- синтаксис `async/await` позволяет писать асинхронный код с синхронном стиле
- async function возвращает промис (или объект AsyncFunction) ㄟ( ▔, ▔ )ㄏ
- await работает только внутри async функции
- async может не сожержать внутри await
- чтобы вернуть промис в функцию, нужно ставить перед этой функцией async
- чтобы вызвать промис из функции, нужно ставить await
- отлавливать ошибки можно с помощью конструкции `try / catch` или в цепочке промисов