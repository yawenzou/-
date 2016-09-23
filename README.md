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
###图片预览
<pre>
    <code>
    <div id="previewImg" ></div>
    <input type="file" onchange="PreviewImage(this,'previewImg');" />
    </code>
</pre>
<pre>
    <code>
//js本地图片预览，兼容ie[5-9]、火狐、Chrome17+、Opera11+、Maxthon3
        function PreviewImage(fileObj, previewImgId) {
            var allowExtention = ".jpg,.bmp,.gif,.png"; //允许上传文件的后缀名
            var extention = fileObj.value.substring(fileObj.value.lastIndexOf(".") + 1).toLowerCase();
            var browserVersion = window.navigator.userAgent.toUpperCase();
            if (allowExtention.indexOf(extention) > -1) {//判断文件类型
                var imgNode = document.createElement("img");
                imgNode.style.width = '100%';
                imgNode.style.height = '100%';
                if (fileObj.files) {//兼容chrome、火狐7+、ie10+等
                    if (window.FileReader) {
                        var reader = new FileReader();
                        reader.readAsDataURL(fileObj.files[0]);
                        reader.onload = function (e) {
                            imgNode.setAttribute("src", e.target.result);
                        }
                    } else if (browserVersion.indexOf("SAFARI") > -1) {
                        alert("不支持Safari6.0以下浏览器的图片预览!");
                    }
                } else if (browserVersion.indexOf("FIREFOX") > -1) {//firefox
                    var firefoxVersion = parseFloat(browserVersion.toLowerCase().match(/firefox\/([\d.]+)/)[1]);
                    if (firefoxVersion < 7) {//firefox7以下版本
                        imgNode.setAttribute("src", fileObj.files[0].getAsDataURL());
                    } else {//firefox7.0+                    
                        imgNode.setAttribute("src", window.URL.createObjectURL(fileObj.files[0]));
                    }
                }
                else { //ie5-9
                    imgNode.setAttribute("src", fileObj.value);
                }
            } else {
                alert("仅支持" + allowExtention + "为后缀名的文件!");
                fileObj.value = ""; //清空选中文件
            }
            document.getElementById(previewImgId).appendChild(imgNode);
            return fileObj.value;    //返回路径
        }
    </code>
</pre>