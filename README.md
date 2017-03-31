# pReact2017
ereddate/pReact的另一个版本，写法有些类似react、jQuery。

# 引用
```
<script src="preact.20170215.js"></script>
```
# 模板写法：
```
<script type="text/pReact">
...
(
  <div style={styles.main}{style.clearfix}>
    <span style={styles.title}>pReact</span>
  </div>
)
...
</script>
```
或者javascript写法：
```
<script>
  let element = pReact.createDom("iframe", {
    src:"https://github.com/ereddate/pReact2017"
  }, pReact.createDom("span", {
    html:"pReact demo"
  }, ...));
</script>
```
# 对象间的引用：
```
let xnav = pReact.createClass("xnav", {
  render(){
    return (
      <div style={styles.xnav} id="{{id}}">
        <span>xnav element</span>
      </div>
    )
  }
}),
xpage = pReact.createClass("xpage", {
  render(){
    return (
      <div class="page">
        <xnav id="tools" style={styles.xnav}></xnav>
      </div>
    )
  }
});
pReact.renderDom(
  <xpage />,
  document.body
);
```
# 样式创建及引用：
```
let styles = pReact.createStyle({
  page:{
    background:"rgb(255,255,255),
    margin:0
  }
});
let demo = pReact.createClass("demo", {
  render(){
    return (
      <div style={styles.page}{styles.page}{styles.page}{styles.page}></div>
    )
  }
})
```
# 事件的使用：
```
let demo = pReact.createClass("demo", {
  handleClick(e){
    e.preventDefault();
    console.log(this);
  },
  ...
  render(){
    return (
      <div style={styles.page} ontouchstart={handleTouchStart}
        ontouchmove={handleTouchMove} ontouchend={handleTouchEnd}>
        <a href="javascript:;" onclick={handleClick}>{{title}}</a>
      </div>
    )
  }
})
```
# 数据的获取：
```
let demo = pReact.createClass("demo", {
  getInitData(success, error){
    ajax(url, (data) => {
      success(data)
    }, (err) => {
      error(err)
    })
  },
  render(){
    let a = document.createDocumentFragment();
    this._data.data.forEach((n) => {
       a.appendChild(pReact.tmpl((
        <div>
          <span>{{id}}</span>
        </div>
       ),n))
    });
    return a;
  }
});
或者
let demo = pReact.createClass("demo", {
  render(){
    return (
      <span>{{name}}</span>
    )
  }
});
pReact.renderDom(
  <demo name="a" />,
  document.body
)
```
# pReact提供的方法:
```
Callbacks
  Callbacks(function, function...).add(function).delay(time, function).done(function)
  顺序执行

createClass
  createClass(name, classObject)
  创建class，返回classObject

createDom
  createDom(tagName, options, 子节点...)
  创建节点，返回element

createStyle
  createStyle(styleJson)
  创建样式，返回styleJson

each
  each(object, function)
  each循环，返回pReact

extend
  extend(object, object)
  extend对象扩展，返回第一个object

findNode
  findNode(parent, selector)
  在父节点下按条件查找，支持多条件查找用空格分开，返回数组

get
  get(url, data, success, error, type, options)
  ajax下get请求

getBaseFontSize
  getBaseFontSize(num)
  获取基础字体大小的rem值

getStyle
  getStyle(name)
  获取pReact库中已知name的样式对象

import
  import(url).then(success, error).catch(function)
  引用js、CSS或其他文件，返回promise对象

is
  is(b, a)
  判断AB是否相同

isEmptyObject
  isEmptyObject(obj)
  判断是否为空对象

isPlainObject
  isPlainObject(obj)
  判断是否是普通对象

jsonp
  jsonp(url, data, ops).done(success function, error function)
  ajax下jsonp请求

loaded
  loaded()

loading
  loading()

mixElement
  mixElement(element)
  扩展element对象，增加40多个私有方法

off
  off(element, eventName)
  删除事件

on
  on(element, eventName, fn)
  增加事件

post
  post(url, data, success, error, type, options)
  ajax下post请求，data为空时传{}

ready
  ready(callback)

renderDom
  renderDom(name, data, parent, callback)
  生成element对象并插入parent，当完成后执行callback

renderPage
  renderPage()

serialize
  serialize(obj)
  form表单转字符串

storage
  storage(options).set(key, value).get(key).delete(key)
  本地存储，优先选用localStorage反之使用cookie

tmpl
  tmpl(html, data)
  模板转意

toAmp
  toAmp()
  让页面支持chrome amp

toMobile
  toMobile(num)
  将页面转为适合移动端页面

touchDirection
  touchDirection(startPoint, endPoint)
  判断touch滑动方向

trim
  trim(string)
  清除字符串空格

```
# Element对象私有方法
```
_set(option)
按配置重绘原有Element

_findNode(selector)
以当前节点为父节点近条件查找，支持多条件查找用空格分开，返回数组

_contents()
查找父节点下的全部子节点

_empty()
清空当前节点

_parents(selector)
按条件查找当前节点的父节点

_attr(name, value)
给属性赋值

_children(selector)
按条件查找当前节点的子节点

_removeAttr(name)
删除属性

_text(value)
取文本或赋文本

_html(value)
取html或赋html

_clone(bool)
克隆节点

_on(eventName, fn)
赋事件

_off(eventName)
删除事件

_trigger(eventName)
执行事件

_one(eventName, fn)
赋一次性事件

_remove(element)
删除当前节点

_append(element)
追加节点

_appendTo(element)
将当前节点追加到指定节点

_prepend(element)
开头插入节点

_prependTo(element)
插入到指定节点的开头

_after(element)
当前节点后插入指定指定节点

_css(name, value)
取或设置样式属性值

_addClass(name)
添加class名，支持添加多个class名，用空格分开

_removeClass(name)
删除class名，其他同上

_prop(name, value)
设置或返回属性值

_data(name, value)
设置或返回数据

_removeData(name)
删除数据

_toggleClass(name)
切换样式名

_hasClass(name)
判断是否包含指定样式名

_width(value)
宽度，value等于true，将返回包含margin\padding\border的值

_animate(styles, time, callback, timingFunction)
CSS3动画

_show()
显示

_hide()
隐藏

_height(value)
高度，其他同_width

_tmpl(data)
给当前标签的html模板赋值

_offset()
取绝对值，返回{top, left}

_index()
取索引值

_prevAll()
取当前节点前的同父节点的所有节点

_nextAll()
取当前节点后的同父节点的所有节点

_previous()
取上一节点

_next()
取下一节点

_has(a, b)
判断是否包含

_scrollLeft(value)
滚动条的水平偏移

_scrollTop(value)
滚动条的垂直偏移

```
