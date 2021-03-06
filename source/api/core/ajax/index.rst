.. module:: io

ajax
===============================================

|  ajax
|  作者: `承玉 <yiminghe@gmail.com>`_, `拔赤 <lijing00333@163.com>`_
|  `源码 <https://github.com/kissyteam/kissy/tree/master/src/ajax>`_ 

module
-----------------------------------------------

KISSY.io
  
Methods
-----------------------------------------------
    
  .. toctree::
   :titlesonly:
   
   io
   setupConfig
   get
   post
   getJSON
   jsonp
   upload
   
Events
----------------------------------------------

所有 io 请求都会在 io 模块上触发事件，可通过 ``io.on`` 来捕获所有的 io 请求，例如

.. code-block:: javascript
    
    var indicator=KISSY.one("#indicator"),num;
    
    //发送前显示 loading 状态
    io.on("send",function(){
        num++;
        indicator.show();
    });
    
    //发送后隐藏 loading 状态
    io.on("complete",function(){
        num--;
        if(!num)
            indicator.hide();
    });

.. data:: start

    当配置初始化后，获取传输对象前触发。事件对象包括一下属性
    
    .. attribute:: start.event.ajaxConfig
    
        当前的配置项
        
    .. attribute:: start.event.xhr
    
        .. versionadded:: 1.2
            当前的请求关联的 :class:`~io.XhrObj` 对象 
            
.. data:: send 

    请求发送前触发。可用于 loading indicator 显示时机。事件对象同 ``start`` 事件.   
    
.. data:: success

    服务器返回成功后触发.事件对象同 ``start`` 事件.        
    
.. data:: error

    服务器返回失败后触发.事件对象同 ``start`` 事件.           
    
.. data:: error

    服务器返回失败或成功后触发.事件对象同 ``start`` 事件.       