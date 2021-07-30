# lLikeAndroid.github.io
我的博客

以下为暂时记录的要添加的文章

vue开发-遇到的疑难杂症

兄弟组件通信问题：
在main.js里面new Vue()对象时，在参数里面添加一个beforeCreate()方法，这个是钩子函数，里面添加如下代码 Vue.prototype.$bus = this ，然后就可以在需要的页面里去使用事件总线了。
使用方式： this.$bus.$on(string, function) ;  this.$bus.$emit(string, object)  ;  this.$bus.$off(string)  ;  分别对应： 注册事件，冒泡事件，销毁事件。
具体使用方式： this.$bus.$on('detectionShow',(data)=>this.autoInspection(data));  this.$bus.$emit("switchOverPwdShow", true);  this.$bus.$off('detectionShow');

element-ui框架el-tree组件自定义渲染内容：
由于官方给的样例里面渲染数据格式是固定的，叶子节点展示的都是一个字符串，但是客户就提出了需要加上标志性内容，而且是要带有颜色的，由于使用样例里的格式是无法实现的，所以需要一个自定义的内容去渲染。
在el-tree里面添加 :render-content="renderContent"  ，这个是支持自定义渲染内容的。里面是一个方法，方法有两个参数，第一个是需要渲染的节点样式，第二个是节点对象，需要的内容都在里面，可以通过这个对象分辨出是否是叶子节点。
具体使用方法： renderContent(h,data) {
                return this.h('span',{},[
                    this.h('span', data.label + " ( "),
                    this.h("span",{
                        style: "color: #c1c1c1",
                        domProps:{
                            innerHTML: "xxxxxx"
                        }
                    }),
                    this.h('span', " ) "),
                ]);
            },
 以上例子是对每个节点都渲染为标签后面加上“（xxxxxx）”的字符串，而且这个字符串有颜色，其实这个节点是由三个span组成，可以通过代码可以看出，我们可以对返回对象进行嵌套，所以可以实现各种各样的节点样子。
 
 更改第三方框架样式：
 我们有时候不满意第三方框架的样式，需要调整成我们需要的样子，我们就需要在样式名前面添加 /deep/ 的代码。
 具体使用方式： /deep/ .text-title { width: xxxpx; height: xxxpx; }
 
 前台打断点调试方法：
 不止后端可以打断点调试，前台浏览器也是可以的，我们可以按F12打开打印台，然后选择source页面，然后选择webpack里面的src的相应代码文件，打开后选择行数就打了相应的断点了
