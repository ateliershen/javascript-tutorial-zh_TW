# 布林運算子

## 概述

布林運算子用於將表示式轉為布林值，一共包含四個運算子。

- 取反運算子：`!`
- 且運算子：`&&`
- 或運算子：`||`
- 三元運算子：`?:`

## 取反運算子（!）

取反運算子是一個感嘆號，用於將布林值變為相反值，即`true`變成`false`，`false`變成`true`。

```javascript
!true // false
!false // true
```

對於非布林值，取反運算子會將其轉為布林值。可以這樣記憶，以下六個值取反後為`true`，其他值都為`false`。

- `undefined`
- `null`
- `false`
- `0`
- `NaN`
- 空字串（`''`）

```javascript
!undefined // true
!null // true
!0 // true
!NaN // true
!"" // true

!54 // false
!'hello' // false
![] // false
!{} // false
```

上面程式碼中，不管什麼型別的值，經過取反運算後，都變成了布林值。

如果對一個值連續做兩次取反運算，等於將其轉為對應的布林值，與`Boolean`函式的作用相同。這是一種常用的型別轉換的寫法。

```javascript
!!x
// 等同於
Boolean(x)
```

上面程式碼中，不管`x`是什麼型別的值，經過兩次取反運算後，變成了與`Boolean`函式結果相同的布林值。所以，兩次取反就是將一個值轉為布林值的簡便寫法。

## 且運算子（&&）

且運算子（`&&`）往往用於多個表示式的求值。

它的運算規則是：如果第一個運運算元的布林值為`true`，則返回第二個運運算元的值（注意是值，不是布林值）；如果第一個運運算元的布林值為`false`，則直接返回第一個運運算元的值，且不再對第二個運運算元求值。

```javascript
't' && '' // ""
't' && 'f' // "f"
't' && (1 + 2) // 3
'' && 'f' // ""
'' && '' // ""

var x = 1;
(1 - 1) && ( x += 1) // 0
x // 1
```

上面程式碼的最後一個例子，由於且運算子的第一個運運算元的布林值為`false`，則直接返回它的值`0`，而不再對第二個運運算元求值，所以變數`x`的值沒變。

這種跳過第二個運運算元的機制，被稱為“短路”。有些程式設計師喜歡用它取代`if`結構，比如下面是一段`if`結構的程式碼，就可以用且運算子改寫。

```javascript
if (i) {
  doSomething();
}

// 等價於

i && doSomething();
```

上面程式碼的兩種寫法是等價的，但是後一種不容易看出目的，也不容易除錯，建議謹慎使用。

且運算子可以多個連用，這時返回第一個布林值為`false`的表示式的值。如果所有表示式的布林值都為`true`，則返回最後一個表示式的值。

```javascript
true && 'foo' && '' && 4 && 'foo' && true
// ''

1 && 2 && 3
// 3
```

上面程式碼中，例一里面，第一個布林值為`false`的表示式為第三個表示式，所以得到一個空字串。例二里面，所有表示式的布林值都是`true`，所以返回最後一個表示式的值`3`。

## 或運算子（||）

或運算子（`||`）也用於多個表示式的求值。它的運算規則是：如果第一個運運算元的布林值為`true`，則返回第一個運運算元的值，且不再對第二個運運算元求值；如果第一個運運算元的布林值為`false`，則返回第二個運運算元的值。

```javascript
't' || '' // "t"
't' || 'f' // "t"
'' || 'f' // "f"
'' || '' // ""
```

短路規則對這個運算子也適用。

```javascript
var x = 1;
true || (x = 2) // true
x // 1
```

上面程式碼中，或運算子的第一個運運算元為`true`，所以直接返回`true`，不再執行第二個運運算元。所以，`x`的值沒有改變。這種只通過第一個表示式的值，控制是否執行第二個表示式的機制，就稱為“短路”（short-cut）。

或運算子可以多個連用，這時返回第一個布林值為`true`的表示式的值。如果所有表示式都為`false`，則返回最後一個表示式的值。

```javascript
false || 0 || '' || 4 || 'foo' || true
// 4

false || 0 || ''
// ''
```

上面程式碼中，例一里面，第一個布林值為`true`的表示式是第四個表示式，所以得到數值4。例二里面，所有表示式的布林值都為`false`，所以返回最後一個表示式的值。

或運算子常用於為一個變數設定預設值。

```javascript
function saveText(text) {
  text = text || '';
  // ...
}

// 或者寫成
saveText(this.text || '')
```

上面程式碼表示，如果函式呼叫時，沒有提供引數，則該引數預設設定為空字串。

## 三元條件運算子（?:）

三元條件運算子由問號（?）和冒號（:）組成，分隔三個表示式。它是 JavaScript 語言唯一一個需要三個運運算元的運算子。如果第一個表示式的布林值為`true`，則返回第二個表示式的值，否則返回第三個表示式的值。

```javascript
't' ? 'hello' : 'world' // "hello"
0 ? 'hello' : 'world' // "world"
```

上面程式碼的`t`和`0`的布林值分別為`true`和`false`，所以分別返回第二個和第三個表示式的值。

通常來說，三元條件表示式與`if...else`語句具有同樣表達效果，前者可以表達的，後者也能表達。但是兩者具有一個重大差別，`if...else`是語句，沒有返回值；三元條件表示式是表示式，具有返回值。所以，在需要返回值的場合，只能使用三元條件表示式，而不能使用`if..else`。

```javascript
console.log(true ? 'T' : 'F');
```

上面程式碼中，`console.log`方法的引數必須是一個表示式，這時就只能使用三元條件表示式。如果要用`if...else`語句，就必須改變整個程式碼寫法了。
