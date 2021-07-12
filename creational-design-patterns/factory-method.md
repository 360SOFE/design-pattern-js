# 工厂方法 Factory Method

## 简单工厂

### 核心代码

    class SimpleFactory {
        static manufacture: Product (kind: string) {
            switch (kind) {
                case "Product1":
                    return new Product1();
                case "Product2":
                    return new Product1();
                default:
                return null
            }
        }
    }

### 特点
- 又称静态方法模式
- 创建对象+switch结构，考虑用简单工厂
- 工厂类根据参数创建不同的具体对象实例
- 产品较少时

### 优点
> 解耦、面向接口编程

### 缺点
> 违反“开闭”、静态无等级结构

### code
[工厂方法示例代码](https://codesandbox.io/s/design-patterns-ih33q?file=/src/factory_method/Simple/SimpleFactory.ts)

-------

## 工厂方法

### 核心代码

    abstract class Factory {
        public abstract manufacture(): Product;
    }

    class Factory1 extends Factory {
        public manufacture(): Product {
            return new Product1();
        }
    }

    class Factory2 extends Factory {
        public manufacture(): Product {
            return new Product2();
        }
    }

### 特点
- 又称多态工厂模式，将类的实例化（具体产品的创建）延迟到工厂类的子类（具体工厂）中完成，即由子类来决定应该实例化（创建）哪一个类
- 此时工厂类不再负责所有产品的创建，而只是给出具体工厂必须实现的接口，这样工厂方法模式在添加新产品的时候就不修改工厂类逻辑而是添加新的工厂子类，符合开放封闭原则，克服了简单工厂模式中缺点

### 优点
> - 更符合开-闭原则
> - 符合单一职责原则
> - 不使用静态工厂方法，可以形成基于继承的等级结构。

### 缺点
> - 具体工厂类开销
> - 系统的难度增加
> - 一个具体工厂只能创建一种具体产品（抽象工厂改进）

### 应用场景
> - 客户只知道创建产品的工厂名，而不知道具体的产品名。
> - 创建对象的任务由多个具体子工厂中的某一个完成，而抽象工厂只提供创建产品的接口。
> - 客户不关心创建产品的细节，只关心产品的品牌

### code
[工厂方法示例代码](https://codesandbox.io/s/design-patterns-ih33q?file=/src/factory_method/Normal/Factory.ts)


