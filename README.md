# sjsg / Signaltech Javascript Style Guide

[![Code Climate](https://codeclimate.com/github/sorx00/sjsg/badges/gpa.svg)](https://codeclimate.com/github/sorx00/sjsg)

## Содержание

1. [Общие моменты](#general)
1. [Отступы](#indentation)
1. [Длина строки](#linelen)
1. [Комментарии](#comments)
1. [Имена](#names)
1. [Объявление переменных](#variables)
1. [Объявление функций](#functions)
1. [Инструкции, операторы и выражения](#statements)
  - [Простые](#simple)
  - [Блочные](#compound)
  - [return](#return)
  - [if](#if)
  - [try](#try)
  - [for](#for)
  - [while](#while)
  - [do](#do)
  - [switch](#switch)
  - [with](#with)
  - [eval](#eval)
1. [Строки](#strings)
1. [Массивы](#arrays)
1. [Объекты](#objects)
1. [И ещё...](#addons)
1. [Линтеры JSHint/JSCS](#using)
  - [SublimeText](#sublimetext)
  - [PhpStorm](#phpstorm)
  - [Brackets](#brackets)


## <a name="general"></a>Общие моменты

* Используйте по-возможности краткие формы;
* {} — вместо new Object();
* [] — вместо new Array();
* Используйте инкремент `i++` и декремент `i--`;
* Используйте точное сравнение без приведения типов: `a === b` и `a !== b`;
* Допускается приведение типа при проверке на `undefined`, `null` или пустую строку`''` через `!varName`;
* Для приведения к булевому типу используйте `b = Boolean(a)` вместо двойного отрицания `b = !!a`;
* Для приведения к числу используйте краткую запись `b = +a`,
  также можно использовать `b = parseInt(a, 10)`, но не забываете о радиксе: `parseInt(arg, radix)`.

```javascript
var o = {};
var a = [];

// явное приведение типов
i = ParseInt(a[1], 10);
b = Boolean(a[1]);
s = (i + b).toString();

// неявное приведение типов
i = +a[1];
b = !!a[1];
s = '' + i + b;

// тернарный оператор
result = (expression) ? operand1 : operand2;
или
result = expression ? operand1 : operand2;
```

* Используйте запятые после, а не перед декларацией:

##### Плохо

```javascript
var iAm = {
    firstName:  'Ildar'
  , lastName:   'Gal'
  , age:        36
};
```

##### Хорошо

```javascript
var iAm = {
    firstName: 'Ildar',
    lastName: 'Gal',
    age: 36
};
```


## <a name="indentation"></a>Отступы

Используйте для отступов двойной пробел.
Отсутствие стандарта по ширине символа табуляции приводит к тому, что код выглядит по разному в различных редакторах и IDE.

В конце файлов оставляйте пустую строку.

  ```javascript
  (function() {
  ←←...
  })();
  ↵
  ```


## <a name="linelen"></a>Длина строки

Длина строки не должна превышать 100 символов.


## <a name="comments"></a>Комментарии

- Используйте  `/* ... */` для многострочных и `// ...` для однострочных комментариев;
- Для описания методов и свойств/переменных используется формат jsDoc:
```javascript
/**
 * Описание метода/переменной/свойства
 * @param {type} propName описание аргумента
 */
```
- Не пишите инлайновые комментарии;
- Отбивайте комментарии пустой строкой сверху.
  
##### Плохо

  ```javascript
  var true = false,   // наебал
      a = 1;          // умный комментарий про переменную
  
  function do(what) {
    var a = 1;
    // blah-blah
    // foo
    // bar
    var b = what || '';

    return b;
  }
  ```

##### Хорошо

  ```javascript
  // Наебал
  var true = false;

  // умный комментарий
  var a = 1;
  
  /**
   * @param {string|undefined} what Строка, которая ест коров
   * @return {string}
   */
  function do(what) {
    /*
      blah-blah
      foo
      bar
    */
    var b = what || '';

    return b;
  }
  ```


## <a name="names"></a>Имена

В именах можно использовать только буквы латинского алфавита, цифры и символ подчеркивания ([A-Za-z0-9_]).

* **camelCase** — для имен переменных, публичных методов и свойств;
* **_privateVar** (с ведущим подчеркиванием `_`) — для приватных свойств;
* **UPPER_CASE** — для констант;
* **PascalCase** — для классов, имен конструкторов, namespace'ов;

В именах переменных и функций нельзя использовать зарезервированные слова:
`var`, `array`, `object`, `null`, `arguments`, `call`, `apply`, `case`, `default`, ...

Имя переменных и функций должно отражать их смысл. Имя функция должно выражать действие. 
Если после недолгого размышления вы решили назвать переменную *r_chkbx* — подумайте еще.


## <a name="variables"></a>Объявление переменных

* Не используйте глобальные переменные;
* Переменные должны быть объявлены cверху;
* Каждая переменная должна быть объявлена на новой строке с индивидуальным `var`;
* Переменные желательно группировать по смыслу, а затем по алфавиту;
* Неинициализированные переменные объявляйте последними;
* Не используйте имена, которые уже определены во внешней области видимости.

##### Плохо

```javascript
z = 0;                          // переменная объявляется ниже как локальная

var x,y;                        // один var на несколько переменных
var uselessVar = 'useless text' // инициализированные переменные должны стоять в начале

function square(x) {            // 'x' уже определена во внешнем скоупе
  return x*x;
}

var label = 'Coding is cool!';
var z;                          // по смыслу эта переменная должна стоять рядом с 'x' и 'y'
```

##### Хорошо

```javascript
var label = 'Coding is cool!';
var uselessVar = 'useless text';
var x;
var y;
var z;

function square(arg) {
  return arg * arg;
}
```


## <a name="functions"></a>Объявление функций

* Объявляйте функции до первого использования, в начале блока, но после объявления переменных;
* Не декларируйте функции внутри блоков `if`, `for` и т. д.;
* Между именем функции и открывающей скобкой не должно быть пробела;
* Между закрывающей скобкой и открывающей фигурной скобкой должен быть пробел;
* Блок тела функции должен открываться на одной строке с именем функции;
* Для изоляции и замыканий используйте немедленно-выполняемый функтор ([IIFE on MDN](https://developer.mozilla.org/ru/docs/Glossary/IIFE)).

##### Плохо

```javascript
function doSomethingUseful (){
  // here is no nothing useful in real
}

function anotherFunc()
{
  // body
}

if (true) {
  function good() { ... }
}

/**
 * Comment
 */

function a() {
  
}
function b() {
  
}
```

#####  Хорошо

```javascript
function doSomethingUseful() {
  // here is no nothing useful in real
}

function a() {
  
}

/**
 * Comment 
 */
function b() {
  
}
```


## <a name="statements"></a>Инструкции, операторы и выражения

### <a name="simple"></a>Простые

Размещайте каждую инструкцию на новой строке. Все инструкции кроме блочных
завершаются символом `;`.

> Ребята, давайте жить дружно и не забывать ставить точку с запятой!

##### Плохо

```javascript
var i=0; i=i+1;return i

if (true) {
  
};
```

##### Хорошо

```javascript
var i = 0;
++i;
return i;

function a() {
  
}

var functionVariable = function() {
  
};
```


### <a name="compound"></a>Блочные

* Блоки инструкций заключаются в фигурные скобки `{` и `}`;
* Открывающая скобка завершает строку и не переносится на новую;
* Закрывающая скобка, напротив, переносится на следующую строку, кроме случаев с однострочными блоками;
* Используйте блок даже для одиночного выражения;
* Разделяйте блоки пустой строкой. Если над функцией комментарий, то пустой
 строки не должно быть.

##### Плохо

```javascript
/**
* Comment
* @param {object} username 
*/

var superSu = function (username)
{username.evilmode = true}

if (true) return false;
```

##### Хорошо

```javascript
/**
* Comment
* @param {object} username 
*/
var superSu = function(userName) {
  userName.godMode = true;
}
// Фильтр четных чисел
[1, 2, 3, 4].filter(function(number) {
  return !(number % 2);
});

if (true) { return false; }
```


### <a name="return"></a>return

Не заключайте в скобки возвращаемый объект и не переносите его на новую строку.

##### Плохо

```
return
  a;

return (a);
```

### <a name="if"></a>if

* Ставьте пробел перед круглыми скобками и после них;
* Правила оформления блока описаны в соответствующем разделе.

##### Плохо

```javascript
if(){
  ...
}

if ()
{
  ...
} else
{ ... }
```

##### Хорошо

```javascript
if (...) {
  ...
} else if (...) {
  ...
} else {
  ...
}
```


### <a name="try"></a>try

```javascript
try {
  ...
} catch (...) {
  ...
} finally {
  ...
}
```


### <a name="for"></a>for

* Не объявляйте статические переменные в теле цикла;
* Не объявляйте функции в теле цикла.
* При переборе объектов в конструкции `for...in` используйте обертку `hasOwnProperty` для исключения из перечисления свойств, добавленных в прототип;

##### Плохо

```javascript
var items = [ ... ];
for(i=0;i<len; i=i+1)
{
  len = items.length;
  function do(a,b) { ... }
  do(i, items[i]);
}

for(a in b){ if(b.a<10) return false }
```

##### Хорошо

```javascript
function do(i, item) {
  ...
}

for(var i = 0, len = items.length; i < len; i++) {
  do(i, item[i]);
}

for (var key in object) {
  if (object.hasOwnProperty(key)) {
    if (b.a < 10) {
      return false;
    }
  }
}
```


### <a name="while"></a>while

```javascript
var n = 0;
var x = 0;

while (n < 3) {
  n++;
  x += n;
}
```


### <a name="do"></a>do

```javascript
var i = 0;

do {
   i += 1;
   console.log(i);
} while (i < 5);
```


### <a name="switch"></a>switch

Завершайте каждый блок кроме `default` оператором `break` или `throw`.

```javascript
switch (...) {
  case value1:
    ...
    break;
  
  case value2: return ...;
  
  default:
    throw ...;
}
```


### <a name="with"></a>with

Никогда не используйте `with`.

[with Statement Considered Harmful](http://yuiblog.com/blog/2006/04/11/with-statement-considered-harmful/)


### <a name="eval"></a>eval

Никогда не используйте `eval`.

> eval is Evil


## <a name="strings"></a>Строки

* Используйте одинарные кавычки, конкатенируйте длинные строки;
* Для новых стандартов используйте [шаблонные литералы](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/template_strings)

##### Плохо

```javascript
var name = "Vasya";

var longStr = "Note that in the 3d example, '3d' had to be quoted. It's possible to quote the JavaScript array indexes as well (e.g., years['2'] instead of years[2]), although it's not necessary.";

var longStr = "Note that in the 3d example, '3d' had to be quoted. \
Possible to quote the JavaScript array indexes as well (e.g.,  \
years['2'] instead of years[2]), although it's not necessary. The 2 ";
```

##### Хорошо

```javascript
var name = 'Vasya';

var longStr = 'Note that in the 3d example, \'3d\' had to be quoted.' +
  'Possible to quote the JavaScript array indexes as well (e.g., ' +
  'years['2'] instead of years[2]), although it\'s not necessary. The 2';

или

var longStr = `Example ${varName}, something`;
```


## <a name="arrays"></a>Массивы
* При инициализации массива после последнего элемента допустима запятая;
* Используйте методы: `push`, `map`, `forEach`, `filter`, `some`, `every`, `slice`.

##### Плохо

```javascript
a[a.length] = 12;

for (i = 0; i < a.length; i++) {
  a[i] = a[i] + 1;
}

var s = '<ul>';
for (i = 0; i < a.length;i++) s+= '<li>' + a[i] '</li>';
s += '</ul>';

var b = [];
for (i = 0; i < a.length; i++) {
  if (a[i] > 0) b[i] = a[i];
}

var aCopy = [];
for (i = 0; i < a.length; i++) {
  aCopy[i] = a[i];
}
```

##### Хорошо

```javascript
var a = [1,2,3,];

a.push(12);

a.forEach(function(i) {i += 1;});

var s = '<ul><li>' + items.join('</li><li>') + '</li></ul>';

var aCopy = a.slice();

var b = a.filter(function(i) { return i>0; });

// чтобы получить массив свойств
var myObj = {a: 1, b: 2, c: 3, d: 'bubble-gum', e: 5};
myObj.length = Object.keys(myObj);
var myArr = Array.prototype.slice.call(myObj);
```

## <a name="objects"></a>Объекты

* Используйте `this.foo = undefined` вместо `delete this.foo` (это быстрее работает);
* Обращение к свойству осуществляется через `obj.propertyName`, а не `obj['propertyName']`,
за исключением, когда имя свойство хранится в переменной `obj[variable]`.

##### Плохо
```javascript
var x = {y: 123};

delete x.y;
// или
x.y = null;
// или
x['y'] = undefined;
```


##### Хорошо
```javascript
x.y = undefined;
```

## <a name="addons"></a>И ещё…

* CoffeScript — нет.
* jQuery — нет.
* Bootstrap — нет. Используйте вместо него sega3.
* Сеттеры и геттеры — пока нет, ждем внедрения ES6.
  ```javascript
  // плохо
  var name = user.getName();
  user.setName('Vasya');

  // хорошо
  var name = user.name();
  user.name('Vasya');

  ```
* Object.defineProperty — да.


## <a name="using"></a>Линтеры JSHint/JSCS

* Скопируйте в корень проекта конфигурационные файлы:
  + `linters/signaltech.jshintrc`,
  + `linters/signaltech.jscsrc`;
* Переименуйте:
  + `signaltech.jshintrc` => `.jshintrc`,
  + `signaltech.jscsrc`   => `.jscsrc`;
* Установите `jshint` и `jscs`:
```bash
npm install -g jshint
npm install -g jscs
```
* Запустите проверку:
```bash
# из каталога с конфигурационными файлами
jshint src/app.js
jscs src/app.js

# из другого каталога
jshint /path/to/file.js --config /path/to/jshint.config
jscs /path/to/file.js --config /path/to/jscs.config

# автоматическое исправление ошибок
jscs /path/to/file.js --config /path/to/jscs.config --fix
```


### <a name="sublimetext"></a>SublimeText

В данной инструкции мы подразумеваем, что модуль `Package Control` уже установлен, если нет - следуйте указаниям в документации: [Package Control Installation](https://packagecontrol.io/installation)

Для подключения линтеров в SublimeText необходимо установить фреймворк `SublimeLinter`. 
* Нажимаем `Ctrl + Shift + P`, для вызова командной консоли;
* Запрашиваем список пакетов, набрав `install package` (пункт `Package Control: Install Package`);
* Устанавливаем пакет с именем `SublimeLinter`, выбрав его в списке.

Сам по себе фреймворк не содержит линтеров, они находятся в отдельных модулях. Устанавливаем пакеты `SublimeLinter-jshint` и `SublimeLinter-jscs` указанным выше методом.

Все должно заработать.
Если ошибки не начали подсвечиваться, попробуйте запустить проверку стандартным сочетанием `Ctrl + k, l`.


### <a name="phpstorm"></a>PhpStorm

> TODO: Добавить инструкцию


### <a name="brackets"></a>Brackets

> TODO: Добавить инструкцию


---


**Signaltech**, 2019
