# Javascript: this, Prototype, Class, Inheritance, Static, etc. 


This post stems from me being unclear about how javascript implements itself. Many talk about it being a prototype language, which doesn't mean much to me on its own. So, this is going to use code to show/uncover exactly what javscript does.

## Executive Summary

- functions are first class objects in JS, wherever they are placed
  - on objects
  - on object prototypes for named functions
  - on object constructor
- class enables inheritance
  - functions are on constructor
  - static places functions on class 
  - super refers to parent class (via extends)
- this is fungible and will screw you up
  - in () => {}
  - in classes
  - in objects
  - in call function (and the other one)
  - in promises
  
## Function location

- Functions keep to themselves and know nothing until called within the context of *this*.

Here is some code for the following.

```
/** A class with val=1. */
class A {
  
  /** */
  constructor() {
    this.val = 1;
  }
}

/** Both static and non-staic. Both return val from A. */
class AA extends A {
  
  /** */
  constructor() {
    super();
  }
  
  /** @return {int} */ 
  static sa() { return this.val; }
  
  /** @return {int} */
  a() { return this.val; }
}

/** Will transfer methods here, with val=2 now. So this.val is 2. */
class B {
  /** */
  constructor() {
    this.val = 2;
  }
}

let a1 = A();
let a2 = AA();
```

- Objects (instances of classes) have data but no functions
```
console.log('a1: ', a1);
console.log('a2: ', a2);
---
a1:  A { val: 1 }
a2:  AA { val: 1 }
```
