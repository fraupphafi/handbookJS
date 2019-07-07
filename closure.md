## Функции ##
При создании функция получает скрытый объект `[[Scope]]`
При каждом вызове функции у неё появляется лексическое окружение

Брать переменные из замыкание - брать переменные из текущего лексического окружения через [[Scope]]

У new Function() [[Scope]] равен window

Свойства и методы функции доступны из внешнего кода.
Функции и переменные объявленные внутри функции - приватны.

## this ##
this - контекст вызова. Определяется тем, где и как вызвана функция.
this у function() берется там, где эта функция определена.
this у () => берется там, где она вызвана (определяется лексикой).

Контекст this никак не привязан к функции, даже если она создана в объявлении объекта. Чтобы this передался, нужно вызвать функцию именно через точку (или квадратные скобки).

## new Function (конструкторы) ##
Пример функции-конструктора с вспомогательными локальными переменными и функциями

```
function User(firstName, lastName) {
  // вспомогательная переменная
  var phrase = "Привет";
  //  вспомогательная вложенная функция
  function getFullName() {
      return firstName + " " + lastName;
    }
  this.sayHi = function() {
    alert( phrase + ", " + getFullName() ); // использование
  };
}
var vasya = new User("Вася", "Петров");
vasya.sayHi(); // Привет, Вася Петров
```

## call, apply ##
`func.call(context, arg1, arg2, ...)`
При этом вызывается функция func, первый аргумент call становится её this, а остальные передаются «как есть».
Вызов func.call(context, a, b...) – то же, что обычный вызов func(a, b...), но с явно указанным this(=context).

`func.apply(context, [arg1, arg2])`
Вызов функции при помощи func.apply работает аналогично func.call, но принимает массив аргументов вместо списка.

## bind ##
Привязка контекста
`var wrapper = func.bind(context[, arg1, arg2...])`


## Дескриптор ##
Метод Object.defineProperty() определяет новое или изменяет существующее свойство непосредственно на объекте, возвращая этот объект.
`Object.defineProperty(obj, prop, descriptor)`
Параметры:
- `obj` - Объект, на котором определяется свойство.
- `prop` - Имя определяемого или изменяемого свойства.
- `descriptor` - Дескриптор определяемого или изменяемого свойства.

```
"use strict";
var user = {};
Object.defineProperty(user, "name", {
  value: "Вася",
  writable: false, // запретить присвоение "user.name="
  configurable: false // запретить удаление "delete user.name"
});
// Теперь попытаемся изменить это свойство.
// в strict mode присвоение "user.name=" вызовет ошибку
user.name = "Петя";
```

### get set ###
Дескриптор позволяет задать свойство, которое на самом деле работает как функция.
get используется для чтения значения, set для записи

```
var user = {
  firstName: "Вася",
  surname: "Петров"
}
Object.defineProperty(user, "fullName", {

  get: function() {
    return this.firstName + ' ' + this.surname;
  },
  set: function(value) {
      var split = value.split(' ');
      this.firstName = split[0];
      this.surname = split[1];
    }
});
user.fullName = "Петя Иванов";
alert( user.firstName ); // Петя
alert( user.surname ); // Иванов
```

get, set можно задавать прямо в определении объекта
```
...  **get** fullName() {
    return this.firstName + ' ' + this.surname;
  },

  **set** fullName(value) {
    var split = value.split(' ');
    this.firstName = split[0];
    this.surname = split[1];
  }
...
```

## ()=> ##
this определяется лексическим окружением.
Вызов с помощью call() и aplly() не влияет на this, даже если передать параметры.
Нет собственного объекта arguments. Будет ссылаться на внешний объект. Лучшая замена rest-параметр.
Не подходят для использования как методов.


### Итого про this ###
Значение this устанавливается в зависимости от того, как вызвана функция:
- При вызове функции как метода:
```
obj.func(...)    // this = obj
obj["func"](...)
```
- При обычном вызове:
```
func(...) // this = window (ES3) /undefined (ES5)
```
- В new:
```
new func() // this = {} (новый объект)
```
- Явное указание:
```
func.apply(context, args) // this = context (явная передача)
func.call(context, arg1, arg2, ...)
```