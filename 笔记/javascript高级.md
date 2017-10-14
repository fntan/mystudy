### 一、闭包

1. 闭包的定义

   - 闭包是引用了自由变量的函数

2. 闭包的特点

   - 闭包的函数和自由变量一同存在，即便离开了创建环境
   - 闭包的本质是作用域链

3. 闭包的应用

   - 减少全局变量的定义
   - 封装对象的成员

4. ### 闭包的缺点

   - 内存无法释放
   - 逻辑等错误

### 二、Javascript对象的创建

1. 字面量方式创建对象

   - ```javascript
     var obj = {		
     	stuName:‘Tom’,		
     	stuSex:‘男’,		
     	stuAge:20,		
     	sayHello:function(){		
     		alert(“你好!”);		
     	}	
     }
     ```

2. Object方式创建对象

   - ```javascript
     //封装Object方式创建对象
     function createObject(name,age){ 
     var person = new Object();     //创建对象
     person.name = name
     person.age = age;
     person.sayHi = function(){	
        	 alert(‘你好！我是’ + this.name);
     }
     return person；
     ｝
     //封装Object创建对象的方式也称为工厂模式
     //对象的属性可以动态添加，结束时需要返回对象
     ```


   - ```javascript
     var person = new Object();     //创建对象
     person.name = name
     person.age = age;
     person.sayHi = function(){	
        	 alert(‘你好！我是’ + this.name);
     }
     ```

3. 构造函数方式创建对象

   ```javascript
   function Human(name,age){  
     this.name=name;
     this.age=age;
        this.show = function(){	
      	 alert(‘你好！我是’ + this.name);
         }
       ｝
   var person1 = new Person("Nicholas", 29);
   var person2 = new Person("Greg", 27);
     //person1 和 person2 分别保存着 Human 的一个不同的实例。这两个对象都有一个 constructor（构造函数）     属性，该属性指向 Human,如下所示。
     alert(person1.constructor == Human); //true
     alert(person2.constructor == Human); //true
       //构造方法在创建对象时发挥作用，不创建对象时和普通方法相同
       //构造方法名首字母大写，通过new关键字创建实例对象
       //构造方法中不需要创建对象，也不用返回，依靠this关键字实现属性的设置
       //构造方法的对象是独立存储的，缺少共享，内存空间消耗较大
   ```

4. 原型方式创建对象

```javascript
 function Human(){}
Human.prototype.name =“tom”;
Human.prototype.age = 22;
Human.prototype.show = function(){
      alert(‘你好！我是’ + this.name);
}
var person1 = new Human();
  person1.show(); //你好！我是tom

   // 在每个对象上都支持一个属性proto；而在其他实现中，这个属性对脚本则是完全不可见的。不过，要明确的真正重		 要的一点就是，这个连接存在于实例与构造函数的原型对象之间，而不是存在于实例与构造函数之间。
   //原型方式实现对对象成员的共享，节省存储空间
   //引用导致实例对象的相互影响
```

5. 混合方式创建对象

   ```javascript
   function Human(name,age){
     this.name=name;
     this.age=age;
   ｝
    Human.prototype.country =“CHN”;
   Human.prototype.show = function(){
          alert(‘你好！我是’ + this.name);
    }
   //混合方式结合了构造函数方式和原型方式
   //构造函数方式用于定义实例的属性，而原型方式用于定义方法和共享的属性
   //支持向构造函数传递参数
   ```

### 三、类继承

1. 通过call、apply方法实现类的继承

   ```javascript
   function Human(name,age){
     this.name=name;
     this.age=age;
        this.show = function(){
   	alert(“I’m +” + this.name);
        }
   ｝
        function  Student(name,age){
            Human.call(this,name,age);    //实现继承
       }
   ```

2. 通过原型和构造函数实现继承

   ```javascript
   function Human(name){
     this.name=name;
     this.show = function(){
   	alert(“I’m +” + this.name);
        }
   ｝
   Human.prototype.city = ‘苏州’；
        function  Student(age){ 
              Human.call(this,age);
       ｝
        for(var Item in Human.prototype)
        	     Student.prototype[i] = Human.prototype[i]; 
   ```
   ```javascript
   function Person(){
   }
   Person.prototype.name = "Nicholas";
   Person.prototype.age = 29;
   Person.prototype.job = "Software Engineer";
   Person.prototype.sayName = function(){
   alert(this.name);
   };
   var person1 = new Person();
   var person2 = new Person();
   person1.name = "Greg";
   alert(person1.name); //"Greg"—— 来自实例
   alert(person2.name); //"Nicholas"—— 来自原型
   delete person1.name;
   alert(person1.name); //"Nicholas"—— 来自原型
   ```

   ​	当为对象实例添加一个属性时，这个属性就会屏蔽原型对象中保存的同名属性；换句话说，添加这
   个属性只会阻止我们访问原型中的那个属性，但不会修改那个属性。即使将这个属性设置为 null，也
   只会在实例中设置这个属性，而不会恢复其指向原型的连接。不过，使用 delete 操作符则可以完全删
   除实例属性，从而让我们能够重新访问原型中的属性 

   ### 更简单的原型语法

   之前每添加一个属性和方法就要敲一遍 Person.prototype。为减少不必要的输入，也为了从视觉上更好地封装原型的功能，更常见的做法是用一个包含所有属性和方法的对象字面量来重写整个原型对象，如下面的例子所示。 

   ```javascript
   function Person(){
   }
   Person.prototype = {
   name : "Nicholas",
   age : 29,
   job: "Software Engineer",
   sayName : function () {
   alert(this.name);
   }
   };
   //注意：constructor属性不再指向person了(指向了Object构造函数)
   //重写原型对象切断了现有原型与任何之前已经存在的对象实例之间的联系；它们引用的仍然是最初的原型
   ```

   ​

   ### 原型的动态性

   由于在原型中查找值的过程是一次搜索，因此我们对原型对象所做的任何修改都能够立即从实例上
   反映出来——即使是先创建了实例后修改原型也照样如此。请看下面的例子。 

   ```javascript
   var friend = new Person();
   Person.prototype.sayHi = function(){
   alert("hi");
   };
   friend.sayHi(); //"hi"（没有问题！）
   ```

   ​

3. 面向对象的理解

   - 对象是属性的集合
   - 函数和对象的关系
     - 对象都是通过函数生成的（new）
     - 函数也是一种对象
     - 函数的prototype属性指向原型对象，原型对象中的constructor指向函数
     - 对象具有隐性属性__proto__，指向原型对象