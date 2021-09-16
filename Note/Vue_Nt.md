Vue.js
<br> 
vue构造函数中的选项

```buildoutcfg
let a = new Vue({
    //选项
});

选项为键值对集，用','隔开
    
    
    挂载元素：   el: 'tag'
    
        该选项的作用是为uve实例提供挂载元素，接下来所有操作都在该元素内进行，元素外部不受影响
        选项的值可以使用CSS选择器   

    
    数据： data: {}
    
        通过data选项能够定义数据，这些数据可以绑定到实例对应的模板上
        在创建vue实例时，如果传入的data是一个对象，那么vue实例会代理data对象的所有属性，当这些属性
        发生变化时，视图也会发生变化。
    
   
   方法： methods
   
        methods选项可以定义多个方法。
        
   
   生命周期钩子函数：
   
        beforeCreate：初始化vue实例时调用
        
        created：实例创建后开始调用，此时还为进行DOM编译
        
        mounted：在DOM文件渲染完成后开始调用，相当于JS的window.onload()方法
        
        beforeDestroy：在销毁实例前调用，此时实例仍然有效
        
        destroy：在实例被销毁后调用
```
<br>
    数据绑定
<br>
<br>
        数据绑定是vue.js最重要的一个特性。建立数据绑定后，数据和视图会相互关联，当数据发生变化时
        视图会自动更新

        1.文本插值
        使用{{}}进行文本插值
        
        2.插入HTML
        使用v-html属性将HTML内容插入到标签中
        
        3.属性
        使用v-bind对属性进行绑定
<br>

过滤器

    