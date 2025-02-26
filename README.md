# 📌 Объекты (Object) в JavaScript

В JavaScript объекты — это структуры данных, которые используются для хранения коллекций значений и более сложных сущностей. Они позволяют организовывать данные в виде пар "ключ-значение".

---

## 🔹 Создание объекта

Объект можно создать несколькими способами:

### ✅ Литерал объекта
```js
const user = {
  name: "Alice",
  age: 25,
  greet: function() {
    console.log("Hello, " + this.name);
  }
};
```

### ✅ Использование `new Object()`
```js
const user = new Object();
user.name = "Alice";
user.age = 25;
```

### ✅ С помощью функции-конструктора
```js
function User(name, age) {
  this.name = name;
  this.age = age;
}
const user1 = new User("Alice", 25);
```

### ✅ С помощью `Object.create()`
```js
const userPrototype = {
  greet() {
    console.log("Hello, " + this.name);
  }
};
const user2 = Object.create(userPrototype);
user2.name = "Alice";
```

---

## 🔹 Методы объекта

Методы объекта — это функции, которые принадлежат объекту.

```js
const person = {
  name: "John",
  sayHello() {
    return "Hello, " + this.name;
  }
};
console.log(person.sayHello()); // "Hello, John"
```

Также можно добавлять методы динамически:

```js
person.sayGoodbye = function() {
  return "Goodbye, " + this.name;
};
console.log(person.sayGoodbye()); // "Goodbye, John"
```

---

## 🔹 `this` в объектах

Ключевое слово `this` в методах объекта указывает на сам объект.

```js
const car = {
  brand: "Toyota",
  model: "Camry",
  getInfo() {
    return `${this.brand} ${this.model}`;
  }
};
console.log(car.getInfo()); // "Toyota Camry"
```

⚠️ `this` ведет себя по-разному в зависимости от контекста. Например, в стрелочных функциях `this` берется из внешнего контекста:

```js
const obj = {
  value: 42,
  getValue: () => console.log(this.value) // Здесь `this` не относится к `obj`
};
obj.getValue(); // undefined
```

---

## 🔹 `call`, `apply` и `bind`

Методы `call`, `apply` и `bind` используются для управления значением `this`.

### ✅ `call()`
Вызывает функцию с заданным `this` и аргументами, переданными через запятую:

```js
function greet(greeting) {
  console.log(greeting + ", " + this.name);
}

const user = { name: "Alice" };
greet.call(user, "Hello"); // "Hello, Alice"
```

### ✅ `apply()`
Работает как `call`, но аргументы передаются массивом:

```js
greet.apply(user, ["Hi"]); // "Hi, Alice"
```

### ✅ `bind()`
Создает новую функцию с привязанным `this`:

```js
const boundGreet = greet.bind(user);
boundGreet("Hey"); // "Hey, Alice"
```

📌 `bind` часто используют для передачи методов объекта как коллбэки.

### 🔹 Пример использования `bind` с `setTimeout`

```js
const obj = {
  name: "Alice",
  sayHi() {
    console.log("Hi, " + this.name);
  }
};
setTimeout(obj.sayHi.bind(obj), 1000); // "Hi, Alice"
```

---

## 🔹 Перебор свойств объекта

Для перебора всех ключей объекта можно использовать `for...in`:

```js
const user = {
  name: "Alice",
  age: 25,
  city: "New York"
};

for (let key in user) {
  console.log(`${key}: ${user[key]}`);
}
```

Также можно использовать `Object.keys()`, `Object.values()` и `Object.entries()`:

```js
console.log(Object.keys(user)); // ["name", "age", "city"]
console.log(Object.values(user)); // ["Alice", 25, "New York"]
console.log(Object.entries(user)); // [["name", "Alice"], ["age", 25], ["city", "New York"]]
```

---

## 🔹 Деструктуризация объектов

Можно извлекать значения объекта с помощью деструктуризации:

```js
const user = { name: "Alice", age: 25 };
const { name, age } = user;
console.log(name); // "Alice"
console.log(age); // 25
```

Также можно задавать значения по умолчанию:

```js
const { city = "Unknown" } = user;
console.log(city); // "Unknown"
```

---

 😊

