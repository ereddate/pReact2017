# pReact2017
ereddate/pReact的另一个版本，写法有些类似react、jQuery。

# 引用
```
<script src="preact.20170215.js"></script>
```
模板写法：
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
对象间的引用：
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
样式创建及引用：
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
事件的使用：
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
数据的获取：
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
