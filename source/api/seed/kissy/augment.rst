.. currentmodule:: Seed

KISSY.augment
===============================

.. function:: KISSY.augment(r,s[,ov=true,wl])

    将 s.prototype 的成员复制到 r.prototype 上。
    
    :param function r: 将要扩充的函数
    :param function|object s: 扩充来源函数或对象。非函数对象时复制的就是 s 的成员。
    :param boolean ov: 是否覆盖 r 已经有的原型属性。
    :param Array<string> wl: 来源属性的白名单列表，只有列表中的被扩充。
    :return: r
    :rtype: function
    
例如：

.. code-block:: javascript

    var S = KISSY,
    Shoutable = {
        shout: function() { alert('I am ' + this.name + '.'); }
    };

    function Dog(name) { this.name = 'Dog ' + name; }
    function Pig(name) { this.name = 'Pig ' + name; }
    
    S.augment(Dog, Shoutable);
    S.augment(Pig, Shoutable);
    
    new Dog('Jack').shout(); // => I am Dog Jack.
    new Pig('Mary').shout(); // => I am Pig Mary.
    
augment 方法在 KISSY 里非常基础非常重要。
传统 OO 语言里，可以通过继承或接口来实现共性方法。
在 JavaScript 里，通过 mixin 特性，一切变得更简单。
augment 是动态语言 mixin 特性的体现，灵活运用，能让代码非常优雅简洁。