# async/await

**Articles:**
- [async function](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Statements/async_function)
- [Всё, что нужно знать об async/await](https://medium.com/@stasonmars/%D0%B2%D1%81%D0%B5%CC%88-%D1%87%D1%82%D0%BE-%D0%BD%D1%83%D0%B6%D0%BD%D0%BE-%D0%B7%D0%BD%D0%B0%D1%82%D1%8C-%D0%BE%D0%B1-async-await-%D1%86%D0%B8%D0%BA%D0%BB%D1%8B-%D0%BA%D0%BE%D0%BD%D1%82%D1%80%D0%BE%D0%BB%D1%8C-%D0%BF%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%B2-%D0%BE%D0%B3%D1%80%D0%B0%D0%BD%D0%B8%D1%87%D0%B5%D0%BD%D0%B8%D1%8F-76dde2cb6949)


Заметки:
- синтаксис `async/await` позволяет писать асинхронный код с синхронном стиле
- `async` function возвращает промис (или объект `AsyncFunction`) ㄟ( ▔, ▔ )ㄏ
- `await` работает только внутри `async` функции
- `async` может не сожержать внутри `await`
- чтобы вернуть промис в функцию, нужно ставить перед этой функцией `async`
- чтобы вызвать промис из функции, нужно ставить `await`
- отлавливать ошибки можно с помощью конструкции `try / catch` или в цепочке промисов
- `Promise.all` для параллельного выполнения массива промисов