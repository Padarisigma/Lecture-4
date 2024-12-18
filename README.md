# JavaScript Lecture-4 
### Table of contents
*  Recursion 
*  Closure
  
### Recursion 
*Рекурсия в программировании похожа на
функцию, которая постоянно вызывает себя. Когда
функция делает это, она называется
рекурсивно определенной функцией.
Но есть правило, которому она должна следовать: она должна
иметь способ прекратить вызывать себя,
иначе она будет продолжаться вечно. Это правило остановки
называется базовым случаем.*
``` js 
function factorial(n) {
  // Базовый случай: факториал 0 и 1 равен 1
  if (n <= 1) {
    return 1;
  } else {
    // Рекурсивный шаг: n! = n * (n-1)!
    return n * factorial(n - 1);
  }
}

console.log(factorial(5)); // Выведет 120
console.log(factorial(0)); // Выведет 1
console.log(factorial(1)); // Выведет 1
```

*Рекурсивная функция function должна иметь условие, чтобы прекратить вызов самой себя. В противном случае функция
вызывается бесконечно.
Как только условие выполнено, функция прекращает вызов самой себя. Это называется базовым условием
Во-первых, вам нужно базовое условие num === 0.
Вам также нужен рекурсивный вызов
findFactorial(num - 1), чтобы гарантировать, что число
продолжает уменьшаться при каждом вызове, когда вы передаете
новый параметр n-1.
Затем вы умножаете результат на предыдущее
число num * findFactorial(num - 1), пока
не будет выполнено базовое условие.*
``` js 
let recursiyaNumber=(num)=>{
   if(num==1) return 1;
   if(num%2!=0){
   return num + recursiyaNumber(num-2)}
   else { 
    return recursiyaNumber(num-1)
   }
}
console.log(recursiyaNumber(5));
```

## *Closure*
Замыкание (closure) в JavaScript — это мощная концепция, которая часто вызывает затруднения у начинающих. Проще всего объяснить её так:

Замыкание — это функция, которая "помнит" окружающую её среду, даже после того, как эта среда уже перестала существовать.

Разберем это подробнее:

В JavaScript функции являются объектами первого класса. Это значит, что их можно передавать в другие функции как аргументы, возвращать из функций как значения, и присваивать переменным. И вот тут появляется интересная особенность: когда функция создается, она "запоминает" все переменные, доступные ей в момент создания, независимо от того, где и как она будет вызвана позже. Эти переменные образуют так называемое *лексическое окружение* функции.

``` js 
function outerFunction() {
  let outerVar = "Я — внешняя переменная";

  function innerFunction() {
    console.log(outerVar); // innerFunction имеет доступ к outerVar
  }

  return innerFunction;
}

let myClosure = outerFunction(); // myClosure теперь хранит innerFunction
myClosure(); // Выведет: "Я — внешняя переменная"
```
В этом примере:

1. `outerFunction` создает переменную `outerVar`.
2. `innerFunction` находится *внутри* `outerFunction` и имеет к ней доступ.
3. `outerFunction` возвращает `innerFunction`.
4. `myClosure` теперь хранит ссылку на `innerFunction`.
5. Даже после того, как `outerFunction` завершила свое выполнение (и `outerVar` вроде бы должна была быть удалена из памяти), `myClosure()` все еще может получить доступ к `outerVar`! Это и есть замыкание. `innerFunction` "закрыла" в себе доступ к `outerVar`.

Вот несколько примеров кода, демонстрирующих замыкания в JavaScript, с различными уровнями сложности:
1. Простой счётчик
``` js 
function createCounter() {
  let count = 0; // Переменная, доступная только внутри createCounter

  return function() {
    count++;
    return count;
  };
}

let counter1 = createCounter();
console.log(counter1()); // 1
console.log(counter1()); // 2
console.log(counter1()); // 3

let counter2 = createCounter();
console.log(counter2()); // 1 (независимый счётчик)
console.log(counter2()); // 2
```
`createCounter` создаёт замыкание. Внутренняя функция (анонимная функция, возвращаемая `createCounter`) имеет доступ к переменной `count`, даже после того, как `createCounter` завершила выполнение. Каждый вызов `createCounter` создает свой независимый счётчик.

2. Частные переменные 
``` js
function createPerson(name) {
  let age = 0; // Частная переменная

  return {
    getName: function() {
      return name;
    },
    getAge: function() {
      return age;
    },
    setAge: function(newAge) {
      age = newAge;
    }
  };
}

let person = createPerson("Иван");
console.log(person.getName()); // Иван
console.log(person.getAge()); // 0
person.setAge(30);
console.log(person.getAge()); // 30
// console.log(age); // Ошибка! age недоступна извне

```
`age` является частной переменной, доступной только через методы объекта, возвращаемого `createPerson`.



*Преимущества замыканий:*

* Позволяют создавать инкапсулированные данные и функции.
* Позволяют сохранять состояние между вызовами функции.
* Повышают модульность и читаемость кода.


*Недостатки замыканий:*

* Неправильное использование может привести к утечкам памяти (если замыкание хранит ссылки на большие объёмы данных).


## Связь Рекурсии и Замыканий

Рекурсия и замыкания — это две мощные концепции в JavaScript, которые могут использоваться вместе для решения сложных задач. Например, рекурсивная функция может использовать замыкания для сохранения состояния между своими вызовами.

# Спасибо за внимание !!!

