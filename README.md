# DrupalMarkDown
## js
Drupal的js常见书写格式以及behaviors的用法[^1]

```
(function($){
  // 这个方法为闭包，所以如果我们如果需要全局使用里面的方法，
  // 必须讲这个方法放在Drupal对象内
  Drupal.myobj = myobj || {};
  Drupal.myobj.fun = function(){
    //todo
  }
  // behaviors 能够有效解决DOM重新加载(比如ajax)之后，
  // 新元素没有触发的问题(类似于jQuery live)
  Drupal.behaviors.fun1 = {
    attach: function (context, settings) {
      // Do something.
    },
    detach: function (context, settings, trigger) {
      // Undo something.
    }
  };
  $(function(){
    //这个等价于document.ready
  })
})(jQuery)
```

为了防止方法被多次执行

```
$('#element').once('myonce', function () { 
  // 这里的代码只会执行一次
});
```
###时间的计算
为了方便在js中计算时间的增加量，如果当前页面有datepicker，我们可以使用datepicker内的方法。而且datepicker本身就在misc内，也不需要另外下载。

```
$date = $.datepicker.parseDate('yy-mm-dd','2015-08-07');
$date.setDate($date.getDate()+2);
$.datepicker.formatDate('yy-mm-dd',$date);
```

###cookie的存储
D7默认加载jquery.cookie.js，不过版本比较老旧，仅为1.0

```
$.cookie('key',value,{path: '/'});
$.cookie('currency',null);
```

###表头悬浮
曾经碰到了这样的情况，前端用js，动态创建了一个table, 然后我们期望这个table和Drupal的其他常见表格一样能够表头悬浮。


假设table的ID是your_table_id

```
var mytable = $('#your_table_id');
mytable.data("drupal-tableheader", new Drupal.tableHeader('#your_table_id'));
```

[^1]: [听晴空讲Drupal主题——第七章 主题中的JS（3）](http://drupalchina.cn/node/5587)
