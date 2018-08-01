title: Networks
class: animation-fade
layout: true

---

class: impact

# HTTP
## и сын его REST

---

# Зачем HTTP?

--

* Чтобы <big><strong>Г̹̲͇̾̚И̩̙͔̼̻̠̊͛П̫ͦ̐Е̣̊͛̌̏ͨР̮͎̱̦̗ͨ̿̐̉М͎̮̀͒̔ͫ̍Е͈̼̳̬ͨ͊ͩ̎̎̆Д̼͖͖̲̗̒И͌̐ͧА̾̈</strong></big>

--

* _Очень много крайне различной_ информации

--

* _Много_ разных агентов c _различными_ задачами

--

* _Малый_ порог входа и участия

---

# Что такое HTTP?

По крайней мере HTTP/1.1. 😓

## Задачи

--

* Организовать обмен <big>**ГИПЕРМЕДИА**</big>

--

* Обеспечить равноправие различных агентов

--

* Дать возможность плавной эволюции протокола и систем

--

* Минимизировать порог входа

---

# Что такое HTTP?

## Участники

--

* пользователькие агенты

--

* веб-сервисы

--

* посредники
    - прокси
    - кэширующие сервера
    - файрволлы

---

# Что такое HTTP?

## Сообщения и формат данных

--

```http
GET /user HTTP/1.1
Host: api.github.com
User-Agent: insomnia/5.16.6
Accept: application/vnd.github.v3+json
Authorization: token 17561dd75d2d4ca18162aa0ee6689ad352f7c716
```

---

# Что такое HTTP?

## Сообщения и формат данных

```http
HTTP/1.1 200 OK
Server: GitHub.com
Date: Mon, 30 Jul 2018 19:07:46 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 1173
X-RateLimit-Limit: 5000
X-RateLimit-Remaining: 4999
X-RateLimit-Reset: 1532981266
Cache-Control: private, max-age=60, s-maxage=60
Vary: Accept, Authorization, Cookie, X-GitHub-OTP
ETag: "43e7e661929a522cbf07d1254805b17e"
Last-Modified: Wed, 11 Jul 2018 15:47:47 GMT

... куча байтов тела ответа ...
```

---

# Зачем REST?

--

* _Очень много_ участников

--

* _Очень часто_ появляются новые

--

* _Очень много_ способов решить задачу

--

* _Крайне мало_ средств общаться на "одном языке"

---

# Что такое REST?

--

* Клиент-серверная архитектура систем

--

* Коммуникация посредством явной передачи состояния

--

* Средства для явного, предсказуемого и безопасного кэширования

--

* Многоуровневая архитектура с разделением задач между уровнями

--

* **Унифицированный интерфейс**

---

## Унифицированный интерфейс

--

* Ресурсы и их расположения в сети

--

* Представления ресурсов

--

* Явные и понятные учатникам без предварительного знания сообщения

--

* <big><strong>Ḥ̹̮͖ͬͧ̆ͧA̦͍͕̮͊́ͦ̆ͯT̹̘̭̱̪ͫE̲͎̖͇̦͋̇̓O̬̻͕̩̣̗ͨ͑̃ͤÂ͐S̯̘̘̟̪͔̀͊́ͤ</strong></big>

---

### Ресурсы и их расположения

#### URL

```
URI = scheme:[//authority]path[?query][#fragment]
```

```
authority = [userinfo@]host[:port]
```

--

#### Примеры

* Github Repository Issues

    ```
    https://github.com/stevemao/left-pad/issues
    ```

--

* Github Logged-in User Settings

    ```
    https://github.com/settings/profile
    ```

---

### Представления ресурсов

```http
GET /v0/item/17621448.json?print=pretty HTTP/1.1
Host: hacker-news.firebaseio.com
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,ru-RU;q=0.8,ru;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate, br
```

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 697

{
  "by" : "captain_perl",
  "id" : 17621448,
  "kids" : [ 17621675, 17621623 ],
  "parent" : 17620543,
  "text" : "Just for the record, I surveyed a dozen Hipchat users who used it all day in late 2016 for software development. They had zero complaints about using Hipchat.<p>My opinion of the Hipchat web client at the time was that it worked fine (no complaints from me.)<p>I believe we were on the free tier, so that was a great deal.<p>A new Eng. VP wanted to seem hip, so he switched us to Slack &quot;to ensure we were using the best tools possible.&quot;<p>Nobody said that Slack was better or added any features that were worth mentioning.",
  "time" : 1532640989,
  "type" : "comment"
}
```

---

### Понятные сообщения

#### Методы

--

* **GET**

    Получить _представление_ ресурса, расположенного по URL.
--
 В ответе присутствует _тело_ с представлением ресурса.
--
 _Безопасный_ метод.
--
 _Идемпотентный_ метод.
--
 Позволено _кэшировать_.

--

* **HEAD**

    Получить _метаданные_ ресурса, расположенного по URL.
--
 В ответе отсутствует _тело_ с представлением ресурса.
--
 _Безопасный_ метод.
--
 _Идемпотентный_ метод.
--
 Позволено _кэшировать_.

--

* **POST**

    Создать _подресурс_ в рамках расположенного по URL ресурса согласно переданному представлению.
--
 В ответе присутствует _тело_ с представлением созданного ресурса.
--
 _Небезопасный_ метод.
--
 _Неидемпотентный_ метод.
--
 Позволено _кэшировать_.

---

### Понятные сообщения

#### Методы

* **PUT**

    Задать _состояние_ расположенного по URL ресурса согласно переданному представлению.
--
 В ответе присутствует _тело_ с представлением созданного или изменённого ресурса.
--
 _Небезопасный_ метод.
--
 _Идемпотентный_ метод.
--
 Недопустимо _кэшировать_.

--

* **PATCH**

    Внести _частичные изменения_ в состояние расположенного по URL ресурса согласно переданному представлению.
--
 В ответе присутствует _тело_ с представлением созданного или изменённого ресурса.
--
 _Небезопасный_ метод.
--
 _Неидемпотентный_ метод.
--
 Недопустимо _кэшировать_.

--

* **DELETE**

    Удалить расположенный по URL ресурс.
--
 В ответе отсутствует _тело_.
--
 _Небезопасный_ метод.
--
 _Идемпотентный_ метод.
--
 Недопустимо _кэшировать_.

---

### Понятные сообщения

#### Классы ответов

* **1XX Informational**

    _Информация для ознакомления_. Обычно используется для согласования обновления прикладных протоколов.

--

* **2XX Success**

    _Успех_. Запрошенное агентом действие было корректно сформулировано, получено и успешно обработано.

--

* **3XX Redirection**

    _Необходимы дополнительные действия_, чаще всего используется для перенаправления агента для совершения действия над _другим_ ресурсом.

---

### Понятные сообщения

#### Классы ошибок

* **4XX Client Error**

    _Агент допустил ошибку_ в процессе формирования запроса, его отправки или в результате попытки проведения действия, неприменимого к текущему состоянию ресурса. Чтобы добиться успеха, агент имеет возможность _скорректировать_ свой запрос.

--

* **5XX Server Error**

    _Сервер не в состоянии обработать запрос_ в результате какой-либо ошибки. Ошибочное состояние может быть _постоянным_ или _временным_ (_транзиентная_ ошибка). Обычно агент не имеет возможности в итоге добиться успеха.

---

## HATEOAS

**H**ypermedia **a**s **t**he **e**ngine **o**f **a**pplication **s**tate

> When I say hypertext, I mean the simultaneous presentation of information and controls such that the information becomes the affordance through which the user (or automaton) obtains choices and selects actions.
>
> <cite>Roy Fielding в своём [блоге](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven#comment-718)</cite>

--

### [https://apidocs.goabout.com](https://apidocs.goabout.com)

---

class: impact

# Ну и хватит
## всё равно в REST никто нормально не может
