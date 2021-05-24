---
title: Ajax分页
top: false
cover: false
toc: true
mathjax: true
date: 2018-07-12 22:01:10
password:
summary:
tags: [分页,Ajax]
categories: Ajax
---

### Ajax分页已经封装完成 简单快捷使用[可遍历部分属性]

修改自己的请求地址  

**注意**： 样式需要导入bootstrap样式会好看一点


分页查询链接 返回的是一个总数目的int 值  在数据库查总条数就可以了

**单页数据查询返回的是一个json格式的数组** 

**注意：** 需要导入jQuery的jar包

代码如下：
```
var page=1;
      var pageend=0;
      /**
       *
       * 每页条目数量pagecount
       *
       */
      var pagecount=5;
      /**
       *
       * headnames  分页标题名称  按照顺序书写
       *
       */
      var headnames=new Array("id","用户名","where are you from")
      /**
       *
       * notlookattr  不需要遍历的对象属性
       *
       */
      var notlookattr=new Array("pwd")
      /**
       *
       * Numberhref  分页查询 链接
       *
       */
      var Numberhref="/user/selectPzd";
 
      /**
       *
       * limithref  单页数据查询 链接
       *
       */
      var limithref="/user/selectPzdLimit";
      /**
       *
       * 刷新分页方法*********************    flseh()  *******
       *
       */
 
      var pagechange=1;
      function  pageTurn(data){
          console.log(data)
          if(data=="?"){
              if(page!=1){
                  page=page-1;
                  flseh();
              }
          }else if(data=="?"){
              if(page!=pageend){
                  page=parseInt(page)+1;
                  flseh();
              }
          }else if(data=="..."){
              var endli=$("#pages li").slice($("#pages li").length-4,$("#pages li").length-3);
              pagechange=endli.text();
              page=pagechange;
              flseh()
 
          }else if(data=="."){
              var endli=$("#pages li").slice(2,3);
              if(endli.text()!=1){
                  pagechange=parseInt(endli.text())-10;
                  page=pagechange;
              }
              flseh()
          }else{
              page=parseInt(data);
              flseh();
          }
      }
      function flseh(){
          $.post(Numberhref,function (data) {
              $("#pages li").remove();
              pageend=data/pagecount;
              $("#pages").append('<li><a href="#">&#171;</a></li>')
              $("#pages").append('<li><a href="#">.</a></li>')
              for (var i=pagechange;i<data/pagecount+1;i++){
                  $("#pages").append('<li><a href="#">'+i+'</a></li>')
                  if(i-pagechange>10){
                      $("#pages").append('<li><a href="#">...</a></li>')
                      break;
                  }
              }
              $("#pages").append('<li><a href="#">&#187;</a></li>')
          })
          $(".usershead td").remove();
          for (var i = 0; i <headnames.length ; i++) {
              $(".usershead").append('<td>'+ headnames[i]+'</td>')
          }
          $.post(limithref,{begin:(page-1)*pagecount,end:pagecount},function (data) {
              $("#users tr").remove();
              for (var i=0;i<pagecount;i++){
                  $("#users").append('<tr id="'+i+'pagerow"></tr>')
                  Object.getOwnPropertyNames(data[i]).forEach(function (key) {
                      var notlookboo=true;
                      for(var j=0;j<notlookattr.length;j++){
                          if(key==notlookattr[j]){
                              notlookboo=false;
                          }
                      }
                      if(notlookboo){
                          $("tr[id='"+i+"pagerow']").append(('<td>' + data[i][key]+ '</td>'))
                      }
                  })
              }
 
          })
      }
```
## html代码 
**注意：** 样式需要导入bootstrap样式会好看一点
```
<table class="table table-hover">
        <thead>
            <tr class="usershead"></tr>
        </thead>
        <tbody id="users">
 
        </tbody>
    </table>
    <ul class="pagination" id="pages">
 
    </ul>
```