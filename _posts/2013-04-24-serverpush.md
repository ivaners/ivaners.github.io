---
layout: post
title: "基于jQuery与PHP实现Ajax长轮询(LongPoll)"
description: ""
category: 
tags: []
---
{% include JB/setup %}

传统的AJAX轮询方式，客服端以用户定义的时间间隔去服务器上查询最新的数据。种这种拉取数据的方式需要很短的时间间隔才能保证数据的精确度，但太短的时间间隔客服端会对服务器在短时间内发送出多个请求。

反转AJAX，就是所谓的长轮询或者COMET。服务器与客服端需要保持一条长时间的请求，它使得服务器在有数据时可以返回消息给客户端。

XHTML

    <div id="msg"></div>     
    <input id="btn" type="button" value="测试" />    


这里使用AJAX请求data.php页面获得‘success’的值,请求的时间达到80秒。在这80秒中若没有从服务端返回‘success’则一直保持连接状态，直到有数据返回或‘success’的值为0才关闭连接。在关闭连接后在继续下一次的请求。

    $(function(){   
        $("#btn").bind("click",{btn:$("#btn")},function(evdata){      
             $.ajax({      
                    type:"POST",      
                    dataType:"json",      
                    url:"data.php",      
                    timeout:80000,     //ajax请求超时时间80秒      
                    data:{time:"80"}, //40秒后无论结果服务器都返回数据      
                    success:function(data,textStatus){      
                        //从服务器得到数据，显示数据并继续查询      
                        if(data.success=="1"){      
                         $("#msg").append("<br>[有数据]"+data.text);      
                         evdata.data.btn.click();      
                        }      
                     //未从服务器得到数据，继续查询      
                        if(data.success=="0"){      
                        $("#msg").append("<br>[无数据]");      
                        evdata.data.btn.click();      
                        }      
                    },      
                 //Ajax请求超时，继续查询      
                 error:function(XMLHttpRequest,textStatus,errorThrown){      
                         if(textStatus=="timeout"){      
                             $("#msg").append("<br>[超时]");      
                             evdata.data.btn.click();      
                         }      
                 }      
                          
                });      
        });      
              
    });    


在这里是无限的循环，循环的结束条件就是获取到了返回结果返回Json数据。

并且接受$_POST['time']参数来限制循环的超时时间，避免资源的过度浪费。(浏览器关闭不会发消息给服务器，使用可能一直循环下去)

    if(emptyempty($_POST['time']))exit();      
    set_time_limit(0);//无限请求超时时间      
    $i=0;      
    while (true){      
        //sleep(1);      
        usleep(500000);//0.5秒      
        $i++;      
              
        //若得到数据则马上返回数据给客服端，并结束本次请求      
        $rand=rand(1,999);      
        if($rand<=15){      
            $arr=array('success'=>"1",'name'=>'xiaocai','text'=>$rand);      
            echo json_encode($arr);      
            exit();      
        }      
              
        //服务器($_POST['time']*0.5)秒后告诉客服端无数据      
        if($i==$_POST['time']){      
            $arr=array('success'=>"0",'name'=>'xiaocai','text'=>$rand);      
            echo json_encode($arr);      
            exit();      
        }      
    }   

运行效果:在图中可以看到无数据的请求时间达到了40S，在40S的请求中若获得数据则请求关闭。

![](http://ivaners.github.io/image/1335580.gif)

原文链接：http://www.xiaocai.name/emlog/?post=32