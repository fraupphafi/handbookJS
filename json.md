# JSON


## `JSON.parse` – читает объекты из строки в формате JSON.

```
let user = '{ "name": "Вася", "age": 35, "isAdmin": false, "friends": [0,1,2,3] }';

user = JSON.parse(user);

alert( user.friends[1] ); // 1
```
### Умный разбор JSON.parse(str, reviver)
Параметр reviver является функцией function(key, value).

```
// дата в строке - в формате UTC
let str = '{"title":"Конференция","date":"2014-11-30T12:00:00.000Z"}';

let event = JSON.parse(str, function(key, value) {
  if (key == 'date') return new Date(value);
  return value;
});

alert( event.date.getDate() ); // теперь сработает!
```



## `JSON.stringify(value, replacer, space)` – превращает объекты в строку в формате JSON.

```
var user = {
  name: "Вася",
  age: 25,
  window: window
};

var str = JSON.stringify(user, function(key, value) {
  if (key == 'window') return undefined;
  return value;
});

alert( str ); // {"name":"Вася","age":25}
```

```
var user = {
  name: "Вася",
  age: 25,
  roles: {
    isAdmin: false,
    isEditor: true
  }
};

var str = JSON.stringify(user, "", 4);

alert( str );
/* Результат -- красиво сериализованный объект:
{
    "name": "Вася",
    "age": 25,
    "roles": {
        "isAdmin": false,
        "isEditor": true
    }
}
*/
```

Строки в JSON должны обязательно содержать двойные кавычки