# 真题实战

## 自己实现一个instanceof(object, target)函数
### 代码
```javascript
function myInstanceof(object, target) {
    if (typeof object !== 'object') { return false } // 判断参数1不为对象时直接返回 false
    let objectPrototype = Object.getPrototypeOf(object) // 获取参数1的原型对象
    let targetPrototype = target.prototype // 获取参数2的原型
    while (true) { // 无限次查询
        if (objectPrototype === null) {
            return false // 如果参数1的原型对象为空，直接返回 false
        }
        if (objectPrototype === targetPrototype) {
            return true // 如果参数1的原型对象与参数2的原型相等，直接返回 ture
        }
        objectPrototype = Object.getPrototypeOf(objectPrototype) // 本次遍历结束后，获取参数1的原型对象的原型对象，赋值到 objectPrototype，再次查询
    }
}
```
### 运行结果
```javascript
function A() { }
function B() { }
var a = new A()
console.log(a instanceof A) // 输出 true
console.log(myInstanceof(a, A)) // 输出 true
console.log(a instanceof B) // 输出 false
console.log(myInstanceof(a, B)) // 输出 false
```

## 根据下面 3 条总结规则，写一个函数按规则输入和输出
 - 输入: ["able""age","are"] 输出: "e"
 - 输入: ["dog""racecar","car"] 输出: ""
 - 输入: ["national""arrival","mental"] 输出: "al"

### 代码
```javascript
function getSameLastChar(arr) {
    let result = ""
    let times = 1
    while (true) {
        let last = arr[0]
        for (let i = 1; i < arr.length; i++) {
            let now = arr[i]
            let nowArr = now.split("")
            let lastArr = last.split("")
            if (times >= now.length && times >= last.length) {
                return result
            }
            if (nowArr[now.length - times] != lastArr[last.length - times]) {
                return result
            }
            last = arr[i]
        }
        result = last[last.length - times] + result
        times++
    }
}
```
### 运行结果
```javascript
const arr1 = ["able", "age", "are"]
const arr2 = ["dog", "racecar", "car"]
const arr3 = ["national", "arrival", "mental"]
console.log(getSameLastChar(arr1)); // 输出 "e"
console.log(getSameLastChar(arr2)); // 输出 ""
console.log(getSameLastChar(arr3)); // 输出 "al"
```