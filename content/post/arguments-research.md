+++
title = 'Javascript Function Argument 筆記'
date = 2024-04-29T11:27:23+08:00
draft = false
+++
## Javascript Function Argument 筆記
紀錄實作工作上部分 function 使用 argument 直接取值時的一些筆記。

### Array-like Object

argument是類似`array`的物件，具有`length`可取得長度，如要調用`array`的函式，需要透過`call`。

```
function pump() {
    console.log('arguments', arguments)
    console.log('length', arguments.length)

    const joinString = Array.prototype.join.call(arguments, '&');
    console.log('joinString', joinString)
}

pump('BTC', 'ETH')
```

Output:
```
arguments Arguments(2) ['BTC', 'ETH', callee: ƒ, Symbol(Symbol.iterator): ƒ]
length 2
joinString BTC&ETH
```
### Argument 屬性
1. Length
   如上面範例所示，具有`length`屬性可取得長度。
2. callee
   可取得函數本身。

### 對應參數綁定特性
傳入的參數會與`arguments`的值會共享，但未傳入時將不會。
```
function pump(name, age, sex) {
    console.log(name, arguments[0]); // foo foo
    name = 'poo';
    console.log(name, arguments[0]); // poo poo

    console.log(age, arguments[1]); // 18 18
    arguments[1] = 20
    console.log(age, arguments[1]); // 20 20

    console.log(sex, arguments[2]); // undefined undefined
    sex = 'female';
    console.log(sex, arguments[2]); // female undefined   
}
pump('foo', 18)
```
### 常見操作

透過`ES6`可直接展開`arguments`為陣列。
```
function pump(...arguments) {
    console.log('arguments', arguments)  // ['foo', 18]
    console.log('lenth', arguments.length)  // 2
    console.log('join', arguments.join('&'))  // foo&18
}
pump('foo', 18)
```

透過`apply`傳遞參數至另一函式
```
function pump() {
    bump.apply(this, arguments)
}
function bump(name, age) {
    console.log('name', name)
    console.log('age', age)
}
pump('foo', 18)
```