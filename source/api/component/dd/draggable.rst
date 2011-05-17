﻿.. currentmodule:: DD

Draggable
-----------------------------------------------


引入
=====================================

页面引入 kissy.js :

.. code-block:: html

    <script src='kissy.js'></script>



.. versionadded:: 1.2
    通过 use 加载 dd 模块：
    
    .. code-block:: javascript
    
        KISSY.use("dd",function(S,DD){
            var Draggable = DD.Draggable;
        });

.. seealso::

    KISSY 1.2 :mod:`Loader` 新增功能




构造器
================================

.. class:: Draggable(config)

    :param object config: 实例化可拖放对象的配置项，包括
    
        .. attribute:: config.node
        
            类型选择器字符串或者 HTMLElement ，将要进行拖放的节点。
            
        .. attribute:: config.handlers
        
            类型数组，数组每个元素是选择器字符串或者 HTMLElementNode ，作为鼠标在其上按下时触发节点拖放的钩子。
            如果不设置，则整个 ``node`` 作为触发钩子。
            
                .. note ::
                    
                    handlers 的每个元素 dom 节点必须位于配置项 ``node`` dom 子树中。
                    
        .. attribute:: config.cursor
        
            类型字符串，默认值 "move"，handlers 元素中的每个元素要设置的鼠标样式。
            
        .. attribute:: config.mode
        
            类型枚举字符串，默认值 "point"，和 ``Droppable`` 关联，决定何时和可放对象开始交互（触发相应事件），
            可取值 "point","intersect","strict"
            
            * 在 "point" 模式下，只要鼠标略过可放对象，即开始和可放对象交互。                          
            * 在 "intersect" 模式下，只要拖动对象和可放对象有交集，即开始和可放对象交互。
            * 在 "strict" 模式下，只有拖动对象完全位于可放对象内，才开始和可放对象交互。  


类常量
==========================================

.. data:: Draggable.POINT

    等于 "point"
    
.. data:: Draggable.INTERSECT

    等于 "intersect"
    
.. data:: Draggable.STRICT

    等于 "strict"      

    
实例属性
============================================

.. attribute:: Draggable.node

    类型 ``KISSY.Node`` ，表示当前拖动的节点，在应用 ``DD.Proxy`` 时表示代理节点。
    
.. attribute:: Draggable.dragNode

    类型 ``KISSY.Node`` ，表示配置项中 :attr:`~Draggable.config.node` 的值。    

    
.. note::

    实例属性通过 ``get`` 方法获取，例如 ``drag.get("node")``     
    
实例方法
===========================================

.. method::  Draggable.destroy()

    销毁当前可拖放对象实例，清除绑定事件。     


.. _draggable-events:
            
触发事件
=================================

.. data:: Draggable.dragstart

    当可拖放对象开始被用户拖放时触发，传给事件处理函数参数为事件对象 event ，包含
    
        .. attribute:: Draggable.dragstart.event.drag
        
            自身，当前拖放对象
    
    
.. data:: Draggable.drag

    当可拖放对象拖放过程中触发，传给事件处理函数为事件对象 event ，包含
    
        .. attribute:: Draggable.drag.event.left
        
            type number , 拖放节点应该设置的相对文档根节点的横坐标位置。
            
        .. attribute:: Draggable.drag.event.top
        
            type number , 拖放节点应该设置的相对文档根节点的纵坐标位置。
            
        .. attribute:: Draggable.drag.event.pageX
        
            type number , 当前鼠标的绝对横坐标       
            
        .. attribute:: Draggable.drag.event.pageY
        
            type number , 当前鼠标的绝对纵坐标
            
        .. attribute:: Draggable.drag.event.drag
        
            自身，当前拖放对象    
            
            
.. data::  Draggable.dragend

    当用户鼠标弹起放弃拖放时触发，传给事件处理函数参数为事件对象 event ，包含
    
        .. attribute:: Draggable.dragend.event.drag
        
            自身，当前拖放对象
    
.. data::  Draggable.dragenter

    同 :data:`Droppable.dropenter` ，只不过该事件在当前 Draggable 对象上触发。   
    
.. data::  Draggable.dragover

    同 :data:`Droppable.dropover` ，只不过该事件在当前 Draggable 对象上触发。

.. data::  Draggable.dragexit

    同 :data:`Droppable.dropexit` ，只不过该事件在当前 Draggable 对象上触发。
    
.. data::  Draggable.dragdrophit

    同 :data:`Droppable.drophit` ，只不过该事件在当前 Draggable 对象上触发。    
    
.. data::  Draggable.dragdropmiss

    当用户鼠标弹起但是没有放置当前 ``Draggable`` 对象到一个 Droppable 对象时触发。
    传给事件处理函数参数为一个事件对象 event
    
        .. attribute:: Draggable.dragdropmiss.event.drag
        
            自身，当前拖放对象
    
.. note ::

    ``Draggble`` 实例化后仅表示会根据鼠标拖放触发相应的事件，但具体怎么处理仍需要调用者自己控制，
    例如可监听 :data:`~Draggable.drag` 事件，根据事件对象参数的坐标设置拖放节点的具体位置。
    
        .. code-block:: javascript
        
            new Draggable({node :"#d"}).on("drag",function(ev){
                this.get("node").offset({left:ev.left,top:ev.top});
            });                                                        
                
                              