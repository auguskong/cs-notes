



将行为分布在各个对象当中，并让对象各自负责自己的行为

实例: 调用不同Map App的API接口

JavaScript动态类型语言的重要思想:

多态的意义: 同一个操作作用于不同的对象，可以产生不同的结果。 例子: 拍电影时候 导演喊action 不同岗位的工作人员做不同的动作 输入都是action命令, 输出可以是 摄像 打灯光 送道具 演戏 不同岗位就是多态

把不变的部分隔离出来，把可变的部分封装起来，就给予了我们扩展程序的能力，仅仅增加代码就能添加功能。

```javascript
var googleMap = {
  show: function() {
    console.log(...)
  }
}    
var baiduMap = {
  show: function() {
    console.log(...)
  }
}  

// 没有实现抽象的代码
var renderMap = function(type) {
  if (type === 'google') {
    googleMap.show();
  } else if (type === 'baidu') {
    baiduMap.show();
  }
}

// 实现了抽象的代码
var renderMap = function(map) {
  if (map.show isinstanceof Funtion) {
    map.show();
  }
}
renderMap(googleMap)
renderMap(baiduMap) 

// 做什么和怎么做是分开的 做什么: show() 怎么做: 每个对象有自己的实现 
```

JavaScript 直接通过clone对象来实现继承 不需要关心原来对象所属的类，不用`new Class()` 这种语法来通过Class类创造对象 例子: 飞机大战游戏里面 增加一个新的飞机替身 直接把当前的飞机对象clone一下 而不是new一个新的对象 然后再设置当前的血量 等级 攻击力等property