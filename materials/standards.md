---
title: Стандарты и версии
slideOptions:
  transition: slide
---

# AJS. Стандарты и версии

###### tags: `netology` `advanced js`

---

# План занятия
1. Редакции и стандарты: основные изменения в версиях ES5-ES9
2. ES5: var, ES6: let, const
3. Синтаксис функций в привязке к стандартам ES5 / ES6
4. Перебор итерируемых объектов с помощью for ... of (ES6)
5. ES6: тегированные шаблонные строки

---

# Зачем вообще нужно знать про стандарты и версии стандартов?
- Точно знать какие именно возможности JavaScript можно использовать в конкретном проекте
- Использовать новейшую версию языка, предоставляющую больше возможностей и содержащую меньше недостатков в дизайне языка

---

# Как использовать фишки самых новых стандартов? 
Использовать транспайлеры, например, [Babel](https://babeljs.io)
![](https://i.imgur.com/3KupPdO.png)

:::info
Рассмотрим на следующей лекции
:::

---

# Редакции, стандарты, версии...?

1) Ecma International - организация, которая создает стандарты для технологий
2) **ECMA-262** - это **стандарт**, изданный Ecma International (в нём прописана спецификация скриптового языка общего назначения)
3) **ECMA-262** можно считать учётным номером **ECMAScript**
4) **ES1-ES9** - это **редакции (версии)** стандарта ECMA-262

ECMAScript — стандарт, а JavaScript — самая популярная реализация этого стандарта.

---

# Версии ECMAScript

**ES1**: 1997 
**ES2**: Июнь 1998 
**ES3**: Декабрь 1999 
 **ES4**: так и не была принята
**ES5**: Декабрь 2009
**ES6 / ES2015**
**ES7 / ES2016
ES8 / ES2017
ES9 / ES2018
ES.Next**

---

# ES5

* Strict mode — специальная директива `"use strict"` указывается для перевода кода в режим полного соответствия ES5 (с отсутствием полной обратной совместимости)
* объект `JSON` с методами `parse`, `stringify`
* новые методы `Array` (`indexOf`, `lastIndexOf`, `forEach`, `map`, `filter`, `reduce`)
* новые методы `Object` и др.

---

# ES6 / ES2015

* `let`, `const`
* стрелочные функции
* параметры по умолчанию
* `spread` / `rest` оператор
* деструктуризация массивов и объектов
* тегированные шаблонные строки
* итераторы и генераторы
* `Promise`
* новый синтаксис для классов
* тип данных `Symbol`
* контейнерные типы: `Map`, `WeakMap`, `Set`, `WeakSet`
* и др.

---  
 
#  ES7 / ES2016

* метод `includes` для класса `Array`
* оператор для возведения в степень `**` (вместо `Math.pow`)

---

# ES8 / ES2017

* конструкция `async`/`await`
* Object.values() - функция, которая возвращает все значения собственных свойств объекта, исключая любые значения в цепочке прототипов
* Object.entries() - метод, который возвращает ключи в виде массива в формате `[key, value]`
* дополнение строк до заданной длины: `String.prototype.padStart()` / `String.prototype.padEnd()`
* и др.

---

# ES9 / ES2018

* разделяемая память и атомарные операции
* `Promise.prototype.finally()`
* for-await-of для создания циклов, работающих с асинхронным кодом
* устранение некоторых ограничений тегированных шаблонных строк
* некоторые новые возможности работы с регулярными выражениями
* и др.

---

# ES.Next
Динамический указатель на последнюю, еще находящуюся в разработке версию ECMAScript

---

# Как смотреть, что уже поддерживается и какими браузерами, а что ещё нет?

* https://caniuse.com:

![](https://i.imgur.com/LpURs0q.png)

* https://developer.mozilla.org

---

# На какой версии языка писать?

**ES6+**
Возможности ES6 поддерживаются последними версиями практически всех браузеров (при необходимости использовать Babel). 
Поддержка браузерами определенных возможностей: https://kangax.github.io/compat-table/es6/

![](https://i.imgur.com/YcnbC1L.png)


---

# ES5: var, ES6: let, const
### Каким образом можно объявить переменную?
В стандарте ES5 переменную можно было объявить только одним способом
```javascript
var a = 10;
```
В стандарте ES6 объявить переменные можно как const или let
```javascript
const a = 10;
let a = 10;
```
---

# Чем отличаются const от let?
**Варианты ответа:**
1. функция не может быть объявлена как const
2. const в отличие от let создает неизменяемую переменную
3. имеют разные области видимости
4. переменные, объявленные как const, обязательно должны иметь быть названы верхнем регистре

---
# const

Const используют для объявления «констант», которые не будут в дальнейшем изменяться:
```javascript
const numberOfDays = 31;
// Uncaught TypeError: Assignment to constant variable
numberOfDays = 28;
```
Переопределение объекта запрещено:

```javascript=
const numberOfDaysInMonths = {
  November: 30,
  December: 31,
};

// Uncaught TypeError: Assignment to constant variable
numberOfDaysInMonths = {
  November: 30,
};
```
Но можем изменить какое-то свойство или добавить новое:
```javascript
numberOfDaysInMonths.January = 31;
console.log(numberOfDaysInMonths.January); // 31
```

---
# const с массивами
```javascript
const numberOfDaysInMonths = [
  31, 28, 31, 30, 31, 30,
  31, 31, 30, 31, 30, 31,
];
// Uncaught TypeError: Assignment to constant variable
numberOfDaysInMonths = [31, 28, 31];
```

### Что будет выведено в стр. 3?:
```javascript
const numbersArray = [1, 2, 3, 4, 5];
numbersArray[0] = 10;
console.log(numbersArray);
```

---

# Отличия var от let/const
#### Область видимости
* Переменная, объявленная как var, доступна в функции, в которой объявлена 
* Переменная, объявленная как let, доступна только в рамках блока {...}, в котором объявлена. В качестве блока могут выступать: функции, `if`, `while` или `for` и др.

### Что будет выведено (стр. 5, 7)? 
```javascript=
var isExamPassed = false;
var isGoodStudent = true;
if (isGoodStudent) {
  var isExamPassed = true;
  console.log(isExamPassed); // ?
}
console.log(isExamPassed); // ?
```

---

# Что будет выведено в этом случае? 
```javascript=
let isExamPassed = false;
let isGoodStudent = true;
if (isGoodStudent) {
  let isExamPassed = true;
  console.log(isExamPassed); // ?
}
console.log(isExamPassed); // ?
```
---

# let в цикле
Для каждой итерации создаётся своя переменная. Сравним:
```javascript
// выведет цифры от 0 до 9
for (let i = 0; i < 10; i++){
  setTimeout(() => console.log(i), 1000)
}

// выведет 10 раз цифру 10
for (var i = 0; i < 10; i++){
  setTimeout(() => console.log(i), 1000)
}
```

---

# Cинтаксис функций ES5 / ES6
В ES5 функцию можно объявить следующим образом:
```javascript=
// объявление функции (Function Declaration)
function multiply(a, b) {
  return a * b;
}
// функциональное выражение (Function Expression)
var multiply = function(a, b) {
    return a * b;
}
```
#### В ES6 появляются стрелочные функции:
```javascript
// примерный аналог объявления функции  выше
const multiply = (a, b) => {
    return a * b;
};

// аналог предыдущей функции,
// но return опущен (т.к. подразумевается неявно):
const multiply = (a, b) => a * b;
// можно добавить скобки для читабельности: (a * b)
```

Стрелочные функции позволяют использовать более короткий синтаксис при объявлении и кроме того, решают проблему [`потерянного this`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Functions/Arrow_functions#Отсутствие_связывания_с_this).

---

# ES6: значения параметров по умолчанию
```javascript=
const getTitle = (title = 'Безымянный') => { // ES6
  // …
  console.log(title);
};

var getTitle = (title) { // ES5
  title = title || 'Безымянный';
  console.log(title);
};
```

---
# ES6: деструктуризация в параметрах
Пользователь кликает на какой-то элемент и функции-обработчику событий onClick приходит объект event:
```javascript=
/*
event = {
  target: {...},
  type: '...',
  ...
}
*/
const onClick = ({ target, type }) => console.log(target, type);

var onClick2 = function(event) { // ES5
 console.log(event.target, event.type);
}
```
---

# ES6: получение массива аргументов при помощи оператора spread (...rest)
```javascript
const multiply = (multiplier, ...args) => args.map(
  element => multiplier * element,
);
console.log(multiply(2, 1, 2, 3)); // [2, 4, 6]
```

ES5: arguments

---
# Отличие стрелочных функций от классических

Стрелочные функции не имеют своего this и arguments (получают из окружающего контекста)
```javascript=
const group = {
  groupNumber: 1,
  students: ['Иванов', 'Петров', 'Сидоров'],
  showList() {
    this.students.forEach(student =>
      console.log(
        'Группа: ' + this.groupNumber +
        ', ' + student
      )
    );
  }
}
```
---

# ES6: перебор итерируемых объектов с помощью for ... of

 ES6 добавлены "итерируемые" (iterable), чье содержимое можно перебрать в цикле (массивы, строки, Map, Set, DOM-коллекции...)
```javascript=
let numbersAr = [10, 20, 30];

const double = () => { //ES6: выведет построчно 20, 40, 60
  for (let value of numbersAr) {
    console.log(value * 2);
  }
};

for (let char of 'лекция') {
  console.log(char.toUpperCase()); // выведет Л, Е, К, Ц, И, Я
}
```
```javascript=
var double = function() { // ES5: только для массивов
  numbersAr.forEach(function(value){ // выведет то же самое
    console.log(value); 
  });
};

var double2 = function() { // ES5, выведет то же самое
  for (var i = 0; i < numbersAr.length; i++) {
	console.log(numbersAr[i] * 2); 
  }
};
```

# ES6: тегированные шаблонные строки

Для начала вспомним что такое шаблонные строки (ES6):
```javascript=
const a = 5;
const b = 10; 
console.log('Сумма: ' + (a + b) + ', разность: ' + (a - b)); //ES5
console.log(`Сумма: ${a + b}, разность: ${a - b}`); //ES6
```
Помимо того, что это легче читается, уходит путаница с приведением типов с оператором "+".

**Задача**: по количеству баллов, которые студент получил за тест, вывести его оценку:
Студент [Фамилия] получил оценку [N] 
```javascript=
const formatMark = (strings, person, numberOfPoints) => {
  const student = strings[0]; // Студент 
  const points = strings[1]; // получил оценку
  let mark;
  if (numberOfPoints <= 60) {
    mark = '2';
  } else if (numberOfPoints > 61 && numberOfPoints <= 75) {
    mark = '3';
  } else if (numberOfPoints > 76 && numberOfPoints <= 85) {
    mark = '4';
  } else if (numberOfPoints > 86) {
    mark = '5';
  }
  return `${student}${person}${points}${mark}`;
}
const person = 'В. Пупкин';
const numberOfPoints = 85;
const output = formatMark`Студент ${person} получил оценку ${numberOfPoints}`;
console.log(output); // Студент В. Пупкин получил оценку 4
```
---

# Чему мы научились
- узнали зачем нужны стандарты JavaScript, основные изменения в версиях ES5-ES9, как узнать поддерживает ли браузер ту или иную новую возможность JavaScript и как использовать свежие возможности
- как объявить переменную при помощи var, let, const, и в чем разница
- повторили как объявлять функции в ES5 и стрелочные функции в ES6
- как осуществить перебор итерируемых объектов с помощью for ... of (ES6)
- как использовать тегированные шаблонные строки (ES6)

---

## Ссылки на дополнительные материалы
1. https://ru.wikipedia.org/wiki/Консорциум_Всемирной_паутины
2. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions
3. https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/template_strings
---

# Спасибо за внимание! Время задавать вопросы 🙂

---

