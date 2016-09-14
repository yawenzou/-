# ie-
各个浏览器出现问题以及解决方法
###ie8下event事件
<pre><code>var eve = event||window.event;
var objEle = eve.target || eve.srcElement;
</code>
</pre>
<p>ie8下event事件是通过window.event来获取，当前元素是用srcElement</p>
###阻止事件冒泡
<pre>
    <code>
        if (event.stopPropagation) { 
        // this code is for Mozilla and Opera 
        event.stopPropagation(); 
        } 
        else if (window.event) { 
        // this code is for IE 
        window.event.cancelBubble = true; 
        }
    </code>
</pre>
