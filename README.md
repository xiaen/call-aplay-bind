# 实现：call、aplay、bind

实现call

​    function fn(name, age) {

​      this.name = name;

​      this.age = age;

​    }

​    Function.prototype.call2 = function (obj) {

​      function sy(obj) {

​        let num = Symbol((Math.random()) + (new Date()))

​        if (obj.hasOwnProperty(num)) {

​          return sy(obj)

​        } else {

​          return num

​        }

​      }

​      let ckey = sy(obj);

​      obj[ckey] = this;

​      //使用es6方法

​      //let arr = Array.from(arguments).slice(1)

​      //let res = obj[ckey](...arr)

​      //不使用es6方法

​      let arr = []

​      for (let i = 1; i < arguments.length; i++) {

​        arr[i - 1] = `arguments[${i}]`;

​      }

​      let res = eval('obj[ckey](' + arr.join(',') + ')')

​      delete obj[ckey];

​      return res;

​    }

​    let cThis = {}

​    fn.call2(cThis, '大毛', '黑色');