.. currentmodule:: io

io()
=================================


.. function:: io ( cfg )

    发送 io 请求
    
    :param Object cfg: 
    
        用来配置请求的键值对对象.所有的配置项都是可选的,可以通过 :func:`io.setupConfig` 来设置默认配置. 包含以下配置项
    
        .. attribute:: cfg.url
        
            类型 String. 本次请求发送的地址. 
            
        .. attribute:: cfg.accepts
        
            .. versionadded:: 1.2
                类型 Object. 该配置和 :attr:`~io.cfg.dataType` 一起确定当前发送给服务器的 Accept 头. 默认包括
            
                .. code-block:: javascript
                
                    {
                        xml: "application/xml, text/xml",
                        html: "text/html",
                        text: "text/plain",
                        json: "application/json, text/javascript"
                    }
                    
        .. attribute:: cfg.dataType
                 
            类型 String. 期望能够从服务器返回的数据类型. 
            
            .. versionadded:: 1.2
                如果没有指定，kissy 将尽量从返回的 ``mimeType`` | ``Content-type`` 相应头中推导出来 ('text/xml' 将推导出 xml , 'text/json' 将推导出 json). 
            
            默认支持的类型（该类型的响应信息会作为第一个参数传到 ``success`` ``complete`` 回调中）有:
            
            * "xml" : 返回响应信息代表的 xml 文档.
            * "text" : 返回响应信息串
            * "html" : 同 "text"        
            * "script" : 将响应信息作为脚本执行。
            * "json" : 返回响应信息代表的 json 对象.
            * "jsonp" : 返回 `jsonp <http://bob.pythonmac.org/archives/2005/12/05/remote-json-jsonp/>`_ 的响应信息代表的 json 对象.
            
            
        .. attribute:: cfg.processData    
            
            .. versionadded:: 1.2
                类型 boolean. 默认 true . 当 :attr:`~io.cfg.data` 为对象时是否用 :func:`~Lang.KISSY.param` 序列化.例如当需要传送一个 xml 到服务器时就不需要 param data，并且最好同时设置 contentType 为合适的值.
            
        .. attribute:: cfg.async
        
            类型 boolean. 默认 true.本次 xhr 请求是否异步发送，如果你需要同步发送，设置该配置为 false,注意同步请求在完成前会锁死浏览器. 
            
        .. attribute:: cfg.cache
        
            .. versionadded:: 1.2
                默认 true.如果设为 false, 则会自动给请求 url 加上时间戳.       
        
        .. attribute:: cfg.contentType
        
            设置请求头 Content-type, 默认 "application/x-www-form-urlencoded".
            
            .. note::
                数据总是以 utf-8 的编码传往服务器端.
                
        .. attribute:: cfg.context
        
            类型object.设置回调函数中的 this 值,默认为当前配置项.例如可以把一个 dom 节点作为 complete 回调函数的上下文:
            
            .. code-block:: javascript
            
                io({
                    url:'test.html',
                    context:document.body,
                    complete:function(){
                        this.className="complete";
                    }
                });
                
        .. attribute:: cfg.crossDomain
        
            类型 boolean.默认同域请求为 true,不同域间为 false。设置该值为 true，则强制 script 以及 jsonp 请求通过 ``script`` 节点发送，用于服务器重定向到其他域脚本的场景.  
            
       .. attribute:: cfg.data
       
            类型 object 或 String。如果为 Object 类型则会通过 :func:`~Lang.KISSY.param` 格式化为字符串.
                
       .. attribute:: cfg.serializeArray
       
            类型 boolean。默认 true。表示序列化 :attr:`~io.cfg.data` 时是否给数组值对应的键名加 ``[]`` ，例如           
             
                * ``true`` 时  ``{x:[1,2]} //=> x[]=1&x[]=2``
                * ``false`` 时 ``{x:[1,2]} //=> x=1&x=2``          
            
       .. method:: cfg.error (null, textStatus, xhrObj)
        
            请求失败时的回调函数.这个函数接受 2 个参数：
            
                * textStatus 表示错误信息，包括 "timeout" , "error" , "abort" 等
                * xhrObj 表示这次请求代表的 xhr 对象.
                
       .. method:: cfg.success ( data , textStatus , xhrObj)
            
            请求成功时的回调函数.该函数传入三个参数. 
                * data : 根据 dataType 格式化服务器响应信息的响应对象
                * textStatus : 描述成功的状态，一般是 "success"
                * xhrObj : 本次请求的 xhr 对象.
                
       .. method:: cfg.complete ( data , textStatus , xhrObj)
            
            请求完成时的回调函数.该函数传入三个参数. 
                * data : 根据 dataType 格式化服务器响应信息的响应对象，失败触发时为 null
                * textStatus : 描述成功的状态，一般是 "success"
                * xhrObj : 本次请求的 xhr 对象.     
                
            .. note::
                无论成功或失败都会触发改回调.                   
                
       .. attribute:: cfg.headers
        
            类型 Object.设置这次请求 xhr 的请求头.  
            
       .. attribute:: cfg.jsonp
        
            类型 String.覆盖这次 jsonp 请求的 callback 函数名. 这个值可以取代请求 url 中 ``callback=?`` 的 callback.例如 
            {jsonp:'onJsonLoad'} 会导致 'onJsonLoad=?' 发送给服务器端.
            
       .. attribute:: cfg.jsonpCallback
        
            类型 String|Function.覆盖这次 jsonp 请求 callback 函数对应的值 (``callback={jsonpCallback}``). 这个值将取代 kissy 默认生成的 UUID 值. 
            
            .. versionadded:: 1.2
                当传入函数时，该函数需要返回字符串，每次请求都会调用该函数得到用于替换的字符串.
                
                                
       .. attribute:: cfg.mimeType
        
            .. versionadded:: 1.2
                类型 String.跨平台设置 xhr 的 `mimeType <https://developer.mozilla.org/en/XmlHttpRequest#overrideMimeType%28%29>`_      
                
       .. attribute:: cfg.password
        
            .. versionadded:: 1.2
                对于需要验证的 http 请求设置密码.
                
       .. attribute:: cfg.username
        
            .. versionadded:: 1.2
                对于需要验证的 http 请求设置用户名.            
                
       .. attribute:: cfg.scriptCharset
        
            .. versionadded:: 1.2
                用于 dataType ``jsonp`` 和 ``script`` ，设定传输用的 script 节点的 ``charset`` 属性。只有当返回编码和当前页面编码不一致时使用. 
                
       .. attribute:: cfg.timeout
        
            类型 number , 对这次请求设个超时时间，单位毫秒. 当超时后会触发 ``error`` 以及 ``complete`` 回调 , 状态字符串为 "timeout".
            
       .. attribute:: cfg.type
        
            请求类型.可取值 "get" 或者 "post".
            
       .. attribute:: cfg.xhrFields
        
            类型 Object , 设置到原生 xhr 对象的键值对.例如为了进行跨域请求你可以设置 `withCredentials <https://developer.mozilla.org/en/http_access_control#Requests_with_credentials>`_ 为 true.
            
            .. code-block:: javascript
            
                io({
                    url:"ping.php",
                    xhrFields:{
                        withCredentials: true    
                    }
                });   
                
       .. attribute:: cfg.form
        
            .. versionadded:: 1.2
                类型 :ref:`KISSY selector <dom-selector>`
                
                    * 如果 form 的 enctype 为 `"multipart/form-data`` 则会采用 `iframe <http://www.webtoolkit.info/ajax-file-upload.html>`_ 的方式进行无刷新文件上传，
                    * 否则将 form 内的输入域和值序列化后通过 xhr 发送到服务器.                
                
.. note::
                
    .. versionadded:: 1.2
        ``io()`` 返回 ``XhrObj`` 对象.
        
    
XhrObj    
--------------------------    
.. versionadded:: 1.2

.. class:: XhrObj
        
        原生 XMLHttpRequest 以及 jsonp 等非 xhr 请求对象的一个封装类.
        
    .. attribute:: config    
    
        当前请求发送时的配置信息.
        
    .. attribute:: readyState
    
        类型整数. 表示请求完成状态。可用于判断当前请求是否完成. 4 表示完成，否则表示正在进行中.(xhr 会有更多取值，jsonp script 只有 0(初始化) 1(发送中) 4(完成))
        
    .. attribute:: status
    
        类型整数. 响应状态码. xhr 会有更多取值。``jsonp script`` 只有 200(成功) , 500(出错)
        
    .. attribute:: statusText
    
        类型字符串. 响应状态字符串. 最终同回调 :attr:`~io.cfg.complete` 中的 ``textStatus`` 一致.        
        
    .. attribute:: responseText(responseXML)
    
        返回响应对应的 text 和 xml（如果需要）.
        
    .. method:: getResponseHeader(key)
    
        获得对应的响应头值.仅对于 xhr 请求有效.
        
        :param String key: 响应头名
        
    .. method:: abort()
    
        如果当前请求还没完成则中断当前的请求.
        
        .. note::
        
            不仅可以中断 xhr 请求，还可以中断 jsonp 以及 script 请求，中断后会触发 :attr:`~io.cfg.error` ( textStatus == "abort" ) 以及 :attr:`~io.cfg.complete` 回调.         
            
            
例子
-------------------------------------------      
    
.. versionadded:: 1.2
    载入并执行一段脚本

.. code-block:: javascript

    io({
       type: "GET",
       url: "test.js",
       dataType: "script"
     });
       
   
发送数据给服务器，服务器返回后通知用户

.. code-block:: javascript

    io({
       type: "POST",
       url: "some.php",
       data: {
        x:'y'
       },
       success: function(msg){
         alert( "Data Saved: " + msg );
       }
     });
 
取得最新的 html 并显示

.. code-block:: javascript

    io({
      url: "test.html",
      cache: false,
      success: function(html){
        KISSY.one("#results").html(html);
      }
    });     

发送 xml 文档给服务器

.. code-block:: javascript

    var xmlDocument=S.parseXML("<a>h</a>");

    io({
       url: "page.php",
       processData: false,
       contentType:'text/xml',
       data: xmlDocument,
       type:'post'
     });
     
通过 xhr 发送 form 内容

.. code-block:: html

    <form>
        <input name='test' value='v' />
    </form>
    
    <script>
        io({
            
        });
    </script>                                               