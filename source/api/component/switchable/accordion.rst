﻿.. py:currentmodule:: Switchable

子类 Accordion
===================================================================


默认配置
-------------------------------------------------------------

S.Accordion 接口及配置项, 与 :attr:`~Switchable.Switchable` 相同, 其中以下配置项的默认值有所区别:


**Switchable.markupType**    默认为1, 选择自定义 trigger 和 panel 的 class


**Switchable.triggerType**    默认为 'click', 点击触发


新增配置
-------------------------------------------------------------

.. attribute:: Accordion.multiple

    (optional): {Booelan} 是否开启同时展开多个面板功能, 默认为 false