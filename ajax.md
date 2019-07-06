# AJAX COMET #

`AJAX` (аббревиатура от «Asynchronous Javascript And Xml») – технология обращения к серверу без перезагрузки страницы.
Форматы получаемых файлов: JSON, HTML, XML, бинарные файлы.

`COMET` -  общий термин, описывающий различные техники получения данных по инициативе сервера. (чаты, аукицоны, ...)

## XMLHttpRequest ##
Объект XMLHttpRequest (или, как его кратко называют, «XHR») дает возможность из JavaScript делать HTTP-запросы к серверу без перезагрузки страницы.

Типовой код запроса
```
var xhr = new XMLHttpRequest();
xhr.open('GET', '/my/url', true);
xhr.send();
xhr.onreadystatechange = function() {
  if (this.readyState != 4) return;
  // по окончании запроса доступны:
  // status, statusText
  // responseText, responseXML (при content-type: text/xml)
  if (this.status != 200) {
    // обработать ошибку
    alert( 'ошибка: ' + (this.status ? this.statusText : 'запрос не удался') );
    return;
  }
  // получить результат из this.responseText или this.responseXML
}
```

`new XMLHttpRequest()` создать новый объект запроса

Методы запроса:
`.open(method, URL, async, user, password)` - конфигурация запроса. Метод(POST GET); адрес(любой протокол, но ограничение безопасности Same Origin Policy); асинхронность (false блокирует работу страницы); user, password – логин и пароль для HTTP-авторизации, если нужны.
`.send(body)` - отправка. Body для POST запроса
`.abort()` -
`.setRequestHeader(name, value)` - устанавливает заголовок
`.getResponseHeader(name)` - читает заголовок
`.getAllResponseHeaders()` - возвращает все заголовки ответа

Свойства XMLHttpRequest:
`timeout` - задает макс продолжительность асинхронного запроса, после будет сгенерировано событие `ontimeout`
`responseText` - текст ответа сервера
`responseXML` - если сервер вернул XML
`status`- код статуса ответа сервера (200, 404, 403, 0)
`statusText` - текстовое представление ответа (OK, Not Found, Forbidden)

События:
`onreadystatechange` - происходит несколько раз в процессе отсылки и получения ответа  
`onerror` - произошла ошибка
`onload` - запрос УСПЕШНО завершен
`onprogress` - браузер получил очередной пакет данных
`onabort` - запрос отменен
`onloadstart` - запрос начат
`onloadend` - запрос завершен

`readyState` - состояние запроса (0 - unset, 1 - open, 2 - headers_receive, 3 - loading, 4 - done);


## XMLHttpRequest: кросс-доменные запросы ##
Access-Control-Allow-Origin
...


## fetch ##
Улучшенный интерфейс для осуществления запросов к серверу на основе промисов

`let promise = fetch(url[, options]);`
`url` – URL, на который сделать запрос,
`options` – необязательный объект с настройками запроса.

Свойства options:
- `method` – метод запроса,
- `headers` – заголовки запроса (объект),
-`body` – тело запроса: FormData, Blob, строка и т.п.
- `mode` – одно из: «same-origin», «no-cors», «cors», указывает, в каком режиме кросс-доменности предполагается делать запрос.
- `credentials` – одно из: «omit», «same-origin», «include», указывает, пересылать ли куки и заголовки авторизации вместе с запросом.
- `cache` – одно из «default», «no-store», «reload», «no-cache», «force-cache», «only-if-cached», указывает, как кешировать запрос.
- `redirect` – можно поставить «follow» для обычного поведения при коде 30x (следовать редиректу) или «error» для интерпретации редиректа как ошибки.

При вызове `fetch` возвращает промис, который, когда получен ответ, выполняет коллбэки с объектом Response или с ошибкой, если запрос не удался.

- `response.headers` - доступ к заголовам
- `response.status` - доступ к статусу

Прочитать тело ответа в желаемом формате
- `response.arrayBuffer()`
- `response.blob()`
- `response.formData()`
- `response.json()`
- `response.text()`