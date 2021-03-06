﻿.. currentmodule:: DOM

data
=================================


Module
-----------------------------------------------

  :mod:`DOM`


Methods
-----------------------------------------------

.. function:: data( selector [ , name ] )

    获取符合选择器的第一个元素的扩展属性(expando).
    
    :param string|HTMLCollection|Array<HTMLElement> selector: 字符串格式参见 :ref:`KISSY selector <dom-selector>`
    :param string name: 扩展属性名称
    :returns:   * 对应扩展属性名的属性值, 如果不存在返回 ``null``
                * 如不指定扩展属性名, 则取得所有扩展属性键值对象 , 如果当前还没设置过扩展属性, 则返回空对象, 可以直接在该空对象上设置

.. function:: data ( selector, name, data )

    给符合选择器的所有元素的扩展属性(expando).设置扩展属性 name 为 data.
    
    :param string|HTMLCollection|Array<HTMLElement> selector: 字符串格式参见 :ref:`KISSY selector <dom-selector>`
    :param string name: 扩展属性名称
    :param value: 扩展属性值
    
.. function:: data( selector, kv )

    给符合选择器的所有元素设置扩展属性(expando).
    
    :param string|HTMLCollection|Array<HTMLElement> selector: 字符串格式参见 :ref:`KISSY selector <dom-selector>`
    :param object kv: 扩展属性名与扩展属性值的键值对

    .. note::

        embed, object, applet 这三个标签不能设置 expando .
        如果判断是否设置了扩展属性, 请使用 :func:`DOM.hasData`


    举例

    .. code-block:: javascript

        var S = KISSY, DOM = S.DOM;

        // 设置所有 img 的名为 data-size 的 expando , 值为 400;
        DOM.data('img', 'data-size', 400);

        // 获取第一个 img 元素中, 名为 data-size 的 expando 值;
        DOM.data('img', 'data-size');

        var p=DOM.create("<p>");

        DOM.hasData(p); // => false

        var store=DOM.data(p); // => store={}

        store.x="y"; // => 相当于 DOM.data(p,"x","y");

        DOM.removeData(p,"x");

        DOM.data(p,"x"); // => undefined

        DOM.hasData(p,"x"); // => false

        DOM.hasData(p) // => false

        DOM.data("p") // => 返回存储对象          