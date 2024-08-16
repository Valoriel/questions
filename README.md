# Вопросики

## JS Basic
### Какие типы данных бывают в JavaScript?
#### 1. Примитивные типы данных:  
- Числа (number) - например: 10, 3.14  
- Строки (string) - например: "Привет, мир!"  
- Булевы значения (boolean) - true или false  
- undefined - значение, которое присваивается переменной по умолчанию  
- null - значение, представляющее "ничего" или "пустоту"  
- Symbol - уникальные и неизменяемые значения, введенные в ECMAScript 6  
  
#### 2. Структурные типы данных:  
- Объекты (object) - коллекция ключей и значений  
- Массивы (array) - упорядоченная коллекция значений  
- Функции (function) - исполняемый блок кода  
  
#### 3. Специальные типы данных:  
- BigInt - используется для представления целых чисел произвольной длины  
- Символы (new in ECMAScript 6) - используются для создания уникальных идентификаторов
Тип данных Symbol был добавлен в стандарт ECMAScript 6 (или ES2015) и представляет собой уникальный и неизменяемый тип данных. Каждый символ, создаваемый в JavaScript, уникален, что означает, что два символа с одинаковым описанием не будут равны друг другу.  
  
Создать символ можно с помощью глобальной функции Symbol, просто вызвав её без ключевого слова new:  

```
let sym1 = Symbol();
let sym2 = Symbol('описание');
let sym3 = Symbol('описание'); // Еще один символ с таким же описанием, но он все равно уникален
```

  
Символы могут быть использованы в качестве идентификаторов свойств объектов:  

```
const MY_KEY = Symbol();
let obj = {};
obj[MY_KEY] = 123;
console.log(obj[MY_KEY]); // 123
```

  
Также они могут быть использованы в некоторых встроенных методах JavaScript для определения поведения объекта, например, в качестве специальных свойств итераторов.  
  
В целом, символы полезны для создания уникальных идентификаторов без возможности случайного пересечения с другими именами переменных, свойств объектов или другими структурами данных.

### В чём разница между var, let и const
#### 1. **var**:  
- Переменные, объявленные с помощью var, имеют функциональную область видимости, что означает, что они видны только в пределах функции, в которой были объявлены.  
- Переменные var подвержены поднятию (hoisting), что означает, что они могут быть доступны для использования ещё до того, как были объявлены.  
- Значение переменной var можно переопределить.  
Пример:  

```
var x = 10;
if (true) {
	var x = 20;
	console.log(x); // 20
}
console.log(x); // 20   
```

#### 2. **let**:  
- Переменные, объявленные с помощью let, имеют блочную область видимости, что означает, что они видны только внутри блока (например, внутри {}).  
- Переменные let не подвержены поднятию (hoisting), они становятся доступными только после объявления.  
- Значение переменной let можно переопределить.  
Пример:  

```
let x = 10;
if (true) {
	let x = 20;
	console.log(x); // 20 
}
console.log(x); // 10   
```

#### 3. **const**:  
- Переменные, объявленные с помощью const, также имеют блочную область видимости.  
- Переменные const должны быть инициализированы при объявлении, после чего их нельзя переопределить.  
Пример:  

```
const x = 10;
// x = 20; // Ошибка! Операция переопределения константы запрещена   
```
  
В целом, использование let и const рекомендуется вместо var, поскольку они помогают избежать некоторых проблем с областью видимости переменных, позволяют более безопасно управлять переменными и предотвращают нежелательные изменения значений.

### Что такое temporal dead zone?

Temporal Dead Zone (TDZ) - это интересная особенность переменных, объявленных с использованием let и const в JavaScript. Это период времени между началом области видимости переменной и фактическим моментом её объявления, когда обращение к переменной вызовет ReferenceError.  
  
Посмотрим на пример:  
  

```
console.log(x);  // ReferenceError: x is not definedlet x = 10;
```

  
В этом случае, обращение к переменной `x`, хотя она уже существует, вызывает ошибку. Это происходит из-за того, что переменная `x` находится в темпоральной зоне &mdash; временном промежутке между началом области видимости и фактическим моментом инициализации.  
  
Temporal Dead Zone (TDZ) предотвращает использование переменной до момента её объявления, что может помочь предотвратить ошибки и упрощает предсказуемость поведения программы.

### Чем стрелочные функции отличаются от обычных функций? 

> _Не заблуждайтесь, способы объявления функций в Javascript отличаются не только компактностью и элегантным синтаксисом._

Стрелочные функции — это относительно новая функция, реализованная в ES6 ( [ECMAScript 6](https://www.w3schools.com/js/js_es6.asp) ), которая, на наш взгляд, является просто более кратким и элегантным синтаксисом для объявления функциональных выражений в JavaScript. Хотя традиционные функции и функции стрелок работают схожим образом, мы должны остерегаться некоторых различий, которые могут быть незаметны.

#### Синтаксис

Разница в синтаксисе между двумя моделями общеизвестна, поскольку в стрелочной функции становится возможным значительно сократить количество строк, присутствующих в объявлении функции, особенно если это уже простая функция. См. примеры:

Представьте себе функцию, которая берет имя пользователя и выводит его в консоль. Традиционным способом мы могли бы объявить это так:

```
function sayMyNane(name){
  console.log(`My name is ${name}!`);
}

sayMyNane('Ernane'); // => My name is Ernane.
```

Со стрелочными функциями из ES6 мы могли бы сделать это следующим образом:

```
const sayMyName = (name) => {
  console.log(`My name is ${name}`);
};

sayMyName("Ernane"); // => My name is Ernane.
```

Помня, что в случае со стрелочными функциями фигурные скобки необходимы только в том случае, если присутствует выражение, то же правило применяется и к скобкам, поскольку они необходимы только в том случае, если необходимо передать более одного аргумента. Таким образом, мы могли бы уменьшить его еще больше и записать приведенный выше пример следующим образом:

```
const sayMyName = (name) => console.log(`My name is ${name}`);

sayMyName("Ernane"); // => My name is Ernane.
```

Просто, не так ли? Таким образом, мы можем увидеть, как стрелочная функция может облегчить объявление определенной функции из-за своего синтаксиса и при этом вернуть тот же результат, что и обычное объявление.

#### Использование ключевого слова «this»

В отличие от традиционного объявления, стрелочные функции не имеют собственного элемента [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this) , поскольку значение this внутри стрелочной функции остается неизменным на протяжении всего жизненного цикла функции и всегда привязано к значению this в ближайшей традиционной родительской функции.

Это стало немного странно? Позвольте мне попытаться упростить с примером:

Возвращаясь к примеру, использованному в предыдущем разделе, представьте, что у нас есть объект `person`, имя которого определено как один из его атрибутов, и функция, которая выводит имя этого конкретного человека в консоль. В зависимости от типа используемой функции она не сможет правильно получить доступ к родительскому объекту, имеющему запрошенный атрибут _имени_ , и, следовательно, ее возврат будет `undefined`.

```
let person = {
  name: "Ernane Ferreira",
  sayMyName: () => console.log(`My name is ${this.name}.`),
};

person.sayMyName(); // => My name is .
```

В случае объявления функции в традиционной модели это будет работать как положено и мы правильно получим искомый атрибут.

```
let person = {
  name: "Ernane Ferreira",
  sayMyName: function () {
    console.log(`My name is ${this.name}.`);
  },
};

person.sayMyName(); // => My name is Ernane Ferreira.
```

#### Доступ к аргументам

Объект [arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments) — это локальная переменная, доступная внутри всех функций, и это то, что делает ссылку возможными аргументами функции внутри нее, используя объект arguments. Однако стрелочные функции не имеют ссылки на `arguments`объект:

```
const showArguments = () => console.log(arguments);

showArguments(1, 2, 3) // => ReferenceError: arguments is not defined.
```

В случае обычной функции мы можем легко получить доступ к списку аргументов, переданных в качестве параметра при вызове функции:

```
function showArguments(){ 
  console.log(arguments); 
}

showArguments(1, 2, 3) // => Arguments(3) [1, 2, 3]
```

#### Использование оператора new

Оператор [new](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new) позволяет создавать экземпляры определяемого пользователем типа объекта или одного из определяемых пользователем типов. внутренних объектов, которые имеют **функцию конструктора** . Традиционные функции являются конструируемыми и могут быть вызваны с помощью оператора`new`. С другой стороны, _стрелочные функции_ являются вызываемыми, а не конструируемыми, то есть эти функции никогда не могут использоваться в качестве функций-конструкторов и никогда не могут вызываться с помощью оператора `new`.

Поэтому для такого типа выполнения в традиционных функциях мы получаем следующий результат выполнения:

```
function sayMyName(name) {
  console.log(`My name is ${name}`);
}

new sayMyName("Ernane"); // => Ernane
```

Что касается _стрелочных функций_ :

```
const sayMyName = (name) => console.log(`My name is ${name}`);

new sayMyName("Ernane"); // => Uncaught TypeError: sayMyName is not a constructor
```

#### Параметры с дублирующимся именем

Стрелочные _функции_ не допускают дублирования имен параметров, но традиционные функции допускают зависимость от применения или неприменения строгого режима ( [Strict Mode](https://developer.mozilla.org/en-US/docs/Web%20/JavaScript/Reference/Strict_mode) ) в реализации кода. Например, приведенный ниже JavaScript полностью действителен:

```
function addTwoNumbers(x, x){
  console.log(x+x);
}

addTwoNumbers(1,1); // => 2
```

Однако тот же код с примененным строгим режимом больше недействителен:

```
"use strict";

function addTwoNumbers(x, x) {
  console.log(x + x);
}

// => Uncaught SyntaxError: Duplicate parameter name not allowed in this context
```

При использовании стрелочных функций это происходит независимо от того, применяется ли строгий режим. В обоих случаях выполнение недействительно:

```
const addTwoNumbers = (x, x) => console.log(x+x); 

// => SyntaxError: Uncaught SyntaxError: Duplicate parameter name not allowed in this context.
```

### Как работает boxing/unboxing в JavaScript?

### В чем разница между композицией и наследованием?

### Что такое распространение события (Event Propagation)?

### Что такое деструктуризация?

### Работа с асинхронным кодом


## JS Advanced
### Почему typeof null возвращает object?

Это баг, и лично Брэндан Айк это [признает](http://wiki.ecmascript.org/doku.php?id=harmony:typeof_null). Этот баг, вероятно, никогда не будет исправлен из-за необходимости сохранения обратной совместимости существующего кода с новыми версиями языка.  
  
Интересна история того, как же это получилось. Она восходит корнями к первой версии языка, а именно — к тому факту, что значения переменных хранились в 32-битных ячейках в следующем формате:  
29-31 бит: само значение;  
1-3 бита: метка типа данных;  
  
Было всего пять вариантов метки типа:  
000: object;  
1: integer;  
010: double;  
100: string;  
110: boolean;  
  
Соответственно, если младший бит был равен единице, то оставшийся 31 бит интерпретировался как integer. Если 0 — то тип определялся в зависимости от значения следующих двух бит.  
  
Также было два специальных зарезервированных значения:  
  
undefined (JSVAL_VOID) — целое –230  
null (JSVAL_NULL) — указатель на NULL (machine code NULL pointer), то есть, метка объекта и ссылка на то, что его численное представление равно нулю.  
  
Так и вышло, что typeof стал определять null как object — он проверял метку типа, которая сообщала ему, что null — это не что иное, как object.

### Что такое записи (records) и кортежи (tuples)? 

### Основные принципы работы «сборщика мусора» в JS.

### Расскажите о генераторах и итераторах.

### Расскажите про Debounce/ throtling

### За счет чего возможно замыкание в JS?

### Точные вычисления в JS

### Какие способы привязки контекста ты знаешь?

### Расскажите о шаблоне проектирования «Открытый модуль»

### В чём разница между объектами Map и WeakMap?

### Как передаются параметры в функцию: по ссылке или по значению?

### function foo() { let a = b = 0; } Что выведет typeof a и typeof b вне функции


## Typescript
### Какие проблемы помогает решить типизация?

### Как в TypeScript проверять значения на равенство null и undefined?

### Отличия типа от интерфейса

### Отличия extends от implements

### Что такое generics?

### Какие есть utility types? (omit, partial, required etc..)

### Можно ли в TypeScript использовать строго типизированные функции в качестве параметров?

### Поддерживает ли TypeScript перегрузку функций?

### Чем различаются ключевые слова interface и type в TypeScript?

## React

### Что такое React?

Библиотека для разработки интерфейсов
### Какую проблему решает реакт?

Упрощение процесса создания больших приложений.
### Что такое Virtual DOM?
Виртуальный DOM (VDOM) — это концепция программирования, в которой идеальное или «виртуальное» представление пользовательского интерфейса хранится в памяти и синхронизируется с «настоящим» DOM при помощи библиотеки, такой как ReactDOM. Этот процесс называется [согласованием](https://ru.legacy.reactjs.org/docs/reconciliation.html).

Такой подход и делает API React декларативным: вы указываете, в каком состоянии должен находиться пользовательский интерфейс, а React добивается, чтобы DOM соответствовал этому состоянию. Это абстрагирует манипуляции с атрибутами, обработку событий и ручное обновление DOM, которые в противном случае пришлось бы использовать при разработке приложения.

Поскольку «виртуальный DOM» — ==это скорее паттерн==, чем конкретная технология, этим термином иногда обозначают разные понятия. В мире React «виртуальный DOM» обычно ассоциируется с [React-элементами](https://ru.legacy.reactjs.org/docs/rendering-elements.html) , поскольку они являются объектами, представляющими пользовательский интерфейс. ==Тем не менее, React также использует внутренние объекты, называемые «волокнами» (fibers)==, чтобы хранить дополнительную информацию о дереве компонентов. Их также можно считать частью реализации «виртуального DOM» в React.

### Для чего нужно свойство key во время рендеринга списков?

key нужен для итерации списков. У меня возникали проблемы с рендером списков, выдавало ошибку, мол, список неитерируемый. Я так понимаю, под капотом реакт с помощью key оптимизирует алгоритм отрисовки до O(N)

### Что такое Reconciliation?

**Сверка** (Reconciliation) — это алгоритм React, используемый для того, чтобы отличить одно дерево элементов от другого для определения частей, которые нужно будет заменить.

**Апдейт** — это изменение в данных, которые используются для отрисовки React приложения. Обычно это результат вызова метода setState; конечный результат отрисовки компонента.

Сверка — это алгоритм, за которым стоит то, что мы привыкли называть «Virtual DOM». Определение звучит как-то так: когда вы рендерите React приложение, дерево елементов, которое описывает приложение генерируется в зарезервированной памяти. Это дерево потом включается в рендеринг окружение — на примере браузерного приложения, оно переводится в набор DOM операций. Когда состояние приложения обновляется (обычно вызовом setState), новое дерево генерируется. Новое дерево сравнивается с предыдущим, чтоб просчитать и включить именно те операции, которые нужны для перерисовки обновленного приложения.

==ПРОСТЫМИ СЛОВАМИ: В реакте в памяти генерится дом, а при обновлении стейта, генерится в памяти новый дом, потом сравнивается с предыдущим и дифы заменяются, а не целиком ререндерится новый дом==
  
Несмотря на то что Fiber это близкая реализация сверщика, высокоуровненый алгоритм, обьясненный в React документации будет в большинстве таким же.

Причина почему React поддерживает так много целей в том что React построен так, что сверка и рендеринг это отдельные фазы. Сверщик, работая, вычисляет какие части дерева изменились, отрисовщик позже использует эту информацию чтобы обновить ранее отрисованное дерево.

В текущей реализации React проходит дерево рекурсивно и вызвает функции рендеринга на всем обновленном дереве в ходе одного тика (16 мс). Однако в будующем он сможет уметь отменять некоторые апдейты чтобы предотвратить скачки фреймов.  
Это частообсуждаемая тема касательно React дизайна. Некоторые популярные библиотеки реализуют проталкивающий ("push") подход, где вычисления производятся тогда, когда новые данные доступны. Однако, React придерживается подхода протягивания ("pull"), где вычисления могут быть отменены когда это необходимо.  
Реакт это библиотека не для обработки обобщенных данных. Это библиотека для построения пользовательских интерфейсов. Мы думаем что у него должна быть уникальная позиция в приложении, чтоб определять какие вычисления являются подходящими, а какие нет в данный момент.

Можно ли рендерить компонент по условию?

Условный рендеринг в React работает так же, как условные выражения работают в JavaScript. Бывает нужно объяснить React, как состояние влияет на то, какие компоненты требуется скрыть, а какие — отрендерить, и как именно. В таких ситуациях используйте [условный оператор](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Operators/%D0%A3%D1%81%D0%BB%D0%BE%D0%B2%D0%BD%D1%8B%D0%B9_%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80) JavaScript или выражения подобные [`if`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Statements/if...else).

Пример:
```
function UserGreeting(props) {
  return <h1>С возвращением!</h1>
}

function GuestGreeting(props) {
  return <h1>Войдите, пожалуйста.</h1>
}
```
```
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn
  if (isLoggedIn) {
    return <UserGreeting />
  }
  return <GuestGreeting />
}

ReactDOM.render(
  // Попробуйте заменить на isLoggedIn={true} и посмотрите на эффект.
  <Greeting isLoggedIn={false} />,
  document.getElementById('root')
)
```

Переменные-элементы

Элементы React можно сохранять в переменных. Это может быть удобно, когда какое-то условие определяет, надо ли рендерить одну часть компонента или нет, а другая часть компонента остаётся неизменной.

Рассмотрим ещё два компонента, представляющих кнопки Войти (Login) и Выйти (Logout).

```
function LoginButton(props) {
  return <button onClick={props.onClick}>Войти</button>
}

function LogoutButton(props) {
  return <button onClick={props.onClick}>Выйти</button>
}
```

В следующем примере мы создадим [компонент с состоянием](https://reactdev.ru/archive/react16/state-and-lifecycle/#adding-local-state-to-a-class) и назовём его `LoginControl`.

Он будет рендерить либо `<LoginButton />`, либо `<LogoutButton />` в зависимости от текущего состояния. А ещё он будет всегда рендерить `<Greeting />` из предыдущего примера.

```
class LoginControl extends React.Component {
  constructor(props) {
    super(props)
    this.handleLoginClick = this.handleLoginClick.bind(this)
    this.handleLogoutClick = this.handleLogoutClick.bind(
      this
    )
    this.state = { isLoggedIn: false }
  }

  handleLoginClick() {
    this.setState({ isLoggedIn: true })
  }

  handleLogoutClick() {
    this.setState({ isLoggedIn: false })
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn
    let button

    if (isLoggedIn) {
      button = (
        <LogoutButton onClick={this.handleLogoutClick} />
      )
    } else {
      button = (
        <LoginButton onClick={this.handleLoginClick} />
      )
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    )
  }
}

ReactDOM.render(
  <LoginControl />,
  document.getElementById('root')
)
```

Нет ничего плохого в том, чтобы объявить переменную и условно рендерить компонент `if`-выражением. Но иногда хочется синтаксис покороче. Давайте посмотрим на несколько других способов писать условия прямо в JSX.

Встроенные условия if с логическим оператором &&

Вы можете [внедрить любое выражение в JSX](https://reactdev.ru/archive/react16/introducing-jsx/#embedding-expressions-in-jsx), заключив его в фигурные скобки. Это правило распространяется и на логический оператор `&&` языка JavaScript, которым можно удобно вставить элемент в зависимости от условия:

```
function Mailbox(props) {
  const unreadMessages = props.unreadMessages
  return (
    <div>
      <h1>Здравствуйте!</h1>
      {unreadMessages.length > 0 && (
        <h2>
          У вас {unreadMessages.length} непрочитанных
          сообщений.
        </h2>
      )}
    </div>
  )
}

const messages = ['React', 'Re: React', 'Re:Re: React']
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
)
```

Приведённый выше вариант работает корректно, потому что в JavaScript выражение `true && expression` всегда вычисляется как `expression`, а выражение `false && expression` — как `false`.

То есть, если условие истинно (`true`), то элемент, идущий непосредственно за `&&`, будет передан на вывод. Если же оно ложно (`false`), то React проигнорирует и пропустит его.

Встроенные условия if-else с тернарным оператором

Есть ещё один способ писать условия прямо в JSX. Вы можете воспользоваться тернарным оператором [`condition ? true : false`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Operators/%D0%A3%D1%81%D0%BB%D0%BE%D0%B2%D0%BD%D1%8B%D0%B9_%D0%BE%D0%BF%D0%B5%D1%80%D0%B0%D1%82%D0%BE%D1%80).

Вот как этот метод можно использовать, чтобы отрендерить кусочек текста.

```
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      Пользователь <b>{isLoggedIn ? 'сейчас' : 'не'}</b> на сайте.
    </div>
  );
}
```

Этот метод можно использовать и с выражениями покрупнее, но это может сделать код менее очевидным:

```
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn ? (
        <LogoutButton onClick={this.handleLogoutClick} />
      ) : (
        <LoginButton onClick={this.handleLoginClick} />
      )}
    </div>
  );
}
```

Как в JavaScript, так и в React выбор синтаксиса зависит от ваших предпочтений и принятого в команде стиля. Не забывайте, что если какое-то условие выглядит очень сложным, возможно пришло время [извлечь часть кода в отдельный компонент](https://reactdev.ru/archive/react16/components-and-props/#extracting-components).

Предотвращение рендеринга компонента

В редких случаях может потребоваться позволить компоненту спрятать себя, хотя он уже и отрендерен другим компонентом. Чтобы этого добиться, верните `null` вместо того, что обычно возвращается на рендеринг.

Например, будет ли содержимое `<WarningBanner />` отрендерено, зависит от значения пропа под именем `warn`. Если значение `false`, компонент ничего не рендерит:

```
function WarningBanner(props) {
  if (!props.warn) {
    return null
  }

  return <div className="warning">Предупреждение!</div>
}

class Page extends React.Component {
  constructor(props) {
    super(props)
    this.state = { showWarning: true }
    this.handleToggleClick = this.handleToggleClick.bind(
      this
    )
  }

  handleToggleClick() {
    this.setState((state) => ({
      showWarning: !state.showWarning,
    }))
  }

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.handleToggleClick}>
          {this.state.showWarning ? 'Спрятать' : 'Показать'}
        </button>
      </div>
    )
  }
}

ReactDOM.render(<Page />, document.getElementById('root'))
```

Сам факт возврата `null` из метода `render` компонента никак не влияет на срабатывание методов жизненного цикла компонента. Например, `componentDidUpdate` будет всё равно вызван.
### Что такое контролируемые компоненты?

### Делегирование событий в React?

### Что вы знаете о React refs?

### В проекте котором ты работал, в каком стиле писался код? Классовые компоненты? Хуки?

### Какие знаешь хуки?

https://my-js.org/docs/cheatsheet/react-hooks/

> Хуки позволяют функциональным компонентам `React` иметь состояние (state) и методы жизненного цикла (lifecycle methods) подобно классовым компонентам. Появление хуков привело к тому в настоящее время классовые компоненты в `React` почти не используются.

#### useState

Хук `useState()` предназначен для управления состоянием компонента. Данная функция возвращает пару геттер/сеттер - значение начального состояния и функцию для обновления этого значения. Функцию имеет следующую сигнатуру: `const [value, setValue] = useState(defaultValue)`.

##### Обновление одного состояния

```
const UpdateState = () => {
  const [age, setAge] = useState(19)

  const handleClick = () => setAge(age + 1)

  return (
    <>
      <p>Мне {age} лет.</p>
      <button onClick={handleClick}>Стать старше!</button>
    </>
  )
}
```

##### Обновление нескольких состояний

```
const MultipleStates = () => {
  const [age, setAge] = useState(19)
  const [num, setNum] = useState(1)

  const handleAge = () => setAge(age + 1)
  const handleNum = () => setNum(num + 1)

  return (
    <>
      <p>Мне {age} лет.</p>
      <p>У меня {num} братьев и сестер.</p>
      <button onClick={handleAge}>Стать старше!</button>
      <button onClick={handleNum}>Больше братьев и сестер!</button>
    </>
  )
}
```

##### Обновление объекта состояния

```
const StateObject = () => {
  const [state, setState] = useState({ age: 19, num: 1 })

  const handleClick = (val) =>
    setState({
      ...state,
      [val]: state[val] + 1
    })

  const { age, num } = state
  return (
    <>
      <p>Мне {age} лет.</p>
      <p>У меня {num} братьев и сестер.</p>
      <button onClick={() => handleClick('age')}>Стать старше!</button>
      <button onClick={() => handleClick('num')}>
        Больше братьев и сестер!
      </button>
    </>
  )
}
```

##### Счетчик

```
const CounterState = () => {
  const [count, setCount] = useState(0)

  return (
    <>
      <p>Значение счетчика: {count}.</p>
      <button onClick={() => setCount(0)}>Сбросить</button>
      <button onClick={() => setCount((prevVal) => prevVal + 1)}>
        Увеличить (+)
      </button>
      <button onClick={() => setCount((prevVal) => prevVal - 1)}>
        Уменьшить (-)
      </button>
    </>
  )
}
```

##### Более сложный пример

```
const Profile = () => {
  const [profile, setProfile] = useState({
    firstName: 'Иван',
    lastName: 'Петров'
  })

  const handleChange = ({ target: { value, name } }) => {
    setProfile({ ...profile, [name]: value })
  }

  const { firstName, lastName } = profile
  return (
    <>
      <h1>Профиль</h1>
      <form>
        <input
          type='text'
          value={firstName}
          onChange={handleChange}
          name='firstName'
        /> <br />
        <input
          type='text'
          value={lastName}
          onChange={handleChange}
          name='lastName'
        />
      </form>
      <p>
        Имя: {firstName} <br />
        Фамилия: {lastName}
      </p>
    </>
  )
}
```

#### useEffect

Хук `useEffect()` предназначен для запуска побочных эффектов (например, выполнение сетевого запроса или добавление обработчика событий) ==после монтирования и отрисовки компонента==. Данная функция принимает колбек и массив зависимостей. Что касается массива зависимостей, то логика следующая: ^b9ea0b

- массив не указан: эффект запускается при каждом рендеринге
- указан пустой массив: эффект запускается только один раз
- указан массив с элементами: эффект запускается при изменении любого элемента

Очистка эффектов производится посредством возвращения значений из хука.

Функция имеет следующую сигнатуру:

```
// обработчик
const handler = () => {
  console.log('Случился клик!')
}

useEffect(() => {
  // запуск эффекта
  window.addEventListener('click', handler)

  // очистка эффекта
  return () => {
    window.removeEventListener('click', handler)
  }
  // массив зависимостей
}, [handler])
```

##### Базовый пример

```
const BasicEffect = () => {
  const [age, setAge] = useState(19)

  const handleClick = () => setAge(age + 1)

  useEffect(() => {
    document.title = `Тебе ${age} лет!`
  })

  return (
    <>
      <p>Обратите внимание на заголовок текущей вкладки браузера.</p>
      <button onClick={handleClick}>Обновить заголовок!</button>
    </>
  )
}
```

##### Очистка эффекта

```
const CleanupEffect = () => {
  useEffect(() => {
    const clicked = () => console.log('Клик!')

    window.addEventListener('click', clicked)

    return () => {
      window.removeEventListener('click', clicked)
    }
  }, [])

  return (
    <>
      <p>После клика по области просмотра в консоли появится сообщение.</p>
    </>
  )
}
```

##### Несколько эффектов

```
const MultipleEffects = () => {
  useEffect(() => {
    const clicked = () => console.log('Клик!')

    window.addEventListener('click', clicked)

    return () => {
      window.removeEventListener('click', clicked)
    }
  }, [])

  useEffect(() => {
    console.log('Второй эффект.')
  })

  return (
    <>
      <p>Загляните в консоль.</p>
    </>
  )
}
```

##### Массив зависимостей

```
const DependencyEffect = () => {
  const [randomInt, setRandomInt] = useState(0)
  const [effectLogs, setEffectLogs] = useState([])
  const [count, setCount] = useState(1)

  useEffect(() => {
    setEffectLogs((prev) => [
      ...prev,
      `Вызов функции номер ${count}.`
    ])

    setCount(count + 1)
  }, [randomInt])

  return (
    <>
      <h3>{randomInt}</h3>
      <button onClick={() => setRandomInt(~~(Math.random() * 10))}>
        Получить случайное целое число!
      </button>
      <ul>
        {effectLogs.map((effect, i) => (
          <li key={i}>{' 😈 '.repeat(i) + effect}</li>
        ))}
      </ul>
    </>
  )
}
```

##### Пропуск эффекта

```
const SkipEffect = () => {
  const [randomInt, setRandomInt] = useState(0)
  const [effectLogs, setEffectLogs] = useState([])
  const [count, setCount] = useState(1)

  useEffect(() => {
    setEffectLogs((prev) => [
      ...prev,
      `Вызов функции номер ${count}.`
    ])

    setCount(count + 1)
  }, [])

  return (
    <>
      <h3>{randomInt}</h3>
      <button onClick={() => setRandomInt(~~(Math.random() * 10))}>
        Получить случайное целое число!
      </button>
      <ul>
        {effectLogs.map((effect, i) => (
          <li key={i}>{' 😈 '.repeat(i) + effect}</li>
        ))}
      </ul>
    </>
  )
}
```

##### Более сложный пример

```
const UserList = () => {
  const [users, setUsers] = useState([])
  const [count, setCount] = useState(1)
  const [url, setUrl] = useState(
    `https://jsonplaceholder.typicode.com/users?_limit=${count}`
  )

  useEffect(() => {
    async function fetchUsers() {
      const response = await fetch(url)
      const users = await response.json()
      setUsers(users)
    }
    fetchUsers()
  }, [url])

  const handleSubmit = (e) => {
    e.preventDefault()
    setUrl(`https://jsonplaceholder.typicode.com/users?_limit=${count}`)
  }

  return (
    <>
      <h1>Пользователи</h1>
      <form onSubmit={handleSubmit}>
        <label>
          Сколько пользователей вы хотите получить?
          <input
            type='number'
            value={count}
            onChange={(e) => {
              setCount(e.target.value)
            }}
          />
          <button>Получить</button>
        </label>
      </form>
      <ul>
        {users.map(({ id, name, username, email, address: { city } }) => (
          <li key={id}>
            <span>
              <b>Имя:</b> {name}
            </span>
            <br />
            <span>
              <i>Имя пользователя:</i> {username}
            </span>
            <br />
            <span>
              <b>Адрес электронной почты:</b> {email}
            </span>
            <br />
            <span>
              <i>Город:</i> {city}
            </span>
            <br />
          </li>
        ))}
      </ul>
    </>
  )
}
```

#### useLayoutEffect

Хук `useLayoutEffect()` похож на хук `useEffect()`, за исключением того, что он запускает эффект перед отрисовкой компонента. Данный хук предназначен для запуска эффектов, влияющих на внешний вид DOM, незаметно для пользователя. Эта функция имеет такую же сигнатуру, что и `useEffect()`. В подавляющем большинстве случаев для запуска побочных эффектов используется `useEffect()`.

##### Базовый пример

```
const LayoutEffect = () => {
  const [randomInt, setRandomInt] = useState(0)
  const [effectLogs, setEffectLogs] = useState([])
  const [count, setCount] = useState(1)

  useLayoutEffect(() => {
    setEffectLogs((prev) => [...prev, `Вызов функции номер ${count}.`])

    setCount(count + 1)
  }, [randomInt])

  return (
    <>
      <h3>{randomInt}</h3>
      <button onClick={() => setRandomInt(~~(Math.random() * 10))}>
        Получить случайное целое число!
      </button>
      <ul>
        {effectLogs.map((effect, i) => (
          <li key={i}>{' 😈 '.repeat(i) + effect}</li>
        ))}
      </ul>
    </>
  )
}
```

#### useContext

Хук `useContext()` предназначен для прямой передачи пропов компонентам, находящимся на любом уровне вложенности. Он позволяет избежать так называемого "бурения пропов" (prop drilling), т.е. необходимости последовательной передачи пропов на каждом уровне вложенности.

Создание контекста:

```
import { createContext } from 'react'

export const ContextName = createContext()
```

Передача значения контекста нижележащим компонентам:

```
<ContextName.Provider value={initialValue}>
  <App />
</ContextName.Provider>
```

Получение значения контекста:

```
import { useContext } from 'react'
import { ContextName } from './ContextName'

const contextValue = useContext(ContextName)
```

##### Базовый пример

```
const ChangeTheme = () => {
  const [mode, setMode] = useState('light')

  const handleClick = () => {
    setMode(mode === 'light' ? 'dark' : 'light')
  }

  const ThemeContext = createContext(mode)

  const theme = useContext(ThemeContext)

  return (
    <div
      style={{
        background: theme === 'light' ? '#eee' : '#222',
        color: theme === 'light' ? '#222' : '#eee',
        display: 'grid',
        placeItems: 'center',
        minWidth: '320px',
        minHeight: '320px',
        borderRadius: '4px'
      }}
    >
      <p>Выбранная тема: {theme}.</p>
      <button onClick={handleClick}>Поменять тему оформления</button>
    </div>
  )
}
```

##### Более сложный пример

```
// TodoContext.js
import { createContext, useState } from 'react'

export const TodoContext = createContext()

export const TodoProvider = ({ children }) => {
  const [todos, setTodos] = useState([])

  return (
    <TodoContext.Provider value={[todos, setTodos]}>
      {children}
    </TodoContext.Provider>
  )
}
```

```
// index.js
import React, { StrictMode, render } from 'react'

import { Form } from './Form'
import { List } from './List'

import { TodoProvider } from './TodoContext'

const root = document.getElementById('root')
render(
  <StrictMode>
    <TodoProvider>
      <Form />
      <List />
    </TodoProvider>
  </StrictMode>,
  root
)
```

```
// Form.js
import { useState, useContext } from 'react'
import { TodoContext } from './TodoContext'

export const Form = () => {
  // локальное состояние
  const [text, setText] = useState('')
  // глобальное состояние
  const [todos, setTodos] = useContext(TodoContext)

  const handleChange = ({ target: { value } }) => {
    setText(value)
  }

  const handleSubmit = (e) => {
    e.preventDefault()

    const newTodo = {
      id: Date.now(),
      text
    }

    setTodos([...todos, newTodo])

    setText('')
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Текст задачи: <br />
        <input
          type='text'
          value={text}
          onChange={handleChange}
        /> <br />
        <button>Добавить</button>
      </label>
    </form>
  )
}
```

```
// List.js
import { useContext } from 'react'
import { TodoContext } from './TodoContext'

export const List = () => {
  // глобальное состояние
  const [todos] = useContext(TodoContext)

  return (
    <ul>
      {todos.map(({ id, text }) => <li key={id}>{text}</li>)}
    </ul>
  )
}
```

#### useReducer

Хук `useReducer()`, как и хук `useState()`, предназначен для управления состоянием. Он используется при наличии сложной логики управления состоянием или когда следующее состояние зависит от предыдущего. `useReducer()` принимает редуктор (_reducer_), обновляющий состояние на основе типа (_type_) и, опционально, полезной нагрузки (_payload_) переданной операции (_action_).

Сигнатура редуктора:

```
const reducer = (state, action) => {
  switch(action.type) {
    case 'actionType':
      return newState // { value: state.value + action.payload }
    default:
      return state
  }
}
```

Использование хука:

```
const [state, dispatch] = useReducer(reducer, initialState, initFn)
// dispatch({ type: 'actionType', payload: 'actionPayload' }) используется для отправки операции в редуктор (для обновления состояния)
// initFn - функция для "ленивой" установки начального состояния
```

##### Базовый пример

```
// начальное состояние
const initialState = { width: 30 }

// редуктор
const reducer = (state, action) => {
  switch (action) {
    case 'plus':
      return { width: Math.min(state.width + 30, 600) }
    case 'minus':
      return { width: Math.max(state.width - 30, 30) }
    default:
      throw new Error('Что происходит?')
  }
}

const BasicReducer = () => {
  const [state, dispatch] = useReducer(reducer, initialState)

  const [color, setColor] = useState('#f0f0f0')

  useEffect(() => {
    const randomColor = `#${((Math.random() * 0xfff) << 0).toString(16)}`
    setColor(randomColor)
  }, [state])

  return (
    <>
      <div
        style={{
          margin: '0 auto',
          background: color,
          height: '100px',
          width: state.width
        }}
      ></div>
      <button onClick={() => dispatch('plus')}>
        Увеличить ширину контейнера.
      </button>
      <button onClick={() => dispatch('minus')}>
        Уменьшить ширину контейнера.
      </button>
    </>
  )
}
```

##### Отложенная установка начального состояния

```
const initializeState = () => ({
  width: 90
})

// обратите внимание как `initializeState()` перезаписывает начальное значение
const initialState = { width: 0 }

const reducer = (state, action) => {
  switch (action) {
    case 'plus':
      return { width: Math.min(state.width + 30, 600) }
    case 'minus':
      return { width: Math.max(state.width - 30, 30) }
    default:
      throw new Error('Что происходит?')
  }
}

const LazyState = () => {
  const [state, dispatch] = useReducer(reducer, initialState, initializeState)

  const [color, setColor] = useState('#f0f0f0')

  useEffect(() => {
    const randomColor = `#${((Math.random() * 0xfff) << 0).toString(16)}`
    setColor(randomColor)
  }, [state])

  return (
    <>
      <div
        style={{
          margin: '0 auto',
          background: color,
          height: '100px',
          width: state.width
        }}
      ></div>
      <button onClick={() => dispatch('plus')}>
        Увеличить ширину контейнера.
      </button>
      <button onClick={() => dispatch('minus')}>
        Уменьшить ширину контейнера.
      </button>
    </>
  )
}
```

##### Установка нового состояния

```
const NewState = () => {
  const [state, setState] = useReducer(reducer, initialState)

  const [color, setColor] = useState('#f0f0f0')

  useEffect(() => {
    const randomColor = `#${((Math.random() * 0xfff) << 0).toString(16)}`
    setColor(randomColor)
  }, [state])

  return (
    <>
      <div
        style={{
          margin: '0 auto',
          background: color,
          height: '100px',
          width: state.width
        }}
      ></div>
      <button onClick={() => setState({ width: 300 })}>
        Увеличить ширину контейнера.
      </button>
      <button onClick={() => setState({ width: 30 })}>
        Уменьшить ширину контейнера.
      </button>
    </>
  )
}
```

##### useReducer + useContext

```
// TodoReducer.js
export const initialState = {
  todos: [
    { id: 1, text: 'Изучить React' },
    { id: 2, text: 'Изучить Redux' },
    { id: 3, text: 'Изучить GraphQL' }
  ]
}

export const reducer = (state, action) => {
  switch (action.type) {
    case 'add':
      return {
        todos: [...state.todos, action.payload]
      }
    case 'remove':
      return {
        todos: state.todos.filter((todo) => todo.id !== action.payload)
      }
    default:
      throw new Error('Что происходит?')
  }
}
```

```
// TodoContext.js
import { createContext } from 'react'

import { reducer, initialState } from './TodoReducer'

export const TodoContext = createContext()

export const TodoProvider = ({ children }) => {
  const [state, dispatch] = useReducer(reducer, initialState)

  return (
    <TodoContext.Provider value={[state, dispatch]}>
      {children}
    </TodoContext.Provider>
  )
}
```

```
// index.js
import React, { StrictMode, render } from 'react'

import { Form } from './Form'
import { List } from './List'

import { TodoProvider } from './TodoContext'

const root = document.getElementById('root')
render(
  <StrictMode>
    <TodoProvider>
      <Form />
      <List />
    </TodoProvider>
  </StrictMode>,
  root
)
```

```
// Form.js
import { useState, useContext } from 'react'

import { TodoContext } from './TodoContext'

export const Form = () => {
  const [text, setText] = useState('')
  // замыкающая запятая (trailing comma)
  const [, dispatch] = useContext(TodoContext)

  const handleChange = ({ target: { value } }) => {
    setText(value)
  }

  const handleSubmit = (e) => {
    e.preventDefault()

    const newTodo = {
      id: Date.now(),
      text
    }

    dispatch({ type: 'add', payload: newTodo })

    setText('')
  }

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Текст задачи: <br />
        <input type='text' value={text} onChange={handleChange} /> <br />
        <button>Добавить</button>
      </label>
    </form>
  )
}
```

```
// List.js
import { useContext } from 'react'

import { TodoContext } from './TodoContext'

export const List = () => {
  const [state, dispatch] = useContext(TodoContext)

  const handleClick = (id) => {
    dispatch({ type: 'remove', payload: id })
  }

  return (
    <ul>
      {state.todos.map(({ id, text }) => (
        <li key={id}>
          <span>{text}</span>
          <button onClick={() => handleClick(id)}>Удалить</button>
        </li>
      ))}
    </ul>
  )
}
```

#### useCallback

Хук `useCallback()` возвращает мемоизированную версию переданной функции обратного вызова. Данный хук принимает колбек и массив зависимостей. колбек повторно вычисляется только при изменении значений одной из зависимостей. Хук имеет следующую сигнатуру:

```
useCallback(
  fn,
  [deps]
) // deps - dependencies, зависимости
```

##### Базовый пример

```
const BasicCallback = () => {
  const [age, setAge] = useState(19)

  const handleClick = () => { setAge(age < 100 ? age + 1 : age) }

  const getRandomColor = useCallback(
    () => `#${((Math.random() * 0xfff) << 0).toString(16)}`,
    []
  )

  return (
    <>
      <Age age={age} handleClick={handleClick} />
      <Guide getRandomColor={getRandomColor} />
    </>
  )
}

const Age = ({ age, handleClick }) => {
  return (
    <div>
      <p>Мне {age} лет.</p>
      <p>Нажми на кнопку 👇</p>
      <button onClick={handleClick}>Стать старше!</button>
    </div>
  )
}

// `React.memo()` позволяет зафиксировать состояние компонента
const Guide = memo(({ getRandomColor }) => {
  const color = getRandomColor()

  return (
    <div style={{ background: color, padding: '.4rem' }}>
      <p style={{ color: color, filter: 'invert()' }}>
        Следуй инструкциям максимально точно.
      </p>
    </div>
  )
})
```

##### Зависимый колбек

```
const DependencyCallback = () => {
  const [age, setAge] = useState(19)

  const handleClick = () => { setAge(age < 100 ? age + 1 : age) }

  const getRandomColor = useCallback(
    () => `#${((Math.random() * 0xfff) << 0).toString(16)}`,
    [age]
  )

  return (
    <>
      <Age age={age} handleClick={handleClick} />
      <Guide getRandomColor={getRandomColor} />
    </>
  )
}

const Age = ({ age, handleClick }) => {
  return (
    <div>
      <p>Мне {age} лет.</p>
      <p>Нажми на кнопку 👇</p>
      <button onClick={handleClick}>Стать старше!</button>
    </div>
  )
}

const Guide = memo(({ getRandomColor }) => {
  const color = getRandomColor()

  return (
    <div style={{ background: color, padding: '.4rem' }}>
      <p style={{ color: color, filter: 'invert()' }}>
        Следуй инструкциям максимально точно.
      </p>
    </div>
  )
})
```

##### Более сложный пример

```
// пользовательский хук для добавления обработчиков событий
const useEventListener = (ev, cb, $ = window) => {
  const cbRef = useRef()

  useEffect(() => {
    cbRef.current = cb
  }, [cb])

  useEffect(() => {
    const listener = (ev) => cbRef.current(ev)

    $.addEventListener(ev, listener)

    return () => {
      $.removeEventListener(ev, listener)
    }
  }, [ev, $])
}

const CoordsCallback = () => {
  const [coords, setCoords] = useState({ x: 0, y: 0 })

  const cb = useCallback(
    ({ clientX, clientY }) => {
      setCoords({ x: clientX, y: clientY })
    },
    [setCoords]
  )

  useEventListener('mousemove', cb)

  const { x, y } = coords

  return (
    <h1>
      Координаты курсора мыши: {x}, {y}
    </h1>
  )
}
```

#### useMemo

Хук `useMemo()` является альтернативой хука `useCallback()`, но принимает любые значения, а не только функции. Данный хук имеет следующую сигнатуру:

```
useMemo(() => {
  fn,
  [deps]
}) // deps - зависимости
```

##### Базовый пример

```
const BasicMemo = () => {
  const [age, setAge] = useState(19)

  const handleClick = () => { setAge(age < 100 ? age + 1 : age) }

  const getRandomColor = () => `#${((Math.random() * 0xfff) << 0).toString(16)}`

  const memoizedGetRandomColor = useMemo(() => getRandomColor, [])

  return (
    <>
      <Age age={age} handleClick={handleClick} />
      <Guide getRandomColor={memoizedGetRandomColor} />
    </>
  )
}

const Age = ({ age, handleClick }) => {
  return (
    <div>
      <p>Мне {age} лет.</p>
      <p>Нажми на кнопку 👇</p>
      <button onClick={handleClick}>Стать старше!</button>
    </div>
  )
}

const Guide = memo(({ getRandomColor }) => {
  const color = getRandomColor()

  return (
    <div style={{ background: color, padding: '.4rem' }}>
      <p style={{ color: color, filter: 'invert()' }}>
        Следуй инструкциям максимально точно.
      </p>
    </div>
  )
})

```

##### Зависимая мемоизация[​](https://my-js.org/docs/cheatsheet/react-hooks/#%D0%B7%D0%B0%EF%BF%BD%D0%B2%D0%B8%D1%81%D0%B8%D0%BC%D0%B0%D1%8F-%D0%BC%D0%B5%D0%BC%D0%BE%D0%B8%D0%B7%D0%B0%D1%86%D0%B8%D1%8F "Direct link to Зависимая мемоизация")

```
const DependencyMemo = () => {
  const [age, setAge] = useState(19)

  const handleClick = () => { setAge(age < 100 ? age + 1 : age) }

  const getRandomColor = () => `#${((Math.random() * 0xfff) << 0).toString(16)}`

  const memoizedGetRandomColor = useMemo(() => getRandomColor, [age])

  return (
    <>
      <Age age={age} handleClick={handleClick} />
      <Guide getRandomColor={memoizedGetRandomColor} />
    </>
  )
}

const Age = ({ age, handleClick }) => {
  return (
    <div>
      <p>Мне {age} лет.</p>
      <p>Нажми на кнопку 👇</p>
      <button onClick={handleClick}>Стать старше!</button>
    </div>
  )
}

const Guide = memo(({ getRandomColor }) => {
  const color = getRandomColor()

  return (
    <div style={{ background: color, padding: '.4rem' }}>
      <p style={{ color: color, filter: 'invert()' }}>
        Следуй инструкциям максимально точно.
      </p>
    </div>
  )
})

```

##### Более сложный пример

```
const WordsMemo = () => {
  const [count, setCount] = useState(0)
  const [index, setIndex] = useState(0)

  const words = ['hi', 'programming', 'bye', 'real', 'world']
  const word = words[index]

  const getLetterCount = (word) => {
    let i = 0
    while (i < 1e9) i++
    return word.length
  }

  const memoized = useMemo(() => getLetterCount(word), [word])

  return (
    <div style={{ padding: '15px' }}>
      <h2>Вычисление количества букв (медленно 🐌)</h2>
      <p>
        В слове "{word}" {memoized} букв
      </p>
      <button
        onClick={() => {
          const next = index + 1 === words.length ? 0 : index + 1
          setIndex(next)
        }}
      >
        Следующее слово
      </button>

      <h2>Увеличение значения счетчика (быстро ⚡️)</h2>
      <p>Значение счетчика: {count}</p>
      <button onClick={() => setCount(count + 1)}>Увеличить</button>
    </div>
  )
}
```

#### useRef

Хук `useRef()` возвращает объект, свойство `current` которого содержит ссылку на узел DOM. Данный хук также может использоваться для сохранения любого мутирующего значения.

Создание хука: `const node = useRef()`.

Добавление ссылки: `<tagName ref={node}></tagName>`.

##### Получение доступа к DOM-элементу[​](https://my-js.org/docs/cheatsheet/react-hooks/#%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%B0-%D0%BA-dom-%D1%8D%D0%BB%D0%B5%D0%BC%D0%B5%D0%BD%D1%82%D1%83 "Direct link to Получение доступа к DOM-элементу")

```
const DomAccess = () => {
  const textareaEl = useRef(null)

  const handleClick = () => {
    textareaEl.current.value = 'Изучай хуки внимательно! Они не так просты, как кажется'
    textareaEl.current.focus()
  }

  return (
    <>
      <button onClick={handleClick}>Получить сообщение.</button>
      <label htmlFor='message'>
        После нажатия кнопки в поле для ввода текста появится сообщение.
      </label>
      <textarea ref={textareaEl} id='message' />
    </>
  )
}
```

##### Запуск и остановка таймера[​](https://my-js.org/docs/cheatsheet/react-hooks/#%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA-%D0%B8-%D0%BE%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0-%D1%82%D0%B0%D0%B9%D0%BC%D0%B5%D1%80%D0%B0 "Direct link to Запуск и остановка таймера")

```
const IntervalRef = () => {
  const [time, setTime] = useState(0)
  const interval = useRef()

  useEffect(() => {
    const id = setInterval(() => {
      setTime((time) => (time = new Date().toLocaleTimeString()))
    }, 1000)

    interval.current = id

    return () => clearInterval(interval.current)
  }, [time])

  return (
    <>
      <p>Текущее время:</p>
      <time>{time}</time>
    </>
  )
}
```

##### Несколько ссылок[​](https://my-js.org/docs/cheatsheet/react-hooks/#%D0%BD%D0%B5%D1%81%D0%BA%D0%BE%D0%BB%D1%8C%D0%BA%D0%BE-%D1%81%D1%81%D1%8B%D0%BB%D0%BE%D0%BA "Direct link to Несколько ссылок")

```
const StringVal = () => {
  const textareaEl = useRef(null)
  const stringVal = useRef('Изучай хуки внимательно! Они не так просты, как кажется')

  const handleClick = () => {
    textareaEl.current.value = stringVal.current
    textareaEl.current.focus()
  }

  return (
    <>
      <button onClick={handleClick}>Получить сообщение.</button>
      <label htmlFor='message'>
        После нажатия кнопки в поле для ввода текста появится сообщение.
      </label>
      <textarea ref={textareaEl} id='message' />
    </>
  )
}
```

##### Более сложный пример[​](https://my-js.org/docs/cheatsheet/react-hooks/#%D0%B1%D0%BE%D0%BB%D0%B5%D0%B5-%D1%81%D0%BB%D0%BE%D0%B6%D0%BD%D1%8B%D0%B9-%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-5 "Direct link to Более сложный пример")

```
const ProfileRef = () => {
  const firstNameInput = useRef(null)
  const lastNameInput = useRef(null)

  const [profile, setProfile] = useState({})

  function handleSubmit(e) {
    e.preventDefault()
    setProfile({
      firstName: firstNameInput.current.value,
      lastName: lastNameInput.current.value
    })
  }

  return (
    <>
      <h1>Профиль</h1>
      <form onSubmit={handleSubmit}>
        <input type='text' ref={firstNameInput} name='fistName' /> <br />
        <input type='text' ref={lastNameInput} name='lastName' /> <br />
        <button>Отправить</button>
        <p>
          Имя: {profile?.firstName} <br />
          Фамилия: {profile?.lastName}
        </p>
      </form>
    </>
  )
}
```

### Когда вызывается useEffect, до или после рендера?

[[Собес#^b9ea0b | После монтирования и отрисовки компонента]]

### Как выполнить действия на unmount с использованием хуков?

### Можно ли установить state зависимый от предыдущего?

### Какие способы оптимизации Реакт компонентов ты знаешь?

### Что такое порталы? Как их обычно используют?

## Redux + Saga
### Какие библиотеки менеджмента состояния React-приложения вы знаете? Зачем они нужны?

### Когда следует использовать Redux? Какие есть альтернативы?

### Что такое чистая функция?

### Что вы понимаете под «единым источником истины»?

### Опишите работу redux

### Что будет если мы мутируем состояние reducer?

### На чём основана работа Saga?

### Можно ли использовать в данные редакс в сагах?

### Что такое race?

## Web / Программирование

### Преимущества и недостатки монолитной и микросервисной архитектуры?

### Назовите способы хранения данных в браузере. Сравните их.

### Что такое Shadow DOM?

### Для чего используется noscript?

### Что такое CORS?

### Ко всем ли кукам есть доступ из js?

### Сколько ресурсов браузер может одновременно загружать с одного домена?

### Отличия HTTP и HTTPS?

### Как можно уменьшить время загрузки страницы?

### В чем разница между px, em и rem?

### Расскажите, как вы понимаете Web Accessibility.

### Что такое Babel и для чего он используется?

### Для чего нужен package.json.lock / yarn.lock?

### Что такое TDD (Test Driven Development) / BDD (Behavior Driven Development)?

### Какой фреймворк будете использовать для следующего проекта? Какие факторы будут влиять на выбор?

### В чём разница между интерфейсом и абстрактным классом?

### Какие существуют основные принципы ООП?

### Когда не нужно использовать принцип DRY?

### Расскажите о пирамиде тестирования.

### Что такое code coverage?

## Git

### Что такое Git?

### Какова цель команды git init?

### Можете ли вы описать суть методологии git flow в двух словах?

### Для чего нужен указатель HEAD?

### В чем разница между git merge и git rebase?

### Что такое «git remote» и «git clone»?

### Когда нужен параметр --force для git push?

### Что такое Git Stash?

### Какие ещё версии контроля вы знаете?
