﻿.. currentmodule:: DOM

attr
=================================

Module
-----------------------------------------------

  :mod:`DOM`

Methods
-----------------------------------------------

.. function:: attr( selector, name )

    获取符合选择器的第一个元素的属性值.
    
    :param string|HTMLCollection|Array<HTMLElement> selector: 字符串格式参见 :ref:`KISSY selector <dom-selector>`
    :param string name: 属性名称
    :returns: 对应属性名的属性值

    例如

    .. code-block:: javascript

       var S = KISSY, DOM = S.DOM;
       var c=DOM.create("<input type='checkbox' checked='checked'/>");
       DOM.attr(c,"checked") // => "checked"
       DOM.prop(c,"checked") // => true
        
.. versionchanged:: 1.2
    对没有设置的属性返回 ``null`` . 判断属性设置与否可以使用 :func:`DOM.hasAttr` . 如果需要获取 DOM properties，请使用 :func:`DOM.prop` 方法
    
    
.. function:: attr( selector, name, value )

    给符合选择器的所有元素设置属性值.
    
    :param string|HTMLCollection|Array<HTMLElement> selector: 字符串格式参见 :ref:`KISSY selector <dom-selector>`
    :param string name: 属性名称
    :param value: 属性值
    
.. function:: attr( selector, kv )

    给符合选择器的所有元素设置属性值.
    
    :param string|HTMLCollection|Array<HTMLElement> selector: 字符串格式参见 :ref:`KISSY selector <dom-selector>`
    :param object kv: 属性名与属性值的键值对
    
    例如

    .. code-block:: javascript

        var S = KISSY, DOM = S.DOM;

        // 同时设置多个属性
        DOM.attr('img', { src: 'kissy.png', width: 400, height: 400 });