# Vue数据响应式

>以下内容只是本人在学习过程中对Vue数据响应式的理解，它并不深刻和完美，仅用于我对当下所学的梳理。

## 数据响应式是什么
Vue数据响应式可以这样理解：当一个状态改变之后，与这个状态相关的事务也立即随之改变，从前端来看就是数据状态改变后相关 DOM 也随之改变。数据模型仅仅是普通的 JavaScript 对象。而当你修改它们时，视图会进行更新。
****
## 数据响应式的实现方法及其步骤
**方法：**
对象可以通过``` Object.defineProperty(obj, prop, descriptor)```操作其访问器属性，使其拥有getter和setter方法。这是实现Vue数据响应式的基石。
getter和setter主要是用于对读和写的监控。

**步骤：**
Vue实现数据响应式的步骤一般是：
1. 创建一个Vue实例使其成为myData的代理(proxy)。
```JS
vm = new Vue({data:myData})  //此时vm成了myData的代理
```
2. 通过使用```Object.defineProperty``` 操作，使其拥有getter和setter方法。进而对myData的所有属性进行监控。
3. 当myData的属性发生变化时，由于setter和getter方法对myData属性的监控，vm可以察觉到myData的变化，然后调用render(data)实现视图更新。