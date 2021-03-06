.. currentmodule:: Loader

KISSY.getScript
===================================

.. function:: KISSY.getScript(url , config)

    动态加载目标地址的资源文件
    
    :param string url: js/css 的资源地址
    :param object config: 动态加载配置对象，包括
    
        .. attribute:: config.charset
        
            类型 string，资源文件的字符编码
            
        .. attribute:: config.success
        
            类型 function，资源加载成功后回调函数
                * < 1.2 中对于 css 文件是理解回调，而不会等 css 加载完毕
                * 1.2+ 会等 css 加载完毕
                
        .. attribute:: config.error
        
            类型 function，超时或发生错误时回调函数。当资源文件为 css 文件时不支持
                      
        .. attribute:: config.timeout
        
            类型 number，单位为秒，默认 5 秒。超时后触发 error 回调。当资源文件为 css 文件是不支持
            
    :rtype: HTMLELement
    :returns: 创建的 link 节点或 script 节点        
    
.. function:: KISSY.getScript(url,success,charset)

    相当于调用 ``KISSY.getScript(url , { success : success , charset : charset });``                     
        