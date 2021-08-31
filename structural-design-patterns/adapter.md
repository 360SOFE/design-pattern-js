# 适配器模式 Adapter
通过本节的学习，可以了解以下内容：
1. 适配器模式的原理
2. 适配器模式的实现
3. 适配器模式的应用场景

## 回顾一下，创建型模式

我们已经接触过的创建型模式：

* 单例模式：用于创建全局唯一的对象
* 工厂模式：用于创建不同但是相关类型的对象。继承同一父类或者接口的一组子类
* 建造者模式：用于创建复杂对象。可以设置不同的可选参数，“定制化”的创建不同的对象
* 原型模式：对于创建成本比较大的对象，利用对已用对象进行复制的方式进行创建

## 结构型模式

主要总结了一些类和对象组合在一起的经典结构，这些结构可以解决特定用的应用场景的问题。

结构模式有：适配器模式、桥接模式、组合模式，代理模式、装饰器模式、门面模式、享元模式

## 适配器模式的原理

适配器模式就是用来做适配的，通过适配器模式可以将不兼容的接口转换为可兼容的接口。

日常生活中，我们使用的转接头可以更形象的描述适配器模式的原理，如下图国内的插座在国外就不能使用了，但是我们可以通过一个转接头来解决，这个转接头就是一种适配器。

![电源转接头](../.gitbook/assets/gp/shipeiqi.png)

## 适配器模式的结构

适配器模式分为对象适配器和类适配器。

### 对象适配器

适配器实现了其中一个对象的接口，并对另一个对象进行封装。所有流行的编程语言都可以实现对象适配器。

![对象适配器的结构图](../.gitbook/assets/gp/structure-object-adapter.png)

* Client 客户端，包含当前程序业务逻辑的类
* Client Interface 客户端接口，描述了其他类与客户端代码合作时必须遵循的协议。
* Service 服务中有一些功能类（通常来自第三方或遗留系统）。客户端与其接口不兼容，因此无法直接调用其功能。
* Adapter 适配器，可以同时与客户端和服务交互的类；它在实现客户端接口的同时封装了服务对象。适配器接受客户端通过适配器接口发起的调用，并将其转换为适用于被封装服务对象的调用。

客户端代码只需通过接口与适配器交互即可， 无需与具体的适配器类耦合。 因此， 你可以向程序中添加新类型的适配器而无需修改已有代码。 这在服务类的接口被更改或替换时很有用： 你无需修改客户端代码就可以创建新的适配器类。

```javascript
// 客户端接口
interface Target {
    f1():void;
    f2():void;
    fc():void;
}
// Service 服务
class Adaptee {
    constructor(){}
    public fa():void {
        console.log("服务：a");
    }
    public fb():void {
        console.log("服务：b");
    }
    public fc():void {
        console.log("服务：c");
    }
}
// 适配器
class Adapter implements Target {
    private adaptee: Adaptee;
    constructor(adaptee: Adaptee) {
        this.adaptee = adaptee;
    }
    public f1(): void {
        this.adaptee.fa();
    }
    public f2(): void {
        // 重新实现
        console.log("对象适配器:222");
    }
    public fc(): void {
        this.adaptee.fc();
    }
}
// 使用
const target: Target = new Adapter(new Adaptee());

target.f1(); // 服务：a
target.f2(); // 对象适配器:222
target.fc(); // 服务：c
```

### 类适配器

适配器同时继承两个对象的接口。这种方式仅能在支持多重继承的编程语言中实现。

![类适配器的结构图](../.gitbook/assets/gp/structure-class-adapter.png)

类适配器不需要封装任何对象，因为它同时继承了客户端和服务的行为。适配的功能在重写的方法中完成。最后生成的适配器可替代已有的客户端类进行使用。

```javascript
// 客户端接口
interface Target {
    f1(): void;
    f2(): void;
    fc(): void;
}

// service 服务
class Adaptee {
    constructor() {}
    public fa():void {
        console.log("服务：a");
    }
    public fb():void {
        console.log("服务：b");
    }
    public fc():void {
        console.log("服务：c");
    }
}

// 适配器
class Adapter extends Adaptee implements Target {
    constructor() {
        super();
    }
    public f1():void {
        super.fa();
    }
    public f2():void {
        // 重新实现
        console.log("类适配器：222");
    }
}
const target:Target = new Adapter();

target.f1(); // 服务：a
target.f2(); // 类适配器:222
target.fc(); // 服务：c
```

## 适配器模式的应用场景

