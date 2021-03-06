﻿.. currentmodule:: Node


addStyleSheet()
========================================

.. method:: NodeList.addStyleSheet(cssText[, id])

    .. versionadded:: 1.2
        将 cssText 字符串作为内联样式添加到文档中。
        
    :param string cssText: 样式内容
    :param string id: 内联样式所在 style 节点的 id       
    :rtype: NodeList
    :returns: 当前对象
    
.. note::

    该方法只可以在 window 和 document 上调用，例如：
    
    .. code-block:: javascript
    
        KISSY.use("node",function(S,Node){
            var $=Node.all;
            $(window).addStyleSheet("p {color:red;}"); // 段落颜色全部显示为红色
            // 或
            $(document).addStyleSheet("p {color:red;}","addCss");
        });    