# Ajax
搭建了服务器，实现了前端与服务器间的信息传递（响应纯文本与json），ajax与jquery封装的ajax，还有jsonp与XHR2实现了跨域

其中“测试记录”文档是我的执行结果的记录。


# 其他跨域技术


## CORS

IE8引入的XDR类型，异步执行，所以open的第三个参数就不写了


'var xhr=new XDomainRequest();

xdr.onload=function(){

   alert(xdr.responseText);
   
}

xdr.open("get","http://....");

xdr.send(null);'

## 其他浏览器对CORS实现用标准的XHR对象，在open中传入绝对URL即可。


### 跨浏览器的CORS

function creatCORSrequest(method,url){

  var xhr=new XMLHttpRequest();
  
  if("withCrendentials" in xhr){   //非IE
  
     xhr.open(method,url,true);
     
  }
  else if(typeof XDomainRequest !="undefined"){  //IE
  
    xhr=new XDomainRequest();
    
    xhr.open(method,url);
    
  }
  
  else{
  
    xhr=null;
    
  }
  
  return xhr;
  
}
var request=creatCORSrequest("get","http://....url即可.......");
if(request){
  request.onload=function(){
    //对request.responseText进行处理 
  };
  request.send();
}


## 图形Ping (单向，即不能访问响应文本；只能发get)  img可访问任何页面

var img=new Imge();

img.onload=img.onerror=function(){alert("Done!");}

img.src="hrrp://www.baidu.com/test?name=nichoals";


## Jsonp  （回调函数和数据）   script可访问任何页面

function handleResponds(response){alert("you are at in address"+response.ip+",which is in"+response.city+);}

//handleResponds方法中的参数response就是数据

var script-document.createElement("script");

script.src="http://www.baidu.com/test/json/?callback=handleResponds";//？后面就是回调函数

document.body.inserBefore(script,document.body.firstChild);
