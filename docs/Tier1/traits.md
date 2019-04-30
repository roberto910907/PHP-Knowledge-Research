# Traits

Well, a Trait is simply a class that contains methods that can be shared with many classes. All classes that use this Trait can make use of its methods. They allow developers to write methods that can be used in any number of classes, keeping your code DRY and more maintainable.

Sometimes you will need to use multiple inheritance to make your classes extend from more than one parent, but this is not currently supported by PHP. It is an addition to traditional inheritance and enables horizontal composition of behavior; that is, the application of class members without requiring inheritance

> **Tips:** It is not possible to instantiate a Trait on its own.