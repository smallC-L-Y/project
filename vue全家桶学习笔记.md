![image-20200402092105527](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200402092105527.png)<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401200523200.png" alt="image-20200401200523200" />认识Vue全家桶/生态圈

# 大纲

## 核心成员

vue：核心功能---插件，组件，数据管理，生命周期

vue-router：路由机制---拆分，拆开，将文件划分大小

vuex：vue官方提供的数据共享机制，全局性管理数据

## 编译打包

webpack：打包---js，css，图片，包的分隔，提供了很多开发功能

vue-loader：转换器

cli：脚手架，创建默认启动项目

## 开发支持

vue-devtools：按照组件查找

## 后端渲染

​	前端渲染：性能更高，用户体验更好；所有的代码都需要用js写，所有的页面都需要被用户看到；

​	后端渲染：安全性高，SEO

​	结合：

​		vue-server-renderer：后端渲染的核心组件

​		nuxt.js：整合环境	

## UI组件

​	element-UI

​	vue-element-admin

# Vue基础

## 历史介绍

angular 09年，复杂，学习曲线长，一开始被大家拒绝

react 13年，用户体验良好

vue 14年，用户体验良好，尤雨溪，无锡人

## 前端框架与库的区别

- jquery库 -> DOM(操作DOM) +请求
- art-template库 ->  模板引擎
- 框架 = 全方位功能齐全
  - 简单的DOM体验 + 发请求 + 模板引擎 + 路由功能
- KFC的世界里，库就是一个小小的套餐，框架就是全家桶
- 代码上的不同
  - 一般使用库的代码，是调用某个函数，我们自己把控库的代码
  - 一般使用框架，其框架在帮助我们运行编写好的代码
    - 框架：初始化一些行为
      - 执行你所编写的代码
      - 释放一些资源

## vue起步

- 引包

- 启动new Vue({el: 目的地，template：模板内容})；

- opations
  
  - 目的地  el
  - 数据源 data
  - 模板  template

## 插值表达式（{{}}）

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>vue的基本使用</title>
		<!-- 1 引入vue包 -->
		<script src="./node_modules/vue/dist/vue.min.js"></script>
	</head>
	<body>
		<div id="app">
			<!-- 数据绑定 -->
			<!-- vue的模板语法 {{}} 双括号 -->
			<h2>{{ name }}</h2>	<!-- 绑定数据值 -->
			<h3>{{ 1+1 }}</h3>	<!-- 做运算 -->
			<h4>{{ isTure }}</h4>	<!-- 判断真假 -->
			<h5>{{ str.split('').reverse().join('') }}</h5>	<!-- 使用js中的方法 -->
			<h1>{{ 1 > 2 ? '真' : '假' }}</h1>	<!-- 使用三元表达式 -->
			<h6>{{ {"name" : "张三"} }}</h6>		<!-- 插入对象 -->
		</div>
		<script type="text/javascript">
			// 2 创建实例化对象
			var app = new Vue({
				el: '#app',	 // el 挂载点,vue操作的对象
				data: {	// 数据属性
					// 操作对象绑定的数据
					// 既可以是一个对象,也可以是一个函数
					name: '小陈',
					hobby: '电子竞技',	//data中数据发生改变,视图也会发生改变,简而言之,数据驱动视图
					isTure: 1===1,
					str: 'hello vue'
				},
				// 如果template中定义了内容 那么优先渲染 template 模板中的内容
				// 如果没有定义内容,则加载的是#app中的模板
				<!-- template: `<div>{{ hobby }}</div>` -->
				template: ``
			});
			// 除了数据属性 vue 实例还暴露了一些有用的实例属性和方法
			// 她们都有前缀$
			console.log(app);
			// 我们可以通过app.$数据名来获取vue实例中的数据
			console.log(app.$data);
		</script>
	</body>
</html>
```

![image-20200327122537393](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200327122537393.png)

## 指令

- 在vue中提供了一些对于页面 + 数据的 跟为方便的输出，这些输出就成为指令，以v-xxx为例。
  - 比如html中的属性`<div v-xxx></div>`
- 在angular中以`ng-xxx`开头
- 在微信小程序中以`vx-xxx`开头
- 在vue中以`v-xxx`开头的就叫做指令
- 指令中封装了一些DOM行为，结合属性作为一个暗号，暗号有对应的值，根据不同的值，框架会进行相关的DOM操作的绑定

## vue中常用的指令

- v-text：元素的innerText属性，必须是双标签，跟{{}}效果是一样的，使用较少

- v-html：元素的innerHtml

- v-if ：判断是否插入这个元素，相当于元素的销毁和创建

- v-else-if

- v-else

- v-show：隐藏元素，如果元素确定要隐藏，会给元素的style加上`display:none`,是基于css样式的切换

- v-bind：给标签进行属性绑定（类似于：hover--给元素添加属性）【简写   ：bind】

- v-on：绑定事件	      

  - v-on：原生事件名 = '函数名'   【简写   @】

- v-for：遍历          

  - v-for = "(item, index)  in 数组名/对象名"      ---->     使用{{ itme.字段名 }}

  ```javascript
  v-text:只能在双标签中使用，其实就是给元素的innerText赋值
  v-html：其实就是给元素的innerHTML赋值
  v-if：如果值为false，不在页面上渲染，会留下<!---->作为标记，但是可视化界面上面没有显示，如果值为true就将值显示在可视化界面上面
  v-if,v-else-if都有相对应的值，v-else直接写
  v-show是控制DOM元素显示与否，true显示，false隐藏
  ```

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>vue的基本使用</title>
		<style type="text/css">
			.obj {
				width: 200px;
				height: 200px;
				border: 1px solid;
			}
			.obj2 {
				width: 200px;
				height: 200px;
				border: 1px solid;
			}
			.active {
				background-color: aqua;
			}
			table{
				/* 去掉表格中的横向 内部边框线 */
				 border-collapse: collapse;	/* 表格单元格间距样式 */
			}
		</style>
		<!-- 1 引入vue包 -->
		<script src="./node_modules/vue/dist/vue.min.js"></script>
	</head>
	<body>
		<div id="app">
		
		</div>
		<script type="text/javascript">
			// 2 创建实例化对象
			new Vue({
				el: '#app',
				data: function() {
					return {
						msg: 'v-text指令',
						msg2: '<i>斜体i标签</i>',
						isShow: false,
						isBlue: false,
						isRed: false,
						text: 'chenhaha',
						listData: [
							{id: 1, name: '小陈', sex: '女'},
							{id: 2, name: '小王', sex: '女'},
							{id: 3, name: '小姜', sex: '女'},
							{id: 4, name: '小唐', sex: '女'},
							{id: 5, name: '小黎', sex: '女'},
							{id: 6, name: '小肖', sex: '女'}
						],
						person: {
							name: '筱辰',
							hobby: '街舞，rap，吉他',
							age: 20
						}
					}
				},
				template: `
					<div id="app">
						// 通过text做数据的增加
						<h2 v-text = "1 + 1"></h2>
						
						<!-- 给标签添加text值 -->
						<h3 v-text = "msg"></h3>
						
						<!-- 给标签嵌套html标签innerHTML -->
						<div v-html = "msg2"></div>
						
						<!-- 根据条件的真假输出对应项的值 -->
						<div v-if = 'isShow'>雨天，写作业</div>
						<div v-if = '!isShow'>晴天，出去耍，晒太阳</div>
						
						
						<div v-if = 'Math.random() > 0.5'>随机数大于0.5</div>
						<div v-else>随机数小于0.5</div>
						
						<!-- 根据属性值来让元素显示隐藏，实际上是改变display的值 none|block -->
						<div v-show = 'isShow'>夏天</div>
						<div v-show = '!isShow'>夏天</div>
						
						<!-- v-bind 绑定class  通过属性值来让元素增加隐藏 -->
						<div class = "obj" v-bind:class = "{active:!isBlue}" v-on:click = 'clickDiv'></div>
						<!-- v-bind还可以绑定自定义属性 -->
						<div v-bind:aaa = 'text'></div>
						
						<!-- 遍历数组 -->
						<table border="1">
							<tr>
								<th>编号</th>
								<th>姓名</th>
								<th>性别</th>
							</tr>
							<tr   v-for = '(item, index) in listData'>
								<td>{{ item.id }}</td>
								<td>{{ item.name }}</td>
								<td>{{ item.sex }}</td>
							</tr>
						</table>
						
						<!-- 遍历对象 -->
						<ul>
							<li v-for = "(value,key) in person">
								{{ key }} -------> {{ value }}
							</li>
						</ul>
					</div>
				`,
				methods: {
					clickDiv(e) {
						this.isBlue = !this.isBlue;
					}
				}
			});
		</script>
	</body>
</html>
```



## v-if和v-show的区别

v-if 是 “真正”的条件渲染，因为他会确保在切换过程中条件块内的事件监听器和子组件适当的被销毁和重建

v-if也是惰性的：如果在初始渲染时条件为假，则什么也不做——知道条件第一次变为真时，才开始渲染条件块。

相比之下，v-show就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单的基于css进行切换。（导航栏）

一般来说，v-if有更高的切换开销，而v-show有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用v-show较好，如果在运行时条件很少改变，则使用v-if较好。

## vue的双向绑定（v-model）

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 1 引入vue包 -->
		<script src="./node_modules/vue/dist/vue.min.js"></script>
	</head>
	<body>
		<div id="app">
			<!-- 单项数据绑定 -->
			<span>单项数据绑定：</span>
			<input type="text" :value="mag"/>
			<hr />
			<!-- 双向数据绑定   只会体现在UI控件上面  只能应用在value属性上 -->
			<span>双向数据绑定：</span>
			<input type="text" v-model="msg"/>
			<h1>{{ msg }}</h1>
			<hr />
			<!-- 实际上就是一个 语法糖，它是v-bind:value v-on:input的体现 -->
			<span>双向数据实现原理：</span>
			<input type="text" v-bind:value="mfg" v-on:input="valueChange"/>
			<h1>{{ mfg }}</h1>
		</div>
		<script type="text/javascript">
			new Vue({
				el: '#app',
				data() {
					return {
						mag: "小猪佩奇",
						msg: "好友记",
						mfg: "肖申克的救赎"
					}
				},
				methods: {
					valueChange(e){
						console.log(e.target.value);
						this.mfg = e.target.value;
					}
				}
			});
		</script>
	</body>
</html>
```

![image-20200327173446887](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200327173446887.png)

## vue中的template（入口组件）

入口组件包含了：html，css，js

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200327175015513.png" alt="image-20200327175015513" style="zoom:50%;" />

### 局部组件

打油诗：声子  挂子   用子

创建：(类似于自定义全局组件，使用时直接在父组件中，通过局部组件的声明名调用即可)

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 1 引入vue包 -->
		<script src="./node_modules/vue/dist/vue.min.js"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// 局部入口组件的的声明
			var App = {
				data() {
					return {
						
					}
				},
                // 局部入口组件的内容
				template: 
				`
					<h2>我是局部入口组件</h2>
				`
			};
			// 2 实例化对象
			new Vue({
				el: "#app",
				data() {
					return {
						
					}
				},
				<!-- 挂载子组件 -->
				components: {
					App	<!-- 类似于App:App -->
				},
				<!-- 父组件可以直接使用子组件 -->
				template: 
				`
					<app></app>	
				`
			});
		</script>
	</body>
</html>
```

### 全局组件

```javascript
// 全局组件
// 第一个参数是组件的名字,第二个参数是组件的样式
Vue.component('V-button',{
	template:
		`
			<button>按钮</button>
		`
});
```

注意：在使用局部组件和全局组件时，不能单独使用，每个组件都是一个整体，在组件中使用全局组件和局部组件时，必须要写在组件的内部，它们是一个整体。

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 1 引入vue包 -->
		<script src="./node_modules/vue/dist/vue.min.js"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// 全局组件
			// 第一个参数是组件的名字,第二个参数是组件的样式
			Vue.component('V-button',{
				template:
				`
					<button>按钮</button>
				`
			});
			
			// 声子
			var Rightcentent = {
				data() {
					return {
						
					}
				},
				template: 
				`
					<div>
						<div>我是右边内容组件</div>
						<V-button></V-button>
					</div>
				`
			};
			<!-- 侧边栏组件 -->
			var Leftcentent = {
				data() {
					return {
						
					}
				},
				template: 
				`
					<div>我是左边菜单栏组件</div>
				`
			};
			<!-- 头部组件 -->
			var Header = {
				data() {
					return {
						
					}
				},
				template: 
				`
					<div>我是头部组件</div>
				`
			};
			// 局部入口组件的的声明
			var App = {
				data() {
					return {
						
					}
				},
				template: <!-- 用子 	注意：在使用创建的子组件是是一个整体，不能分散开来，不然只能显示第一个子组件的值-->
				`
					<div>
						<Header></Header>
						<div>
							<Leftcentent></Leftcentent>	
							<Rightcentent></Rightcentent>
						</div>
					</div>	
				`,
				<!-- 挂子 -->
				components: {
					Header,
					Leftcentent,
					Rightcentent
				}
			};
			// 2 实例化对象
			new Vue({
				el: "#app",
				data() {
					return {
						
					}
				},
				<!-- 挂载子组件 -->
				components: {
					App	<!-- 类似于App:App -->					
				},
				<!-- 父组件可以直接使用子组件 -->
				template: 
				`
					<app></app>						
				`
			});
		</script>
	</body>
</html>
```

### 父组件往子组件中传值

1 先给父组件绑定自定义属性
2 在子组件中使用prop接收父组件传递的数据
3 只要使用props接收了数据之后，就可以在子组件中任意使用 

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 1 引入vue包 -->
		<script src="./node_modules/vue/dist/vue.min.js"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// 声明全局组件    子组件
			Vue.component('Child',{
				template: 
				`
					<div>
						<p>我是孩子</p>
						<input type="text" v-model="childData"/>
					</div>
				`,
				<!-- 接收自定义属性 -->
				props: ['childData']
			});
			<!--  声明全局组件    父组件 -->
			<!-- 1 先给父组件绑定自定义属性 -->
			<!-- 2 在子组件中使用prop接收父组件传递的数据 -->
			<!-- 3 只要使用props接收了数据之后，就可以在子组件中任意使用 -->
			Vue.component('Parent',{
				data() {
					return {
						msg: '我是父组件中的数据'
					}
				},
				template: 
				`
					<div>
						<p>我是父亲</p>
						<!-- 在子组件中挂载自定义属性 -->
						<Child :childData = 'msg'/>
					</div>
				`
			});
			// 声子
			var App = {
				template:
				`
					<div>
						<Parent />
					</div>
				`
			};
			// 2 实例化对象
			new Vue({
				el: "#app",
				data() {
					return {
						
					}
				},
				<!-- 挂载子组件 -->
				components: {
					App	<!-- 类似于App:App -->					
				},
				<!-- 父组件可以直接使用子组件 -->
				template: 
				`
					<app></app>						
				`
			});
		</script>
	</body>
</html>
```



### 子组件往父组件中传值

1.在父组件中绑定自定义事件 
2.在子组件中触发原生的事件,在函数中使用$emit触发自定义函数 

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 1 引入vue包 -->
		<script src="./node_modules/vue/dist/vue.min.js"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// 声明全局组件    子组件
			Vue.component('Child',{
				template: 
				`
					<div>
						<p>我是孩子</p>
						<input type="text" v-model="childData" @input="changeValue(childData)"/>
					</div>
				`,
				<!-- 接收自定义属性 -->
				props: ['childData'],
				methods: {
					changeValue(val){
						<!-- 自定义的时间一定通过thi.$emit()去触发 -->
						<!-- 在函数中使用$emit(自定义的事件名,传递的消息) -->
						this.$emit('childHeader',val);
					}
				}
			});
			<!-- 1.在父组件中绑定自定义事件 -->
			<!-- 2.在子组件中触发原生的事件,在函数中使用$emit触发自定义函数 -->
			Vue.component('Parent',{
				data() {
					return {
						msg: '我是父组件中的数据'
					}
				},
				template: 
				`
					<div>
						<p>我是父亲</p>
						<!-- 在子组件中挂载自定义属性 -->
						<Child :childData = 'msg' @childHeader = 'childHeader'/>
					</div>
				`,
				methods: {
					childHeader(val){
						console.log(val);
					}
				}
			});
			// 声子
			var App = {
				template:
				`
					<div>
						<Parent />
					</div>
				`
			};
			// 2 实例化对象
			new Vue({
				el: "#app",
				data() {
					return {
						
					}
				},
				<!-- 挂载子组件 -->
				components: {
					App	<!-- 类似于App:App -->					
				},
				<!-- 父组件可以直接使用子组件 -->
				template: 
				`
					<app></app>						
				`
			});
		</script>
	</body>
</html>
```

### vue内置全局组件（插槽）

插槽：slot 插槽，作为承载分发内容的出口

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<style type="text/css">
			.default {
				display: inline-block;
				line-height: 1;
				white-space: nowrap;
				cursor: pointer;
				background: #fff;
				border: 1px solid #dcdfe6;
				color: #606266;
				-webkit-appearance: none;
				text-align: center;
				box-sizing: border-box;
				outline: none;
				margin: 0;
				transition: .1s;
				font-weight: 500;
				-moz-user-select: none;
				-webkit-user-select: none;
				-ms-user-select: none;
				padding: 12px 20px;
				font-size: 14px;
				border-radius: 4px;
			}

			.primary {
				color: #fff;
				background-color: #409eff;
				border-color: #409eff;
			}

			.success {
				color: #fff;
				background-color: green;
				border-color: #409eff;
			}
		</style>
		<!-- 1 引入vue包 -->
		<script src="./node_modules/vue/dist/vue.min.js"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// 通过插槽的方式封装全局组件
			Vue.component('Vbtn', {
				template: `
					<button class = 'default' :class = 'type'>
						<slot>
							按钮
						</slot>
					</button>
				`,
				props: ['type']
			});
			<!-- 声子 -->
			var Vcontent = {
				template: `
					<div>
						我是内容组件
						<Vbtn type = 'primary'>主要按钮</Vbtn>
						<Vbtn type = 'success'>成功按钮</Vbtn>
					</div>
				`
			};
			// 2 实例化对象
			new Vue({
				el: "#app",
				data() {
					return {

					}
				},
				<!-- 挂子 -->
				components: {
					Vcontent <!-- 类似于App:App -->					
				},
				<!-- 用子 -->
				template: `
					<Vcontent></Vcontent>						
				`
			});
		</script>
	</body>
</html>

```

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200328104431413.png" alt="image-20200328104431413" style="zoom:50%;" />

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200328104605397.png" alt="image-20200328104605397" style="zoom:80%;" />

### 具名插槽(通过slot上的name)

```javascript
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title></title>
	<script src="./node_modules/vue/dist/vue.min.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
	<div id="app"></div>
	
	<script type="text/javascript">
		Vue.component('myli',{
			template: 
			`
				<li>
					预留的第一个空白
					<slot name = 'two'></slot>
					
					预留的第二个空白
					<slot name = 'three'></slot>
				</li>
			`
		})
		var App = {
			template: 
			`
				<div>
					<ul>
						<myli>
							<h2 slot = 'two'>我是第一个空白</h2>
							<h2 slot = 'three'>我是第二个空白</h2>
						</myli>
					</ul>
				</div>
			`
		}
		<!-- 实例化vue -->
		new Vue({
			el: '#app',
			components: {
				App
			},
			template: `<App></App>`
		});
	</script>
</body>
</html>
```

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200328110152313.png" alt="image-20200328110152313" style="zoom:50%;" />

## 过滤器

过滤器的功能：就是为页面中的数据进行添油加醋的功能

过滤器的分类：

1. 局部过滤器
2. 全局过滤器

```javascript
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title></title>
	<script src="./node_modules/vue/dist/vue.min.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
	<div id="app"></div>
	<script type="text/javascript">
		// 过滤器的功能：就是为页面中的数据进行添油加醋的功能
		// 有两种:局部过滤器 全局过滤器
		
		// 声明全局过滤器
		Vue.filter('myReverse', function(value,arg) {
			return arg + value.split('').reverse().join('');
		});
		var App = {
			data() {
				return {
					price: 0,
					msg: 'filter'
				}
			},
			template: 
			`
				<div>
					<input type="number" v-model = 'price'/>
					<!-- 使用局部过滤器  {{ 数据 | 过滤器名 }} -->
					<h2>{{ price | myCurrentcy }}</h2>	
					
					<!-- 使用全局过滤器 -->
					<h4>{{ msg | myReverse('I am going to study well you ') }}</h4>
				</div>
			`,
			filters: {
				<!-- 1 声明局部过滤器 -->
				myCurrentcy: function(value) {
					return "￥" + value;
				}
			}
		}
		<!-- 实例化vue -->
		new Vue({
			el: '#app',
			components: {
				App
			},
			template: `<App></App>`
		});
	</script>
</body>
</html>
```

## 监视（watch）

watch监听的是单个属性。

基本的数据类型，简单监视。

复杂的数据类型深度监视。

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<script src="./node_modules/vue/dist/vue.min.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="app">
			<input type="text" v-model="msg">
			<h2>{{ msg }}</h2>
			<button type="button" @click="stus[0].name = 'rose'">获取用户名</button>
			<h4>{{ stus[0].name }}</h4>
		</div>
		<script type="text/javascript">
			new Vue({
				el: '#app',
				data() {
					return {
						msg: '',
						stus: [{name: 'jack'}]
					}
				},
				watch: {	
					//简单监视
					// 字符串
					msg: function(newV, oldV) {
						console.log(newV, oldV);
					},
					//深度监视
					stus:{
						deep: true,	
						handler:function(newV, oldV) {
							console.log(newV, oldV);
							console.log(newV[0].name);
						}
					}
				}
			})
		</script>
	</body>
</html>
```

## 计算属性

利用computed计算属性写网页版音乐播放器。

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<style type="text/css">
			*{
				padding: 0;
				margin: 0;
			}
			ul{
				list-style: none;
			}
			ul li {
				margin: 20px 20px;
				padding: 20px 20px;
			}
			.active{
				background-color: aquamarine;
			}
		</style>
		<script src="./node_modules/vue/dist/vue.min.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="app">
			<audio :src='getCurrentSongSrc' autoplay="autoplay" controls="controls"></audio>
			<ul>
				<li v-for="(item,index) in musicData" @click="clickHander(index)" :class="{active:currentIndex == index}">
					<h2>{{ item.id }} - 歌名：{{ item.name }}h2>
					<p>歌曲来源：{{ item.sonSrc }}</p>
				</li>
			</ul>
		</div>
		<script type="text/javascript">
			var musicData = [
				{
					id: 1,
					name: '世界美好与你环环相扣',
					author: '柏松',
					sonSrc: 'music/世界美好与你环环相扣.mp3'
				},
				{
					id: 2,
					name: '昨天的你现在的未来',
					author: '易烊千玺',
					sonSrc: 'music/昨天的你现在的未来.mp3'
				},
				{
					id: 3,
					name: '精彩才刚刚开始',
					author: '易烊千玺',
					sonSrc: 'music/精彩才刚刚开始.mp3'
				}
			];
			new Vue({
				el: '#app',
				data() {
					return {
						musicData:musicData,
						currentIndex:0
					}
				},
				computed:{
					// 计算属性默认只有getter
					// setter也可以
					
					// 使用getter
					// getCurrentSongSrc:function(){
					// 	return this.musicData[this.currentIndex].sonSrc
					// }
					
					// 使用setter
					getCurrentSongSrc:{
						set: function(newV){
							console.log(newV);
							this.currentIndex = newV;
						},
						get:function(){
							return this.musicData[this.currentIndex].sonSrc
						}
						
					}
				},
				methods:{
					clickHander(index){
						// 使用getter
						// 直接修改数据的属性
						// this.currentIndex = index;
						
						// 使用setter
						console.log(this.getCurrentSongSrc);
						this.getCurrentSongSrc = index;
					}
				}
			})
		</script>
	</body>
</html>

```

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200328123325181.png" alt="image-20200328123325181" style="zoom:80%;" />



## 组件的生命周期

- beforeCreate
  
  - 组件创建之前
- created
  
  - 组件创建之后，就可以拿到自定义组件里面的内容
- beforeMount
  
  - 挂载数据到DOM之前会调用
- mounted
  
  - 挂载数据到DOM之后
- beforeUpdate
  
  - 在更新DOM之前调用该钩子，应用：可以获取原始的DOM
- updated
  
- 在更新DOM之后调用该钩子，应用：可以获取原始的DOM
  
- beforeDeatory

  - 销毁数据之前

- destroyed

  - 销毁数据之后

- activated

  - 激活组件

- deactivated

  - 停用组件

  ```javascript
  <!DOCTYPE html>
  <html lang="zh">
  	<head>
  		<meta charset="UTF-8">
  		<meta name="viewport" content="width=device-width, initial-scale=1.0">
  		<meta http-equiv="X-UA-Compatible" content="ie=edge">
  		<title></title>
  		<script src="./node_modules/vue/dist/vue.min.js" type="text/javascript" charset="utf-8"></script>
  	</head>
  	<body>
  		<div id="app">
  			<App></App>
  		</div>
  		<script type="text/javascript">
  			Vue.component('Test', {
  				data() {
  					return {
  						msg: 'lorry'
  					}
  				},
  				template: `
  				<div>
  					<h2>{{ msg }}</h2>
  					<button @click = 'changerHanlder'>改变</button>
  				</div>
  			`,
  				methods: {
  					changerHanlder() {
  						this.msg = this.msg + 'hello';
  					}
  				},
  				beforeCreate: function() {
  					<!-- 组件创建之前 -->
  					console.log(this.msg); <!-- 打印输出undefined -->
  				},
  				created: function() {
  					<!-- 组件创建之后 -->
  					console.log(this.msg); <!-- 打印输出lorry -->
  					<!-- 使用该组件，就会调用created方法 -->
  					<!-- 在created这个方法中可以操作后端的数据，数据驱动视图 -->
  					<!-- 应用：发起ajax请求 -->
  				},
  				beforeMount: function() {
  					<!-- 挂载数据之前 -->	<!-- 打印输出<div id="app"><app></app></div> -->
  					console.log(document.getElementById('app'));
  				},
  				mounted: function() {
  					<!-- 挂载数据到DOM之后 		Vue作用之后的DOM-->
  					<!-- 打印输出<div id="app"><div class="app"><div><h2>lorry</h2></div></div></div> -->
  					console.log(document.getElementById('app'));
  				},
  				beforeUpdate: function() {
  					<!-- 在更新Dom之前使用改方法 -->
  					<!-- 打印输出 <div class="app"><div><h2>lorry</h2> <button>改变</button></div></div> -->
  					console.log(document.getElementById('app').innerHTML);
  				},
  				updated: function() {
  					<!-- 在更新DOM之后使用该方法 -->
  					<!-- 打印输出 <div class="app"><div><h2>lorryhello</h2> <button>改变</button></div></div> -->
  					console.log(document.getElementById('app').innerHTML);
  				},
  				beforeDeatory: function() {
  					<!-- 销毁数据之前 -->
  					console.log('beforeDeatory'); <!-- Test组件中内容的显示隐藏的时候，打印输出beforeDeatory -->
  				},
  				destroyed: function() {
  					<!-- 销毁数据之后 -->
  					console.log('destroyed'); <!-- Test组件中内容的显示显示的时候，打印输出destroyed -->
  				},
  				activated: function() {
  					console.log('组件被激活了');
  				},
  				deactivated: function() {
  					console.log('组件被停用了');
  				},
  			});
  			var App = {
  				data() {
  					return {
  						isShow: true
  					}
  				},
  				template: `
  				<div class = "app">
  					<!-- <Test v-if = 'isShow'></Test> -->
  					
  					<!-- vue中的内置组件<keep-alive></keep-alive>，能在组件的切换过程中将所有的状态保存在内存中，重复渲染DOM -->
  					<keep-alive>
  						<Test v-if = 'isShow'></Test>
  					</keep-alive>
  					<!-- 根据按钮点击事件确定 Test组件中内容的显示隐藏-->
  					<!-- 点击两次后，再次点击切换，后台会重新创建Test，然后再次调用beforeDeatory和destroyed -->
  					<button @click = 'isShow = !isShow'>点击切换</button>
  				</div>
  			
  			`
  			};
  			new Vue({
  				el: '#app',
  				data() {
  					return {
  
  					}
  				},
  				components: {
  					App
  				}
  			})
  		</script>
  	</body>
  </html>
  ```

  

### keep-alive标签

在组件的切换过程中将所有的状态保存在内存中，重复渲染DOM（缓存）

#### keep-alive在路由中的使用

keep-alive保存加载过的数据，使用时直接调用，不用再次加载，节省项目运行时间，提高用户体验。

```javascript
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title></title>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script src="./node_modules/vue-router/dist/vue-router.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
	<div id="app"></div>
	<script type="text/javascript">
		var Timeline = {
			template:
			`
				<div id = 'timeline'>
					<h2>首页</h2>
				</div>
			`,
			created() {
				console.log('首页组件创建了');
			},
			mounted() {
				console.log('首页组件DOM加载了');
			},
			destroyed() {
				console.log('首页组件销毁了');
			}
		};
		var Pins = {
			template:
			`
				<div>
					<h2 @click = 'clickHandle'>沸点</h2>
				</div>
			`,
			methods: {
				clickHandle(e) {
					e.target.style.color = 'red';
				}
			},
			created() {
				console.log('沸点组件创建了');
			},
			mounted() {
				console.log('沸点组件DOM加载了');
			},
			destroyed() {
				console.log('沸点组件销毁了');
			}
		};
		<!-- // 创建路由对象 -->
		var router = new VueRouter({
			<!-- mode: 'history',	哈希模式，页面跳转时路由不会出现#  -->
			routes:[
				{
					path: '/timeline',
					component: Timeline
				},
				{
					path: '/pins',
					component: Pins
				}
			]
		});
		<!-- // 实例化app组件 -->
		var App = {
			template:
			`
				<div>
					<!-- 动态路由路径 -->
					<router-link to = '/timeline'>首页</router-link>
					<router-link to = '/pins'>沸点</router-link>
					<!-- 路由匹配组件的出口 -->
					<!-- <router-view></router-view> -->
					<!-- 使用keep-alive后，如果前面的数据缓存过后，就不会重新加载，直接调用 -->
					<keep-alive>
						<router-view></router-view>	
					</keep-alive>
				</div>
			`
		}
		<!-- // 实例化对象 -->
		new Vue({
			el: '#app',
			router,
			template: `<App></App>`,
			<!-- 挂载组件 -->
			components: {
				App
			}
		})
	</script>
</body>
</html>
```

## vue组件的通信方式

vue组件之间通信可分为：

### props和$emit(也就是常说的父子组件通信，**常用**)【父子组件中的传值】

父组件向子组件传递数据是通过props传递的，子组件传递数据给父组件是通过$emit触发事件来做到的。

解决父子组件层数较少的情况

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
</head>
<body>
	<div id="app"></div>
	<script src="https://cdn.bootcss.com/vue/2.5.17-beta.0/vue.js"></script>
	<script type="text/javascript">
		/*
			在下面的例子中，有父组件App和子组件Child。 
			1).父组件传递了message数据给子组件，并且通过v-on绑定了一个getChildData事件来监听子组件的触发事件； 
			2).子组件通过props得到相关的message数据,最后通过this.$emit触发了getChildData事件。

		*/
		Vue.component('Child',{
			data(){
				return {
					aaa:this.message
				}
			},
			template:`
				<div>
					<input type="text"  v-model="aaa" @input="passData(aaa)"/>
				</div>
			`,
			props:['message'],
			methods:{
				passData(val){
                    // $emit（自定义事件名，传递的值）
					this.$emit('getChildData',val);
				}
			}
		});
		var App = {
			data(){
				return {
					msg:'我是父组件的内容'
				}
			},
			methods:{
				getChildData(val){
					console.log(`我是子组件传进来的${val}`);
				}
			},
			template:`<div>
				<p>这是一个父组件</p>
				<Child :message = 'msg' @getChildData = "getChildData"></Child>

			</div>`
		}

		new Vue({
			el:"#app",
			data(){
				return {

				}
			},
			components:{
				App
			},
			template:`<App />`
		});




	</script>
	
</body>
</html>
```

### $attrs(绑定属性)和$listeners（监听）  【父子组件中的传值】

$attrs是$pops的集合

解决多层组件之间的嵌套和传值方法

绑定事件，传值，然后通过事件来接收传递的值

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title></title>
</head>

<body>
    <div id="app"></div>
    <script src="https://cdn.bootcss.com/vue/2.5.17-beta.0/vue.min.js"></script>
    <script type="text/javascript">
    /*
    $attrs和$listeners
    第一种方式处理父子组件之间的数据传输有一个问题： 如果父组件A下面有子组件B， 组件B下面有组件C, 这时如果组件A想传递数据给组件C怎么办呢？
    如果采用第一种方法， 我们必须让组件A通过prop传递消息给组件B， 组件B在通过prop传递消息给组件C； 要是组件A和组件C之间有更多的组件， 那采用这种方式就很复杂了。 Vue 2.4 开始提供了$attrs和$listeners来解决这个问题， 能够让组件A之间传递消息给组件C。
    */
      Vue.component('C', {
        data() {
            return {

            }
        },
        template: `
				<div>
					<div @click = 'cClickHandler'>{{$attrs.messagec}}</div>
				</div>
			`,
        methods: {
           cClickHandler(){
           	alert(1);
           	this.$emit('getCData','我是c的数据')
           }
        }
    });
      Vue.component('B', {
        data() {
            return {

            }
        },
        template: `
				<div>
					<C v-bind="$attrs" v-on = '$listeners'></C>
				</div>
			`,
        methods: {
           
        }
    });

    Vue.component('A', {
        data() {
            return {

            }
        },
        // props:['message'],
        template: `
				<div>
					<B v-bind="$attrs" v-on = '$listeners'></B>
					<!--<input type="text" v-model = '$attrs.messagec' />-->
				</div>
			`,
        methods: {
           
        }
    });
    var App = {
        data() {
            return {
                msg: '我是父组件的内容',
                messagec:'hello c'
            }
        },
        methods: {
          
        },
        template: `<div>
				<p>这是一个父组件</p>
				<A :messagec = 'messagec' v-on:getCData="getCData" ></A>

			</div>`,
	methods:{
		// 执行c组件的触发的函数
		getCData(val){
			console.log(val);
		}
	}
    };

    new Vue({
        el: "#app",
        data() {
            return {

            }
        },
        components: {
            App
        },
        template: `<App />`
    });
    </script>
</body>

</html>
```

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200328153842324.png" alt="image-20200328153842324" style="zoom:50%;" />

### 中央事件总线（非父子组件间通信）（创建公共的类）

`$on`绑定自定义事件，`$emit`触发自定义事件

`$on`和`$emit`绑定同一个实例化对象

解决兄弟组件之间的传值

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title></title>
</head>

<body>
    <div id="app"></div>
    <script src="https://cdn.bootcss.com/vue/2.5.17-beta.0/vue.min.js"></script>
    <script type="text/javascript">
   /*
    上面两种方式处理的都是父子组件之间的数据传递，而如果两个组件不是父子关系呢？这种情况下可以使用中央事件总线的方式。新建一个Vue事件bus对象，然后通过bus.$emit触发事件，bus.$on监听触发的事件。
   */
      // 中央事件总线
      var bus = new Vue();
   
      Vue.component('brother2', {
        data() {
            return {
                msg:"hello brother1"
            }
        },
        template: `
				<div>
                                              <p>我是老大</p>
					<input type="text" v-model = 'msg' @input = 'passData(msg)' />
				</div>
			`,
        methods: {
           passData(val){
            // //触发全局事件globalEvent
            bus.$emit('globalEvent',val)
           }
        }
    });

    Vue.component('brother1', {
        data() {
            return {
                msg:"hello brother1",
                brother2Msg:''
            }
        },
        template: `
				<div>
					<p>我是老二</p>
					<p>老大传递过来的数据:{{brother2Msg}}</p>
				</div>
			`,
        
           mounted(){
                // 绑定全局事件globalEvent事件，
               bus.$on('globalEvent',(val)=>{
                    bus.brother2Msg = val;
               })
           }
    });
    var App = {
        data() {
            return {
                msg: '我是父组件的内容',
                messagec:'hello c'
            }
        },
        methods: {
          
        },
        template: `<div>
				<brother1></brother1>
                  <brother2></brother2>


			</div>`,
	methods:{
		// 执行c组件的触发的函数
		getCData(val){
			console.log(val);
		}
	}
    }

    new Vue({
        el: "#app",
        data() {
            return {

            }
        },
        components: {
            App
        },
        template: `<App />`
    });
    </script>
</body>

</html>
```

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200328154341647.png" alt="image-20200328154341647" style="zoom:50%;" />

### provide(传值)和inject（接收）【父组件传值，子组件接收】

父组件中通过provide来提供变量，然后在子组件中通过inject来注入变量。不论子组件有多深，只要调用了inject那么就可以注入provider中的数据。而不是局限于只能从当前父组件的prop属性来获取数据，只要在父组件的生命周期内，子组件都可以调用。

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
</head>
<body>
	<div id="app"></div>
    <script src="https://cdn.bootcss.com/vue/2.5.17-beta.0/vue.min.js"></script>
    <script type="text/javascript">
    	
    	Vue.component('Child',{
    		data(){
    			return {
    				msg:''
    			}
    		},
    		template:`
			<div>我是孩子{{msg}}</div>
    		`,
    		 inject:['for'],
    		 created(){
                 // 拿到传递过来的值
    		 	this.msg = this.for;
    		 }
    	});

    	Vue.component('Parent',{
    		template:`
			<div>
				<p>我是父亲</p>
				<Child />
			</div>
			
    		`
    		
    	});
    	var App = {
    		data(){
    			return {

    			}
    		},
            
    		provide:{
    			for:'他爹'
    		},
    		template:`
			<div>
				<h2>我是入口组件</h2>
				<Parent />
			</div>
    		`
    	}

    	new Vue({
    		el:"#app",
    		template:`<App />`,
    		data(){
    			return {

    			}
    		},
    		components:{
    			App
    		}
    	});
    </script>
	
</body>
</html>
```

### $parent和$children

挂载父组件，在子组件中通过props去接收

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title></title>
</head>

<body>
    <div id="app"></div>
    <script src="https://cdn.bootcss.com/vue/2.5.17-beta.0/vue.min.js"></script>
    <script type="text/javascript">
    

    Vue.component('Child', {
                props: {
                    value: String, //v-model会自动传递一个字段为value的prop属性
                },
                data() {
                    return {
                      	// 将value 的值赋值给  mymessage
                        mymessage: this.value
                    }
                },
                methods: {
                    changeValue() {
                        console.log(this.mymessage);
                        this.$parent.message = this.mymessage; //通过如此调用可以改变父组件的值
                        console.log(this.$parent);
                    }
                },
                template: `
            <div>
                <input type="text" v-model="mymessage" @change="changeValue"> 
            </div>
            `
    })
    Vue.component('Parent',{
      // 点击按钮，将mymessage的值传递给子组件  
        template:` <div >
                    <p>我是父亲组件{{message}}</p>
                    <button @click = "changeChildValue" > test < /button > 
                    <Child ></Child> 
                    </div>
                `,
        methods:{
            changeChildValue(){
                this.$children[0].mymessage = 'hello';
            }
        },

        data(){
            return {
                message:'hello'
            }
        }
    })
    var App = {
            data(){
                return {

                }
            },
            template:`
            <div>
                <h2>我是入口组件</h2>
                <Parent />
            </div>
            `
        }

   var vm = new Vue({
        el:'#app',
        components:{
            App
        },
        template:`
            <App></App>
                `
    })
   console.log(vm);

    </script>
</body>

</html>
```

### vuex流程图

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200328161839735.png" alt="image-20200328161839735" style="zoom:80%;" />

**Vuex原理**

Vuex实现了一个单向数据流，在全局拥有一个State存放数据，当组件要更改State中的数据时，必须通过Mutation进行，Mutation同时提供了订阅者模式供外部插件调用获取State数据的更新。而当所有异步操作(常见于调用后端接口异步获取更新数据)或批量的同步操作需要走Action，但Action也是无法直接修改State的，还是需要通过Mutation来修改State的数据。最后，根据State的变化，渲染到视图上。

**各模块之间的工作流程**

- Vue Components：Vue组件。HTML页面上，负责接收用户操作等交互行为，执行dispatch方法触发对应action进行回应。
- dispatch：操作行为触发方法，是唯一能执行action的方法。
- actions：**操作行为处理模块,由组件中的`$store.dispatch('action 名称', data1)`来触发。然后由commit()来触发mutation的调用 , 间接更新 state**。负责处理Vue Components接收到的所有交互行为。包含同步/异步操作，支持多个同名方法，按照注册的顺序依次触发。向后台API请求的操作就在这个模块中进行，包括触发其他action以及提交mutation的操作。该模块提供了Promise的封装，以支持action的链式触发。
- commit：状态改变提交操作方法。对mutation进行提交，是唯一能执行mutation的方法。
- mutations：**状态改变操作方法，由actions中的`commit('mutation 名称')`来触发**。是Vuex修改state的唯一推荐方法。该方法只能进行同步操作，且方法名只能全局唯一。操作之中会有一些hook暴露出来，以进行state的监控等。
- state：页面状态管理容器对象。集中存储Vue components中data对象的零散数据，全局唯一，以进行统一的状态管理。页面显示所需的数据从该对象中进行读取，利用Vue的细粒度数据响应机制来进行高效的状态更新。
- getters：state对象读取方法。图中没有单独列出该模块，应该被包含在了render中，Vue Components通过该方法读取全局state对象。

**Vuex与localStorage**

 	vuex 是 vue 的状态管理器，存储的数据是响应式的。但是并不会保存起来，刷新之后就回到了初始状态，   	**具体做法应该在vuex里数据改变的时候把数据拷贝一份保存到localStorage里面，刷新之后，如果		localStorage里有保存的数据，取出来再替换store里的state。**

```
let defaultCity = "上海"
try {   // 用户关闭了本地存储功能，此时在外层加个try...catch
  if (!defaultCity){
    defaultCity = JSON.parse(window.localStorage.getItem('defaultCity'))
  }
}catch(e){}
export default new Vuex.Store({
  state: {
    city: defaultCity
  },
  mutations: {
    changeCity(state, city) {
      state.city = city
      try {
      window.localStorage.setItem('defaultCity', JSON.stringify(state.city));
      // 数据改变的时候把数据拷贝一份保存到localStorage里面
      } catch (e) {}
    }
  }
})
复制代码
```

这里需要注意的是：由于vuex里，我们保存的状态，都是数组，而localStorage只支持字符串，所以需要用JSON转换：

```
JSON.stringify(state.subscribeList);   // array -> string
JSON.parse(window.localStorage.getItem("subscribeList"));    // string -> array 
```

## 在vue中获取DOM元素

```javascript
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title></title>
	<script src="./node_modules/vue/dist/vue.min.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
	<div id="app"></div>
	<script type="text/javascript">
		// 组件的挂载
		Vue.component('SubCom', {
			template:
			`
				<div></div>
			`
		});
		var App = {
			template:
			`
				<div class = 'app'>
					<button ref = 'btn'>按钮1</button>
					<button ref = 'btn2'>按钮2</button>
					<!-- 给组件绑定ref -->
					<SubCom ref = 'abc'/>
				</div>b
			`,
			created() {
				<!-- 获取所有的加上有ref属性的集合 -->
				console.log(this.$refs.btn);
			},
			beforeMount:function() {
				<!-- 获取所有的加上有ref属性的集合 -->
				console.log(this.$refs.btn);
			},
			mounted() {
				<!-- 如果给标签蚌寺那个ref = 'xxx' 属性，使用this.$refs.xxx获取原生的js对象 -->
				<!-- ref属性值不能重名 -->
				console.log(this.$refs.btn);
				console.log(this.$refs.btn2);
				
				<!-- 如果是给自定义组件绑定ref属性，那么this.$refs.abc获取的是当前的组件对象 -->
				console.log(this.$refs.abc);
			}
		};
		new Vue({
			el: '#app',
			data() {
				return {
					
				}
			},
			template: `<App></App>`,
			components: {
				App
			}
		});
	</script>
</body>
</html>
```

## 给DOM元素添加事件的特殊情况

使用focus()方法，获取焦点事件

```javascript
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title></title>
	<script src="./node_modules/vue/dist/vue.min.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
	<div id="app"></div>
	<script type="text/javascript">
		var App = {
			data() {
				return {
					isShow: false
				}
			},
			template:
			`
				<div class = 'app'>
					<input type = 'text' v-show = 'isShow' ref = 'input'/>
				</div>
			`,
			mounted() {
				this.isShow = true;
				<!-- 能获取到input框，但是不能使用focus()方法 -->
				console.log(this.$refs.input);
				<!-- 在Dom更新 -->
				<!-- $nextTick()方法，在DOM更新循环之后执行回调函数，再修改数据之后可以使用此方法，在回调函数中获取到更新之后的数据 -->
				<!-- this.$ref.input.focus(); -->
				this.$nextTick(function() {	
					console.log(this);
					<!-- 窗体加载的时候input框默认触发焦点事件 -->
					this.$refs.input.focus();
				});
				
			}
		};
		new Vue({
			el: '#app',
			data() {
				return {
					
				}
			},
			template: `<App></App>`,
			components: {
				App
			}
		});
	</script>
</body>
</html>
```

## 生命周期的图示

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200329125846436.png" alt="image-20200329125846436" style="zoom:80%;" />



## 核心插件

### 路由

#### 路由的实现

- 传统开发方式url改变后，立刻发生请求响应整个页面，有可能资源过多，传统开发会让页面出现白屏

- 前端路由的原理

  ```javascript
  <!DOCTYPE html>
  <html lang="zh">
  <head>
  	<meta charset="UTF-8">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<meta http-equiv="X-UA-Compatible" content="ie=edge">
  	<title></title>
  </head>
  <body>
  	<a href="#/login">登录</a>
  	<a href="#/register">注册</a>
  	<div id="app"></div>
  	<script type="text/javascript">
  		var oDiv = document.getElementById('app');
  		
  		// onhashchange方法,哈希值改变后调用的方法
  		// a标签中href属性的值就是哈希值
  		window.onhashchange = function(){
  			// 访问到用户点击的哈希值
  			console.log(location.hash);
  			// 根据哈希值来做相对应的处理
  			switch (location.hash){
  				case '#/login':
  					oDiv.innerHTML = '<h2>我是登录页面</h2>'
  					break;
  				case '#/register':
  					oDiv.innerHTML = '<h2>我是注册页面</h2>'	
  					break;
  				default:
  					break;
  			}
  		}
  	</script>
  </body>
  </html>
  ```

- SPA（Single Page Application） 单页面应用

  - 锚点值改变
    - 锚点值改变后，不会立刻发送请求，而是在某个合适的实际，发起的ajax请求页面的局部渲染
    - 优点：页面不会立刻跳转，用户体验好
    - Vue，Angular，React这些框架都是做单页面应用

#### Vue-Router的基本使用

下载packag.json配置文件

```javascript
npm init --yes
```

下载vue包

```javascript
npm install vue --save
```

下载vue-router包

```javascript
npm install vue-router -S
```

使用：

1. 引包（两个全局组件 router-link to属性   router-view（匹配路由组件的出口））
2. 创建实例化VueRouter对象
3. 匹配路由规则
4. 挂载new  Vue()实例化对象中
   1. 给vue实例化对象挂在了两个对象 this.$router()，它就是VueRouter
   2. this.route()获取的是配置路由信息的对象
5. 命名路由
   1. 绑定自定义属性 ：to = “{name：‘路由的名字’}”
6. 路由的参数
   1. path：‘/user/id’
      1. to：“{name：‘user’，params：{id: 1}}”
   2. path：‘/user’
      1. to：“{name：‘user’，query：{userId: 1}}”
7. 嵌套路由（应用于  子路由是不同的页面结构）
   1. /home/music   ===>   /home/movie
      1. 一个router-view中嵌套另外一个router-view

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 1引入vue模块-->
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<!-- 2 引入vue-router模块 -->
		<!-- 引入vue-router模块后 会抛出两个全局组件 router-link 和 router-view -->
		<!-- router-link 相当于a标签 ，router-link中的to属性相当于a标签的href属性 -->
		<!-- router-view 路由匹配组件的出口 -->
		<script src="./node_modules/vue-router/dist/vue-router.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// 创建使用vue-router
			// 3 让Vue使用VueRouter创建
			Vue.use(VueRouter);

			var Login = {
				template: `
				<div>我是登陆页面</div>
			`
			};
			var Register = {
				template: `
				<div>我是注册页面</div>
			`
			};
			<!-- // 4 创建router对象 -->
			var router = new VueRouter({
				<!-- //5 配置路由对象 -->
				routes: [
					<!-- // 路由匹配的规则 -->
					<!-- 当路径为login时，自动匹配Login组件，然后加载组件中的内容 -->
					{
						path: "/login",
						component: Login
					},
					{
						path: "/register",
						component: Register
					},
				]
			});


			<!-- // 声明组件 -->
			var App = {
				template: `
					<div>
						<!-- <a href="">登录页面</a> -->
						<router-link to="/login">登录页面</router-link>
						<router-link to="/register">注册页面</router-link>
						<!-- 路由匹配组件的出口 -->
						<router-view></router-view>
					</div>
			`
			}
			new Vue({
				el: '#app',
				data() {
					return {

					}
				},
				components: {
					App
				},
				<!-- 将 router 路由交给Vue实例化对象管理-->
				router,	
				template: `<App></App>`
			})
		</script>
	</body>
</html>
```

#### 命名路由

绑定to属性，匹配路由对象(通过定义的name来使用)

routes中的path属于动态路由参数，以冒号开头

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 1引入vue模块-->
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<!-- 2 引入vue-router模块 -->
		<!-- 引入vue-router模块后 会抛出两个全局组件 router-link 和 router-view -->
		<!-- router-link 相当于a标签 ，router-link中的to属性相当于a标签的href属性 -->
		<!-- router-view 路由匹配组件的出口 -->
		<script src="./node_modules/vue-router/dist/vue-router.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// 创建使用vue-router
			// 3 让Vue使用VueRouter创建
			Vue.use(VueRouter);

			var Login = {
				template: `
				<div>我是登陆页面</div>
			`
			};
			var Register = {
				template: `
				<div>我是注册页面</div>
			`
			};
			<!-- // 4 创建router对象 -->
			var router = new VueRouter({
				<!-- //5 配置路由对象 -->
				routes: [
					<!-- // 路由匹配的规则 -->
					<!-- 当路径为login时，自动匹配Login组件，然后加载组件中的内容 -->
					{
						path: "/login",
						name: "login",	<!-- 给当前路由命名 -->
						component: Login
					},
					{
						path: "/register",
						name: "register",
						component: Register
					},
				]
			});


			<!-- // 声明组件 -->
			var App = {
				template: `
					<div>
						<!-- <a href="">登录页面</a> -->
						<!-- <router-link to="/login">登录页面</router-link> -->
						
						<!-- 通过路由的命名来使用 -->
						<router-link :to="{name: 'login'}">登录页面</router-link>
						
						
						<!-- <router-link to="/register">注册页面</router-link> -->
						<router-link :to="{name: 'register'}">登录页面</router-link>
						<!-- 路由匹配组件的出口 -->
						<router-view></router-view>
					</div>
			`
			}
			new Vue({
				el: '#app',
				data() {
					return {

					}
				},
				components: {
					App
				},
				<!-- 将 router 路由交给Vue实例化对象管理-->
				router,	
				template: `<App></App>`
			})
		</script>
	</body>
</html>

```

#### 路由参数

路由范式（规则）：

- xxx.html#/user/1   
  - 动态参数（params）路由
- ooo.html#/user?userId = 1 
  - （ ？）query查询

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 1引入vue模块-->
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<!-- 2 引入vue-router模块 -->
		<!-- 引入vue-router模块后 会抛出两个全局组件 router-link 和 router-view -->
		<!-- router-link 相当于a标签 ，router-link中的to属性相当于a标签的href属性 -->
		<!-- router-view 路由匹配组件的出口 -->
		<script src="./node_modules/vue-router/dist/vue-router.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// 创建使用vue-router
			// 3 让Vue使用VueRouter创建
			Vue.use(VueRouter);

			var userParams = {
				template: `
					<div>我是用户1</div>
				`,
				created() {
					<!--引入vue-router时就会抛出两个对象  -->
					<!-- 这两个对象就挂载到Vue实例化对象 -->
					console.log(this.$router);
					console.log(this.$route);
					<!-- 获取用户点击的id -->
					<!-- 注意通过  :id传递了id参数参能获取到id的值 -->
					console.log(this.$route.params.id);
				}
			};
			var userQuery = {
				template: `
				<div>我是用户2</div>
			`
			};
			<!-- // 4 创建router对象 -->
			var router = new VueRouter({
				<!-- //5 配置路由对象 -->
				routes: [
					<!-- // 路由匹配的规则 -->
					<!-- 当路径为login时，自动匹配Login组件，然后加载组件中的内容 -->
					{
						path: "/user/:id",
						<!-- params动态参数 -->
						name: "userP",	<!-- 给当前路由命名 -->
						component: userParams
					},
					{
						path: "/user",
						<!-- query 查询 -->
						name: "userQ",
						component: userQuery
					},
				]
			});


			<!-- // 声明组件 -->
			var App = {
				template: `
					<div>
						<!-- params:{key,value} -->
						<!-- 动态路由路径 -->
						<router-link :to="{name: 'userP', params:{id:1}}">用户1</router-link>
						<router-link :to="{name: 'userQ', params:{userId:2}}">用户2</router-link>
						<!-- 路由匹配组件的出口 -->
						<router-view></router-view>
					</div>
			`
			}
			new Vue({
				el: '#app',
				data() {
					return {

					}
				},
				components: {
					App
				},
				<!-- 将 router 路由交给Vue实例化对象管理-->
				router,	
				template: `<App></App>`
			})
		</script>
	</body>
</html>

```

#### 嵌套路由

菜单栏的动态切换，标题栏一样，通过小组件来实现页面的动态切换

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 1引入vue模块-->
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<!-- 2 引入vue-router模块 -->
		<!-- 引入vue-router模块后 会抛出两个全局组件 router-link 和 router-view -->
		<!-- router-link 相当于a标签 ，router-link中的to属性相当于a标签的href属性 -->
		<!-- router-view 路由匹配组件的出口 -->
		<script src="./node_modules/vue-router/dist/vue-router.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// 创建使用vue-router
			// 3 让Vue使用VueRouter创建
			Vue.use(VueRouter);
			<!-- 内层小组件 -->
			var Song = {
				template: 
				`
					<div>歌曲列表</div>
				`
			};
			var Movie = {
				template: 
				`
					<div>电影列表</div>
				`
			};
			
			<!-- // 外层大组件 -->
			<!-- 注意：每一个组件模板都是一个大的整体，需要在一个盒子里面 -->
			var Home = {
				template: `
					<div>首页
						<br />
						<!-- 动态路由路径 -->
						<router-link to = '/home/song'>歌曲</router-link>
						<router-link to = '/home/movie'>电影</router-link>
						<!-- 路由匹配组件的出口 -->
						<router-view></router-view>
					</div>
				`
			};
			
			<!-- // 4 创建router对象 -->
			var router = new VueRouter({
				<!-- //5 配置路由对象 -->
				routes: [
					<!-- // 路由匹配的规则 -->
					<!-- 当路径为login时，自动匹配Login组件，然后加载组件中的内容 -->
					{
						path: "/home",
						<!-- params动态参数 -->
						name: "home",	<!-- 给当前路由命名 -->
						component: Home,
						<!-- 匹配多层目录下面的子目录 -->
						children: [
							{
								path: "song",
								<!-- params动态参数 -->
								component: Song
							},
							{
								path: "movie",
								<!-- params动态参数 -->
								component: Movie
							},
						]
					}
				]
			});


			<!-- // 声明组件 -->
			var App = {
				template: `
					<div>
						<!-- params:{key,value} -->
						<!-- 动态路由路径 -->
						<router-link :to="{name: 'home'}">首页</router-link>
						<!-- 路由匹配组件的出口 -->
						<router-view></router-view>
					</div>
			`
			}
			new Vue({
				el: '#app',
				data() {
					return {

					}
				},
				components: {
					App
				},
				<!-- 将 router 路由交给Vue实例化对象管理-->
				router,	
				template: `<App></App>`
			})
		</script>
	</body>
</html>

```

#### 动态路由匹配

```javascript
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title></title>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script src="./node_modules/vue-router/dist/vue-router.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
	<div id="app"></div>
	<script type="text/javascript">
		// 当前使用路由参数,列入/timeline/fronted导航到/timeline/backed,原来的组件实例会被复用,
		// 因为两个路由都渲染同个组件,比起销毁在创建,复用则显得更高效,不过这也意味着组件的生命周期
		// 不会再被调用
		
		var ComDesc = {
			data() {
				return {
					msg: ''
				}
			},
			template:
			`
				<div>我是{{ msg }}</div>
			`,
			created() {
				<!-- created方法只会走一次 -->
				<!-- created可以发Ajax请求 -->
				this.msg = '前端';
			},
			<!-- watch在当前组件内部监听路由信息的变化 -->
			watch: {
				'$route'(to,from) {
					console.log(to);	<!-- to就是一个routes对象 -->
					console.log(from);
					<!-- 发送ajax请求，获取到对应的参数 -->
					this.msg = to.params.id;
				}
			}
		};
		var Timeline = {
			template:
			`
				<div id = 'timeline'>
					<!-- 动态路由路径 -->
					<router-link :to = "{name: 'comDesc',params:{id: 'frontend'}}">前端</router-link>
					<router-link :to = "{name: 'comDesc',params:{id: 'backed'}}">后端</router-link>
					<!-- 路由匹配组件的出口 -->
					<router-view></router-view>
				</div>
			`
		};
		var Pins = {
			template:
			`
				<div>
					<h2>沸点</h2>
				</div>
			`
		};
		<!-- // 创建路由对象 -->
		var router = new VueRouter({
			<!-- mode: 'history',	哈希模式，页面跳转时路由不会出现#  -->
			routes:[
				{
					path: '/timeline',
					component: Timeline,
					children: [
						{
							name: 'comDesc',
							<!-- 动态路由的参数  以:开头 -->
							path: '/timeline/:id',
							component: ComDesc
						}
					]
				},
				{
					path: '/pins',
					component: Pins
				}
			]
		});
		<!-- // 实例化app组件 -->
		var App = {
			template:
			`
				<div>
					<!-- 动态路由路径 -->
					<router-link to = '/timeline'>首页</router-link>
					<router-link to = '/pins'>沸点</router-link>
					<!-- 路由匹配组件的出口 -->
					<router-view></router-view>
				</div>
			`
		}
		<!-- // 实例化对象 -->
		new Vue({
			el: '#app',
			router,
			template: `<App></App>`,
			<!-- 挂载组件 -->
			components: {
				App
			}
		})
	</script>
</body>
</html>
```

#### 路由元信息（meta的使用及权限控制）

```javascript
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title></title>
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<script src="./node_modules/vue-router/dist/vue-router.js" type="text/javascript" charset="utf-8"></script>
</head>
<body>
	<div id="app">
		<router-link to = '/home'>首页</router-link>
		<router-link to = '/blog'>我的博客</router-link>
		<router-link to = '/login'>登录</router-link>
		<a href="javascript:void(0)">退出</a>
		<!-- 每个路由组件都渲染到router-view里面了 -->
		<router-view></router-view>
	</div>
	<script type="text/javascript">
		Vue.use(VueRouter);
		var Home = {
			template: 
			`
				<div>首页</div>
			`
		};
		var Blog = {
			template: 
			`
				<div>我的博客</div>
			`
		};
		var Login = {
			data() {
				return {
					name: '',
					pwd: ''
				}
			},
			template: 
			`
				<div>
					<input type="text" v-model="name"/>
					<input type="password" v-model="pwd"/>
					<input type="button" value="登录" @click = 'loginHandle'/>
				</div>
			`,
			methods: {
				loginHandle() {
					<!-- 登录 -->
					<!-- 将用户名 密码保存下来 -->
					localStorage.setItem('user', {name:this.name,pwd:this.pwd});
					<!-- 跳转到博客页面 -->
					<!-- 编程式导航 -->
					this.$router.push({
						name: 'blog'
					})
				}
			}
		};
		<!-- // 创建路由对象 -->
		var router = new VueRouter({
			<!-- mode: 'history',	哈希模式，页面跳转时路由不会出现#  -->
			routes:[
				{
					path: '/',
					redirect: '/home'
				},
				{
					path: '/home',
					component: Home
				},
				{
					path: '/blog',
					name: 'blog',
					component: Blog,
					<!-- meta给未来的路由做权限控制 -->
					meta: {
						<!-- 证明用户访问该组件的时候需要登录 -->
						auth: true
					}
				},
				{
					path: '/login',
					component: Login
				}
			]
		});

		<!-- 全局路由匹配 -->
		<!-- beforeEach会监测路由 -->
		router.beforeEach((to, from, next) => {
			console.log(to);
			console.log(from);
			if(to.meta.auth) {	<!-- true -->
				if (localStorage.getItem('user')) {
					<!-- 如果localStorage有值则证明用户登录完成了 -->
					next();
				}else{
					<!-- 用户需要登录 -->
					next({
						path: '/login'
					});
				}
				
			} else {
				<!-- false  直接放行 -->
				<!-- 如果不调用 next() 方法会卡主页面-->
				next();
			}
		});
		<!-- // 实例化对象 -->
		new Vue({
			el: '#app',
			router,		<!-- 挂载路由 -->
		})
	</script>
</body>
</html>
```

### Vuex

### Vue服务端渲染

## Axios

Axios是一个基于promise的HTTP库，可以在浏览器和node.js中使用。

作用：

- 从浏览器中创建`XMLHttpRequests`
- 从node.js创建`http`请求
- 支持`Promise`API
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防御`XSRF`攻击

> 参考文档链接：https://www.kancloud.cn/yunye/axios/234845

### 使用

安装

使用npm：

```javavascript
npm install axios
```

使用bower:

```javascript
bower install axios
```

使用cdn：

```javascript
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

### axios的基本使用

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 引包vue -->
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<!-- 引包axios -->
		<script src="./node_modules/axios/dist/axios.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// console.log(axios);
			var App = {
				template:
				`
					<div>
						<button @click = 'sendAjax'>发请求</button>
					</div>
				`,
				methods: {
					sendAjax(){
						this.$axios.get('http://127.0.0.1:8888/')
						.then(res => {
							<!-- 拿到statusText: "OK" -->
							console.log(res.data.msg);	<!-- 打印输出ok -->
						})
						.catch(err => {
							console.log(err);
						}) 
					}
				}
			};
				Vue.prototype.$axios = axios;
			new Vue({
				el: '#app',
				data() {
					return {

					}
				},
				template: `<App></App>`,
				components: {
					App
				}
			});
		</script>
	</body>
</html>
```

### 处理并发请求

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<!-- 引包vue -->
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<!-- 引包axios -->
		<script src="./node_modules/axios/dist/axios.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<div id="app"></div>
		<script type="text/javascript">
			// console.log(axios);
			var App = {
				data() {
					return {
						res1: '',
						res2: ''
					}
				},
				template: `
					<div>
						响应1: {{ res1 }},
						响应2: {{ res2 }},
						<button @click = 'sendAjax'>并发请求</button>
					</div>
				`,
				methods: {
					sendAjax() {
						<!-- 请求1 get: /-->
						<!-- 请求2 post :/add -->
						<!-- 配置 -->
						this.$axios.defaults.baseURL = `http://127.0.0.1:8888/`;
						<!-- 发请求 -->
						var r1 = this.$axios.get('');
						var r2 = this.$axios.post('add','a = 1');
						this.$axios.all([r1, r2])
						.then(this.$axios.spread((res1,res2) => {
							<!-- 请求全部成功 -->
							this.res1 = res1.data;
							this.res2 = res2.data;
						}))
						.catch(err => {
							<!-- 有一个失败就失败了 -->
							console.log(err);
						})
					}
				}
			};
			Vue.prototype.$axios = axios;
			new Vue({
				el: '#app',
				data() {
					return {

					}
				},
				template: `<App></App>`,
				components: {
					App
				}
			});
		</script>
	</body>
</html>
```

### 请求配置

这些是创建请求时可以用的配置选项。只有`url`是必需的。如果没有指定`method`，请求将使用替代`get`方法。

```javascript
{
  // `url` 是用于请求的服务器 URL
  url: '/user',

  // `method` 是创建请求时使用的方法
  method: 'get', // 默认是 get

  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: 'https://some-domain.com/api/',

  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 只能用在 'PUT', 'POST' 和 'PATCH' 这几个请求方法
  // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
  transformRequest: [function (data) {
    // 对 data 进行任意转换处理

    return data;
  }],

  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对 data 进行任意转换处理

    return data;
  }],

  // `headers` 是即将被发送的自定义请求头
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // `params` 是即将与请求一起发送的 URL 参数
  // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
  params: {
    ID: 12345
  },

  // `paramsSerializer` 是一个负责 `params` 序列化的函数
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // `data` 是作为请求主体被发送的数据
  // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
  // 在没有设置 `transformRequest` 时，必须是以下类型之一：
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属：FormData, File, Blob
  // - Node 专属： Stream
  data: {
    firstName: 'Fred'
  },

  // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
  // 如果请求话费了超过 `timeout` 的时间，请求将被中断
  timeout: 1000,

  // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // 默认的

  // `adapter` 允许自定义处理请求，以使测试更轻松
  // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
  adapter: function (config) {
    /* ... */
  },

  // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
  // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

  // `responseType` 表示服务器响应的数据类型，可以是 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
  responseType: 'json', // 默认的

  // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
  xsrfCookieName: 'XSRF-TOKEN', // default

  // `xsrfHeaderName` 是承载 xsrf token 的值的 HTTP 头的名称
  xsrfHeaderName: 'X-XSRF-TOKEN', // 默认的

  // `onUploadProgress` 允许为上传处理进度事件
  onUploadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },

  // `onDownloadProgress` 允许为下载处理进度事件
  onDownloadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },

  // `maxContentLength` 定义允许的响应内容的最大尺寸
  maxContentLength: 2000,

  // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
  validateStatus: function (status) {
    return status >= 200 && status < 300; // 默认的
  },

  // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
  // 如果设置为0，将不会 follow 任何重定向
  maxRedirects: 5, // 默认的

  // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
  // `keepAlive` 默认没有启用
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // 'proxy' 定义代理服务器的主机名称和端口
  // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
  // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
  proxy: {
    host: '127.0.0.1',
    port: 9000,
    auth: : {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // `cancelToken` 指定用于取消请求的 cancel token
  // （查看后面的 Cancellation 这节了解更多）
  cancelToken: new CancelToken(function (cancel) {
  })
}
```

### 请求拦截器interceptors

在请求或响应被`then`或`catch`处理前拦截它们。

```
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 对响应错误做点什么
    return Promise.reject(error);
  });
```

如果你想在以后可移除拦截器，可以这样：

```
var myInterceptor = axios.interceptors.request.use(function () {/*...*/});
axios.interceptors.request.eject(myInterceptor);
```

可以为自定义axios实例添加拦截器

```
var instance = axios.create();
instance.interceptors.request.use(function () {/*...*/});
```

#### 错误处理

```
axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // 请求已发出，但服务器响应的状态码不在 2xx 范围内
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else {
      // Something happened in setting up the request that triggered an Error
      console.log('Error', error.message);
    }
    console.log(error.config);
  });
```

可以使用`validateStatus`配置选项定义一个自定义HTTP状态码的错误范围。

```
axios.get('/user/12345', {
  validateStatus: function (status) {
    return status < 500; // 状态码在大于或等于500时才会 reject
  }
})
```

#### 取消

使用*取消令牌*取消请求

> Axios的取消令牌API基于[cancelable promises提议](https://github.com/tc39/proposal-cancelable-promises)，它还处于第一阶段。

可以使用`CancelToken.source`工厂方法创建cancel token，像这样：

```
var CancelToken = axios.CancelToken;
var source = CancelToken.source();

axios.get('/user/12345', {
  cancelToken: source.token
}).catch(function(thrown) {
  if (axios.isCancel(thrown)) {
    console.log('Request canceled', thrown.message);
  } else {
    // 处理错误
  }
});

// 取消请求（message 参数是可选的）
source.cancel('Operation canceled by the user.');
```

还可以通过传递一个executor函数到`CancelToken`的构造函数来创建取消令牌：

```
var CancelToken = axios.CancelToken;
var cancel;

axios.get('/user/12345', {
  cancelToken: new CancelToken(function executor(c) {
    // executor 函数接收一个 cancel 函数作为参数
    cancel = c;
  })
});

// 取消请求
cancel();
```

注意：可以使用同一个cancel token取消多个请求

```javascript
<!DOCTYPE html>
<html lang="zh">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<meta http-equiv="X-UA-Compatible" content="ie=edge">
		<title></title>
		<style type="text/css">
			.spinner {
				margin: 100px auto;
				width: 50px;
				height: 60px;
				text-align: center;
				font-size: 10px;
			}

			.spinner>div {
				background-color: #67CF22;
				height: 100%;
				width: 6px;
				display: inline-block;
				-webkit-animation: stretchdelay 1.2s infinite ease-in-out;
				animation: stretchdelay 1.2s infinite ease-in-out;
			}

			.spinner .rect2 {
				-webkit-animation-delay: -1.1s;
				animation-delay: -1.1s;
			}

			.spinner .rect3 {
				-webkit-animation-delay: -1.0s;
				animation-delay: -1.0s;
			}

			.spinner .rect4 {
				-webkit-animation-delay: -0.9s;
				animation-delay: -0.9s;
			}

			.spinner .rect5 {
				-webkit-animation-delay: -0.8s;
				animation-delay: -0.8s;
			}

			@-webkit-keyframes stretchdelay {

				0%,
				40%,
				100% {
					-webkit-transform: scaleY(0.4)
				}

				20% {
					-webkit-transform: scaleY(1.0)
				}
			}

			@keyframes stretchdelay {

				0%,
				40%,
				100% {
					transform: scaleY(0.4);
					-webkit-transform: scaleY(0.4);
				}

				20% {
					transform: scaleY(1.0);
					-webkit-transform: scaleY(1.0);
				}
			}
		</style>
		<!-- 引包vue -->
		<script src="./node_modules/vue/dist/vue.js" type="text/javascript" charset="utf-8"></script>
		<!-- 引包axios -->
		<script src="./node_modules/axios/dist/axios.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>

		<div id="app"></div>
		<script type="text/javascript">
			// console.log(axios);
			var App = {
				data() {
					return {
						isShow: false
					}
				},
				template: `
					<div>
						<div class="spinner" v-show = 'isShow'>
							<div class="rect1"></div>
							<div class="rect2"></div>
							<div class="rect3"></div>
							<div class="rect4"></div>
							<div class="rect5"></div>
						</div>	
						<button @click = 'sendAjax'>发请求</button>
					</div>
				`,
				methods: {
					sendAjax() {
						<!-- 模拟类似cookie的机制 -->
						<!-- 添加请求拦截器 -->
						this.$axios.interceptors.request.use((config) => {
							console.log(config);
							var token = localStorage.setItem('token');
							if (token) {
								config.headers['token'] = token;
							}
							this.isShow = true;
							return config;
						}, function(err) {
							return Promise.reject(err);
						});

						<!-- // 添加响应拦截器 -->
						this.$axios.interceptors.response.use(response => {
							<!-- // 对响应数据做点什么 -->
							console.log(response);
							this.isShow = false;
							return response;
						}, function(error) {
							<!-- // 对响应错误做点什么 -->
							return Promise.reject(error);
						});

						this.$axios.get('http://127.0.0.1:8888')
							.then(res => {
								console.log(res);
							})
							.catch(err => {
								console.log(err);
							})
					}
				}
			};
			Vue.prototype.$axios = axios;
			new Vue({
				el: '#app',
				data() {
					return {

					}
				},
				template: `<App></App>`,
				components: {
					App
				}
			});
		</script>
	</body>
</html>

```



# 认识webpack

能完成所有常用的功能：

- 压缩
- 打包
- 多种文件的编译(比如less文件编译成css文件)
- 脚手架
- 生成

安装：

> npm i webpack-cli -g

### 基本使用

index.js

```javascript
//jquery存放在本地
import $ from './libs/jquery';	// 引入jquery
//jquery存放在node_modules
import $ from 'jquery';

$(function(){
    alert(a);
})
```

webpack.config.js

```javascript
model.exports{
    //模式
    mode: 'development',
        
    //入口
    entry: './src/js/index.js',
    
    //输出
    output: {
    	path: path.resolve(__dirname,'build'),
    	filename: 'build.js'
    }
}
```



> webpack是一个现代JavaScript应用程序的静态模块打包器。当 webpack 处理应用程序时，它会递归地构建一个*依赖关系图(dependency graph)*，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 *bundle*。
>
> ![image-20200331142837324](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200331142837324.png)

### 历史介绍

- 2009年初，commonjs规范还未出来，此时前端开发人员编写的代码都是非模块化的，
  - 那个时候开发人员经常需要十分留意文件加载顺序所带来的依赖问题
- 与此同时 nodejs开启了js全栈大门，而requirejs在国外也带动着前端逐步实现模块化
  - 同时国内seajs也进行了大力推广
  - AMD 规范 ，具体实现是requirejs define('模块id',[模块依赖1,模块依赖2],function(){  return ;}) , ajax请求文件并加载
  - Commonjs || CMD 规范seajs 淘宝玉伯
    - commonjs和cmd非常相似的
      - cmd  require/module.exports
    - commonjs是js在后端语言的规范: 模块、文件操作、操作系统底层
    - CMD 仅仅是模块定义
  - UMD 通用模块定义，一种既能兼容amd也能兼容commonjs 也能兼容浏览器环境运行的万能代码
- npm/bower集中包管理的方式备受青睐，12年browserify/webpack诞生
  - npm 是可以下载前后端的js代码475000个包
  - bower 只能下载前端的js代码,bower 在下载bootstrap的时候会自动的下载jquery
  - browserify 解决让require可以运行在浏览器，分析require的关系，组装代码
  - webpack 打包工具，占市场主流

```javascript
(function (root, factory) {  
    if (typeof exports === 'object') { 
        module.exports = factory();  //commonjs环境下能拿到返回值
    } else if (typeof define === 'function' ) {  
        define(factory);   //define(function(){return 'a'})  AMD
    } else {  
        window.eventUtil = factory();  
    }  
})(this, function() {  //this相当于传的root
    // module  返回给factory
    return {  
        //具体模块代码
        addEvent: function(el, type, handle) {  
            //...  
        },  
        removeEvent: function(el, type, handle) {  
              
        },  
    };  
}); 
```

手动实现vue-cli脚手架工具，同时也学习webpack的使用

### 模块实现

#### 1.下载webpack为项目开发依赖

``` npm install webpack@3.12.0 -D```

安装全局webpack：

```javascript
npm install webpack -g
```

####   2.创建main.js作为项目的入口文件

```javascript
// 整个程序的入口文件

import Vue from './vue.js'
import App from './App.js'
// 模块整体加载
// import {num,num2,add} from './App.js'

// console.log(num);
// console.log(num2);
// add(3,5);

// import * as object from './App.js'
// console.log(object);
// console.log(object.num);
// console.log(object.num2);
// add(3,5);
new Vue({
	el:'#app',
	components:{
		App
	},
	template:`<App />`
});
```



#### 3.创建一个App.js

```javascript
var App = {
	template:`
		<div>
			我是一个入口组件
		</div>
	`
};
//1. 声明并导出
export var num = 2; //作为一整个对象key导出

//2. 声明再导出
var  num2 = 4;
export {num2};
//3.抛出一个函数
export function add(x,y) {
	return console.log(x+y);
}
//4.抛出一个对象
export default App;
```

####  4.在package.json文件中配置如下：

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401165356620.png" alt="image-20200401165356620" style="zoom:50%;" />

```javascript
{
  "name": "29_module",
  "version": "1.0.0",
  "description": "",
  "main": "main.js",
  "scripts": {
    "build": "webpack ./main.js ./build.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "webpack": "^3.12.0"
  }
}

```

#### 5.新建一个index.html，script脚本引入打包完成的build.js如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
</head>
<body>
	<div id="app"></div>
	<script type="text/javascript" src="./build.js"></script>
	
</body>
</html>
```

### webpack打包后文件的运行方式

1. 直接运行build.js文件

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401165720742.png" alt="image-20200401165720742" style="zoom:50%;" />

2. 配置build文件，然后通过run命令来运行打包后的build文件

   <img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401165932667.png" alt="image-20200401165932667" style="zoom:80%;" />

   <img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401170013894.png" alt="image-20200401170013894" style="zoom:80%;" />

   3.上面那种方法也可以通过webpack直接运行

   ![image-20200401182302745](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401182302745.png)

### webpack 编译之后的build.js文件解读

打包后的每个文件都会有一个解析函数

```javascript
// 模块化文件
/******/
(function(modules) { // webpackBootstrap
	/******/ // The module cache
	/******/
	var installedModules = {};
	/******/
	/******/ // The require function
	/******/
	function __webpack_require__(moduleId) {
		/******/
		/******/ // Check if module is in cache
		/******/
		if (installedModules[moduleId]) {
			/******/
			return installedModules[moduleId].exports;
			/******/
		}
		/******/ // Create a new module (and put it into the cache)
		/******/
		var module = installedModules[moduleId] = {
			/******/
			i: moduleId,
			/******/
			l: false,
			/******/
			exports: {}
			/******/
		};
		/******/
		/******/ // Execute the module function
		/******/
		modules[moduleId].call(module.exports, module, module.exports, __webpack_require__);
		/******/
		/******/ // Flag the module as loaded
		/******/
		module.l = true;
		/******/
		/******/ // Return the exports of the module
		/******/
		return module.exports;
		/******/
	}
	/******/
	/******/
	/******/ // expose the modules object (__webpack_modules__)
	/******/
	__webpack_require__.m = modules;
	/******/
	/******/ // expose the module cache
	/******/
	__webpack_require__.c = installedModules;
	/******/
	/******/ // define getter function for harmony exports
	/******/
	__webpack_require__.d = function(exports, name, getter) {
		/******/
		if (!__webpack_require__.o(exports, name)) {
			/******/
			Object.defineProperty(exports, name, {
				enumerable: true,
				get: getter
			});
			/******/
		}
		/******/
	};
	/******/
	/******/ // define __esModule on exports
	/******/
	__webpack_require__.r = function(exports) {
		/******/
		if (typeof Symbol !== 'undefined' && Symbol.toStringTag) {
			/******/
			Object.defineProperty(exports, Symbol.toStringTag, {
				value: 'Module'
			});
			/******/
		}
		/******/
		Object.defineProperty(exports, '__esModule', {
			value: true
		});
		/******/
	};
	/******/
	/******/ // create a fake namespace object
	/******/ // mode & 1: value is a module id, require it
	/******/ // mode & 2: merge all properties of value into the ns
	/******/ // mode & 4: return value when already ns object
	/******/ // mode & 8|1: behave like require
	/******/
	__webpack_require__.t = function(value, mode) {
		/******/
		if (mode & 1) value = __webpack_require__(value);
		/******/
		if (mode & 8) return value;
		/******/
		if ((mode & 4) && typeof value === 'object' && value && value.__esModule) return value;
		/******/
		var ns = Object.create(null);
		/******/
		__webpack_require__.r(ns);
		/******/
		Object.defineProperty(ns, 'default', {
			enumerable: true,
			value: value
		});
		/******/
		if (mode & 2 && typeof value != 'string')
			for (var key in value) __webpack_require__.d(ns, key, function(key) {
				return value[key];
			}.bind(null, key));
		/******/
		return ns;
		/******/
	};
	/******/
	/******/ // getDefaultExport function for compatibility with non-harmony modules
	/******/
	__webpack_require__.n = function(module) {
		/******/
		var getter = module && module.__esModule ?
			/******/
			function getDefault() {
				return module['default'];
			} :
			/******/
			function getModuleExports() {
				return module;
			};
		/******/
		__webpack_require__.d(getter, 'a', getter);
		/******/
		return getter;
		/******/
	};
	/******/
	/******/ // Object.prototype.hasOwnProperty.call
	/******/
	__webpack_require__.o = function(object, property) {
		return Object.prototype.hasOwnProperty.call(object, property);
	};
	/******/
	/******/ // __webpack_public_path__
	/******/
	__webpack_require__.p = "";
	/******/
	/******/
	/******/ // Load entry module and return exports
	/******/
	return __webpack_require__(__webpack_require__.s = "./main.js");
	/******/
})
/************************************************************************/
/******/
({

	/***/
	"./App.js":
		/*!****************!*\
		  !*** ./App.js ***!
		  \****************/
		/*! exports provided: num1, num2, add, default */
		/***/
		(function(module, __webpack_exports__, __webpack_require__) {

			"use strict";
			eval(
				"__webpack_require__.r(__webpack_exports__);\n/* harmony export (binding) */ __webpack_require__.d(__webpack_exports__, \"num1\", function() { return num1; });\n/* harmony export (binding) */ __webpack_require__.d(__webpack_exports__, \"num2\", function() { return num2; });\n/* harmony export (binding) */ __webpack_require__.d(__webpack_exports__, \"add\", function() { return add; });\n// 声明组件\r\nvar App = {\r\n\ttemplate: \r\n\t`\r\n\t\t<div>我是一个入口组件</div>\r\n\t`\r\n};\r\n\r\n// 声明并导出\r\nvar num1 = 4;\r\n// 声明再导出\r\nvar num2 = 1;\r\n\r\n// 抛出函数\r\nfunction add(x, y){\r\n\treturn x + y;\r\n\tconsole.log(x + y);\r\n}\r\n\r\n// 抛出对象\r\n/* harmony default export */ __webpack_exports__[\"default\"] = (App);\n\n//# sourceURL=webpack:///./App.js?"
			);

			/***/
		}),

	/***/
	"./main.js":
		/*!*****************!*\
		  !*** ./main.js ***!
		  \*****************/
		/*! no exports provided */
		/***/
		(function(module, __webpack_exports__, __webpack_require__) {

			"use strict";
			eval(
				"__webpack_require__.r(__webpack_exports__);\n/* harmony import */ var _node_modules_vue_dist_vue_js__WEBPACK_IMPORTED_MODULE_0__ = __webpack_require__(/*! ./node_modules/vue/dist/vue.js */ \"./node_modules/_vue@2.6.11@vue/dist/vue.js\");\n/* harmony import */ var _node_modules_vue_dist_vue_js__WEBPACK_IMPORTED_MODULE_0___default = /*#__PURE__*/__webpack_require__.n(_node_modules_vue_dist_vue_js__WEBPACK_IMPORTED_MODULE_0__);\n/* harmony import */ var _App_js__WEBPACK_IMPORTED_MODULE_1__ = __webpack_require__(/*! ./App.js */ \"./App.js\");\n// 入口文件\r\n// 从vue.js文件中导入Vue模块\r\n// esModel的模块导入\r\n\r\n// 引入声明的组件\r\n\r\n// 取值\r\n\r\n\r\nconsole.log(_App_js__WEBPACK_IMPORTED_MODULE_1__[\"num1\"],_App_js__WEBPACK_IMPORTED_MODULE_1__[\"num2\"]);\r\nconsole.log(Object(_App_js__WEBPACK_IMPORTED_MODULE_1__[\"add\"])(3, 5));\r\n\r\nnew _node_modules_vue_dist_vue_js__WEBPACK_IMPORTED_MODULE_0___default.a({\r\n\tel: '#app',\r\n\tcomponents: {\r\n\t\tApp: _App_js__WEBPACK_IMPORTED_MODULE_1__[\"default\"]\r\n\t},\r\n\ttemplate: '<App></App>'\r\n});\n\n//# sourceURL=webpack:///./main.js?"
			);

			/***/
		}),

	/***/
	"./node_modules/_vue@2.6.11@vue/dist/vue.js":
		/*!**************************************************!*\
		  !*** ./node_modules/_vue@2.6.11@vue/dist/vue.js ***!
		  \**************************************************/
		/*! no static exports found */
		/***/
		(function(module, exports, __webpack_require__) {

			eval(
				"/* WEBPACK VAR INJECTION */(function(global, setImmediate) {/*!\n * Vue.js v2.6.11\n * (c) 2014-2019 Evan You\n * Released under the MIT License.\n */\n(function (global, factory) {\n   true ? module.exports = factory() :\n  undefined;\n}(this, function () { 'use strict';\n\n  /*  */\n\n  var emptyObject = Object.freeze({});\n\n  // These helpers produce better VM code in JS engines due to their\n  // explicitness and function inlining.\n  function isUndef (v) {\n    return v === undefined || v === null\n  }\n\n  function isDef (v) {\n    return v !== undefined && v !== null\n  }\n\n  function isTrue (v) {\n    return v === true\n  }\n\n  function isFalse (v) {\n    return v === false\n  }\n\n  /**\n   * Check if value is primitive.\n   */\n  function isPrimitive (value) {\n    return (\n      typeof value === 'string' ||\n      typeof value === 'number' ||\n      // $flow-disable-line\n      typeof value === 'symbol' ||\n      typeof value === 'boolean'\n    )\n  }\n\n  /**\n   * Quick object check - this is primarily used to tell\n   * Objects from primitive values when we know the value\n   * is a JSON-compliant type.\n   */\n  function isObject (obj) {\n    return obj !== null && typeof obj === 'object'\n  }\n\n  /**\n   * Get the raw type string of a value, e.g., [object Object].\n   */\n  var _toString = Object.prototype.toString;\n\n  function toRawType (value) {\n    return _toString.call(value).slice(8, -1)\n  }\n\n  /**\n   * Strict object type check. Only returns true\n   * for plain JavaScript objects.\n   */\n  function isPlainObject (obj) {\n    return _toString.call(obj) === '[object Object]'\n  }\n\n  function isRegExp (v) {\n    return _toString.call(v) === '[object RegExp]'\n  }\n\n  /**\n   * Check if val is a valid array index.\n   */\n  function isValidArrayIndex (val) {\n    var n = parseFloat(String(val));\n    return n >= 0 && Math.floor(n) === n && isFinite(val)\n  }\n\n  function isPromise (val) {\n    return (\n      isDef(val) &&\n      typeof val.then === 'function' &&\n      typeof val.catch === 'function'\n    )\n  }\n\n  /**\n   * Convert a value to a string that is actually rendered.\n   */\n  function toString (val) {\n    return val == null\n      ? ''\n      : Array.isArray(val) || (isPlainObject(val) && val.toString === _toString)\n        ? JSON.stringify(val, null, 2)\n        : String(val)\n  }\n\n  /**\n   * Convert an input value to a number for persistence.\n   * If the conversion fails, return original string.\n   */\n  function toNumber (val) {\n    var n = parseFloat(val);\n    return isNaN(n) ? val : n\n  }\n\n  /**\n   * Make a map and return a function for checking if a key\n   * is in that map.\n   */\n  function makeMap (\n    str,\n    expectsLowerCase\n  ) {\n    var map = Object.create(null);\n    var list = str.split(',');\n    for (var i = 0; i < list.length; i++) {\n      map[list[i]] = true;\n    }\n    return expectsLowerCase\n      ? function (val) { return map[val.toLowerCase()]; }\n      : function (val) { return map[val]; }\n  }\n\n  /**\n   * Check if a tag is a built-in tag.\n   */\n  var isBuiltInTag = makeMap('slot,component', true);\n\n  /**\n   * Check if an attribute is a reserved attribute.\n   */\n  var isReservedAttribute = makeMap('key,ref,slot,slot-scope,is');\n\n  /**\n   * Remove an item from an array.\n   */\n  function remove (arr, item) {\n    if (arr.length) {\n      var index = arr.indexOf(item);\n      if (index > -1) {\n        return arr.splice(index, 1)\n      }\n    }\n  }\n\n  /**\n   * Check whether an object has the property.\n   */\n  var hasOwnProperty = Object.prototype.hasOwnProperty;\n  function hasOwn (obj, key) {\n    return hasOwnProperty.call(obj, key)\n  }\n\n  /**\n   * Create a cached version of a pure function.\n   */\n  function cached (fn) {\n    var cache = Object.create(null);\n    return (function cachedFn (str) {\n      var hit = cache[str];\n      return hit || (cache[str] = fn(str))\n    })\n  }\n\n  /**\n   * Camelize a hyphen-delimited string.\n   */\n  var camelizeRE = /-(\\w)/g;\n  var camelize = cached(function (str) {\n    return str.replace(camelizeRE, function (_, c) { return c ? c.toUpperCase() : ''; })\n  });\n\n  /**\n   * Capitalize a string.\n   */\n  var capitalize = cached(function (str) {\n    return str.charAt(0).toUpperCase() + str.slice(1)\n  });\n\n  /**\n   * Hyphenate a camelCase string.\n   */\n  var hyphenateRE = /\\B([A-Z])/g;\n  var hyphenate = cached(function (str) {\n    return str.replace(hyphenateRE, '-$1').toLowerCase()\n  });\n\n  /**\n   * Simple bind polyfill for environments that do not support it,\n   * e.g., PhantomJS 1.x. Technically, we don't need this anymore\n   * since native bind is now performant enough in most browsers.\n   * But removing it would mean breaking code that was able to run in\n   * PhantomJS 1.x, so this must be kept for backward compatibility.\n   */\n\n  /* istanbul ignore next */\n  function polyfillBind (fn, ctx) {\n    function boundFn (a) {\n      var l = arguments.length;\n      return l\n        ? l > 1\n          ? fn.apply(ctx, arguments)\n          : fn.call(ctx, a)\n        : fn.call(ctx)\n    }\n\n    boundFn._length = fn.length;\n    return boundFn\n  }\n\n  function nativeBind (fn, ctx) {\n    return fn.bind(ctx)\n  }\n\n  var bind = Function.prototype.bind\n    ? nativeBind\n    : polyfillBind;\n\n  /**\n   * Convert an Array-like object to a real Array.\n   */\n  function toArray (list, start) {\n    start = start || 0;\n    var i = list.length - start;\n    var ret = new Array(i);\n    while (i--) {\n      ret[i] = list[i + start];\n    }\n    return ret\n  }\n\n  /**\n   * Mix properties into target object.\n   */\n  function extend (to, _from) {\n    for (var key in _from) {\n      to[key] = _from[key];\n    }\n    return to\n  }\n\n  /**\n   * Merge an Array of Objects into a single Object.\n   */\n  function toObject (arr) {\n    var res = {};\n    for (var i = 0; i < arr.length; i++) {\n      if (arr[i]) {\n        extend(res, arr[i]);\n      }\n    }\n    return res\n  }\n\n  /* eslint-disable no-unused-vars */\n\n  /**\n   * Perform no operation.\n   * Stubbing args to make Flow happy without leaving useless transpiled code\n   * with ...rest (https://flow.org/blog/2017/05/07/Strict-Function-Call-Arity/).\n   */\n  function noop (a, b, c) {}\n\n  /**\n   * Always return false.\n   */\n  var no = function (a, b, c) { return false; };\n\n  /* eslint-enable no-unused-vars */\n\n  /**\n   * Return the same value.\n   */\n  var identity = function (_) { return _; };\n\n  /**\n   * Generate a string containing static keys from compiler modules.\n   */\n  function genStaticKeys (modules) {\n    return modules.reduce(function (keys, m) {\n      return keys.concat(m.staticKeys || [])\n    }, []).join(',')\n  }\n\n  /**\n   * Check if two values are loosely equal - that is,\n   * if they are plain objects, do they have the same shape?\n   */\n  function looseEqual (a, b) {\n    if (a === b) { return true }\n    var isObjectA = isObject(a);\n    var isObjectB = isObject(b);\n    if (isObjectA && isObjectB) {\n      try {\n        var isArrayA = Array.isArray(a);\n        var isArrayB = Array.isArray(b);\n        if (isArrayA && isArrayB) {\n          return a.length === b.length && a.every(function (e, i) {\n            return looseEqual(e, b[i])\n          })\n        } else if (a instanceof Date && b instanceof Date) {\n          return a.getTime() === b.getTime()\n        } else if (!isArrayA && !isArrayB) {\n          var keysA = Object.keys(a);\n          var keysB = Object.keys(b);\n          return keysA.length === keysB.length && keysA.every(function (key) {\n            return looseEqual(a[key], b[key])\n          })\n        } else {\n          /* istanbul ignore next */\n          return false\n        }\n      } catch (e) {\n        /* istanbul ignore next */\n        return false\n      }\n    } else if (!isObjectA && !isObjectB) {\n      return String(a) === String(b)\n    } else {\n      return false\n    }\n  }\n\n  /**\n   * Return the first index at which a loosely equal value can be\n   * found in the array (if value is a plain object, the array must\n   * contain an object of the same shape), or -1 if it is not present.\n   */\n  function looseIndexOf (arr, val) {\n    for (var i = 0; i < arr.length; i++) {\n      if (looseEqual(arr[i], val)) { return i }\n    }\n    return -1\n  }\n\n  /**\n   * Ensure a function is called only once.\n   */\n  function once (fn) {\n    var called = false;\n    return function () {\n      if (!called) {\n        called = true;\n        fn.apply(this, arguments);\n      }\n    }\n  }\n\n  var SSR_ATTR = 'data-server-rendered';\n\n  var ASSET_TYPES = [\n    'component',\n    'directive',\n    'filter'\n  ];\n\n  var LIFECYCLE_HOOKS = [\n    'beforeCreate',\n    'created',\n    'beforeMount',\n    'mounted',\n    'beforeUpdate',\n    'updated',\n    'beforeDestroy',\n    'destroyed',\n    'activated',\n    'deactivated',\n    'errorCaptured',\n    'serverPrefetch'\n  ];\n\n  /*  */\n\n\n\n  var config = ({\n    /**\n     * Option merge strategies (used in core/util/options)\n     */\n    // $flow-disable-line\n    optionMergeStrategies: Object.create(null),\n\n    /**\n     * Whether to suppress warnings.\n     */\n    silent: false,\n\n    /**\n     * Show production mode tip message on boot?\n     */\n    productionTip: \"development\" !== 'production',\n\n    /**\n     * Whether to enable devtools\n     */\n    devtools: \"development\" !== 'production',\n\n    /**\n     * Whether to record perf\n     */\n    performance: false,\n\n    /**\n     * Error handler for watcher errors\n     */\n    errorHandler: null,\n\n    /**\n     * Warn handler for watcher warns\n     */\n    warnHandler: null,\n\n    /**\n     * Ignore certain custom elements\n     */\n    ignoredElements: [],\n\n    /**\n     * Custom user key aliases for v-on\n     */\n    // $flow-disable-line\n    keyCodes: Object.create(null),\n\n    /**\n     * Check if a tag is reserved so that it cannot be registered as a\n     * component. This is platform-dependent and may be overwritten.\n     */\n    isReservedTag: no,\n\n    /**\n     * Check if an attribute is reserved so that it cannot be used as a component\n     * prop. This is platform-dependent and may be overwritten.\n     */\n    isReservedAttr: no,\n\n    /**\n     * Check if a tag is an unknown element.\n     * Platform-dependent.\n     */\n    isUnknownElement: no,\n\n    /**\n     * Get the namespace of an element\n     */\n    getTagNamespace: noop,\n\n    /**\n     * Parse the real tag name for the specific platform.\n     */\n    parsePlatformTagName: identity,\n\n    /**\n     * Check if an attribute must be bound using property, e.g. value\n     * Platform-dependent.\n     */\n    mustUseProp: no,\n\n    /**\n     * Perform updates asynchronously. Intended to be used by Vue Test Utils\n     * This will significantly reduce performance if set to false.\n     */\n    async: true,\n\n    /**\n     * Exposed for legacy reasons\n     */\n    _lifecycleHooks: LIFECYCLE_HOOKS\n  });\n\n  /*  */\n\n  /**\n   * unicode letters used for parsing html tags, component names and property paths.\n   * using https://www.w3.org/TR/html53/semantics-scripting.html#potentialcustomelementname\n   * skipping \\u10000-\\uEFFFF due to it freezing up PhantomJS\n   */\n  var unicodeRegExp = /a-zA-Z\\u00B7\\u00C0-\\u00D6\\u00D8-\\u00F6\\u00F8-\\u037D\\u037F-\\u1FFF\\u200C-\\u200D\\u203F-\\u2040\\u2070-\\u218F\\u2C00-\\u2FEF\\u3001-\\uD7FF\\uF900-\\uFDCF\\uFDF0-\\uFFFD/;\n\n  /**\n   * Check if a string starts with $ or _\n   */\n  function isReserved (str) {\n    var c = (str + '').charCodeAt(0);\n    return c === 0x24 || c === 0x5F\n  }\n\n  /**\n   * Define a property.\n   */\n  function def (obj, key, val, enumerable) {\n    Object.defineProperty(obj, key, {\n      value: val,\n      enumerable: !!enumerable,\n      writable: true,\n      configurable: true\n    });\n  }\n\n  /**\n   * Parse simple path.\n   */\n  var bailRE = new RegExp((\"[^\" + (unicodeRegExp.source) + \".$_\\\\d]\"));\n  function parsePath (path) {\n    if (bailRE.test(path)) {\n      return\n    }\n    var segments = path.split('.');\n    return function (obj) {\n      for (var i = 0; i < segments.length; i++) {\n        if (!obj) { return }\n        obj = obj[segments[i]];\n      }\n      return obj\n    }\n  }\n\n  /*  */\n\n  // can we use __proto__?\n  var hasProto = '__proto__' in {};\n\n  // Browser environment sniffing\n  var inBrowser = typeof window !== 'undefined';\n  var inWeex = typeof WXEnvironment !== 'undefined' && !!WXEnvironment.platform;\n  var weexPlatform = inWeex && WXEnvironment.platform.toLowerCase();\n  var UA = inBrowser && window.navigator.userAgent.toLowerCase();\n  var isIE = UA && /msie|trident/.test(UA);\n  var isIE9 = UA && UA.indexOf('msie 9.0') > 0;\n  var isEdge = UA && UA.indexOf('edge/') > 0;\n  var isAndroid = (UA && UA.indexOf('android') > 0) || (weexPlatform === 'android');\n  var isIOS = (UA && /iphone|ipad|ipod|ios/.test(UA)) || (weexPlatform === 'ios');\n  var isChrome = UA && /chrome\\/\\d+/.test(UA) && !isEdge;\n  var isPhantomJS = UA && /phantomjs/.test(UA);\n  var isFF = UA && UA.match(/firefox\\/(\\d+)/);\n\n  // Firefox has a \"watch\" function on Object.prototype...\n  var nativeWatch = ({}).watch;\n\n  var supportsPassive = false;\n  if (inBrowser) {\n    try {\n      var opts = {};\n      Object.defineProperty(opts, 'passive', ({\n        get: function get () {\n          /* istanbul ignore next */\n          supportsPassive = true;\n        }\n      })); // https://github.com/facebook/flow/issues/285\n      window.addEventListener('test-passive', null, opts);\n    } catch (e) {}\n  }\n\n  // this needs to be lazy-evaled because vue may be required before\n  // vue-server-renderer can set VUE_ENV\n  var _isServer;\n  var isServerRendering = function () {\n    if (_isServer === undefined) {\n      /* istanbul ignore if */\n      if (!inBrowser && !inWeex && typeof global !== 'undefined') {\n        // detect presence of vue-server-renderer and avoid\n        // Webpack shimming the process\n        _isServer = global['process'] && global['process'].env.VUE_ENV === 'server';\n      } else {\n        _isServer = false;\n      }\n    }\n    return _isServer\n  };\n\n  // detect devtools\n  var devtools = inBrowser && window.__VUE_DEVTOOLS_GLOBAL_HOOK__;\n\n  /* istanbul ignore next */\n  function isNative (Ctor) {\n    return typeof Ctor === 'function' && /native code/.test(Ctor.toString())\n  }\n\n  var hasSymbol =\n    typeof Symbol !== 'undefined' && isNative(Symbol) &&\n    typeof Reflect !== 'undefined' && isNative(Reflect.ownKeys);\n\n  var _Set;\n  /* istanbul ignore if */ // $flow-disable-line\n  if (typeof Set !== 'undefined' && isNative(Set)) {\n    // use native Set when available.\n    _Set = Set;\n  } else {\n    // a non-standard Set polyfill that only works with primitive keys.\n    _Set = /*@__PURE__*/(function () {\n      function Set () {\n        this.set = Object.create(null);\n      }\n      Set.prototype.has = function has (key) {\n        return this.set[key] === true\n      };\n      Set.prototype.add = function add (key) {\n        this.set[key] = true;\n      };\n      Set.prototype.clear = function clear () {\n        this.set = Object.create(null);\n      };\n\n      return Set;\n    }());\n  }\n\n  /*  */\n\n  var warn = noop;\n  var tip = noop;\n  var generateComponentTrace = (noop); // work around flow check\n  var formatComponentName = (noop);\n\n  {\n    var hasConsole = typeof console !== 'undefined';\n    var classifyRE = /(?:^|[-_])(\\w)/g;\n    var classify = function (str) { return str\n      .replace(classifyRE, function (c) { return c.toUpperCase(); })\n      .replace(/[-_]/g, ''); };\n\n    warn = function (msg, vm) {\n      var trace = vm ? generateComponentTrace(vm) : '';\n\n      if (config.warnHandler) {\n        config.warnHandler.call(null, msg, vm, trace);\n      } else if (hasConsole && (!config.silent)) {\n        console.error((\"[Vue warn]: \" + msg + trace));\n      }\n    };\n\n    tip = function (msg, vm) {\n      if (hasConsole && (!config.silent)) {\n        console.warn(\"[Vue tip]: \" + msg + (\n          vm ? generateComponentTrace(vm) : ''\n        ));\n      }\n    };\n\n    formatComponentName = function (vm, includeFile) {\n      if (vm.$root === vm) {\n        return '<Root>'\n      }\n      var options = typeof vm === 'function' && vm.cid != null\n        ? vm.options\n        : vm._isVue\n          ? vm.$options || vm.constructor.options\n          : vm;\n      var name = options.name || options._componentTag;\n      var file = options.__file;\n      if (!name && file) {\n        var match = file.match(/([^/\\\\]+)\\.vue$/);\n        name = match && match[1];\n      }\n\n      return (\n        (name ? (\"<\" + (classify(name)) + \">\") : \"<Anonymous>\") +\n        (file && includeFile !== false ? (\" at \" + file) : '')\n      )\n    };\n\n    var repeat = function (str, n) {\n      var res = '';\n      while (n) {\n        if (n % 2 === 1) { res += str; }\n        if (n > 1) { str += str; }\n        n >>= 1;\n      }\n      return res\n    };\n\n    generateComponentTrace = function (vm) {\n      if (vm._isVue && vm.$parent) {\n        var tree = [];\n        var currentRecursiveSequence = 0;\n        while (vm) {\n          if (tree.length > 0) {\n            var last = tree[tree.length - 1];\n            if (last.constructor === vm.constructor) {\n              currentRecursiveSequence++;\n              vm = vm.$parent;\n              continue\n            } else if (currentRecursiveSequence > 0) {\n              tree[tree.length - 1] = [last, currentRecursiveSequence];\n              currentRecursiveSequence = 0;\n            }\n          }\n          tree.push(vm);\n          vm = vm.$parent;\n        }\n        return '\\n\\nfound in\\n\\n' + tree\n          .map(function (vm, i) { return (\"\" + (i === 0 ? '---> ' : repeat(' ', 5 + i * 2)) + (Array.isArray(vm)\n              ? ((formatComponentName(vm[0])) + \"... (\" + (vm[1]) + \" recursive calls)\")\n              : formatComponentName(vm))); })\n          .join('\\n')\n      } else {\n        return (\"\\n\\n(found in \" + (formatComponentName(vm)) + \")\")\n      }\n    };\n  }\n\n  /*  */\n\n  var uid = 0;\n\n  /**\n   * A dep is an observable that can have multiple\n   * directives subscribing to it.\n   */\n  var Dep = function Dep () {\n    this.id = uid++;\n    this.subs = [];\n  };\n\n  Dep.prototype.addSub = function addSub (sub) {\n    this.subs.push(sub);\n  };\n\n  Dep.prototype.removeSub = function removeSub (sub) {\n    remove(this.subs, sub);\n  };\n\n  Dep.prototype.depend = function depend () {\n    if (Dep.target) {\n      Dep.target.addDep(this);\n    }\n  };\n\n  Dep.prototype.notify = function notify () {\n    // stabilize the subscriber list first\n    var subs = this.subs.slice();\n    if (!config.async) {\n      // subs aren't sorted in scheduler if not running async\n      // we need to sort them now to make sure they fire in correct\n      // order\n      subs.sort(function (a, b) { return a.id - b.id; });\n    }\n    for (var i = 0, l = subs.length; i < l; i++) {\n      subs[i].update();\n    }\n  };\n\n  // The current target watcher being evaluated.\n  // This is globally unique because only one watcher\n  // can be evaluated at a time.\n  Dep.target = null;\n  var targetStack = [];\n\n  function pushTarget (target) {\n    targetStack.push(target);\n    Dep.target = target;\n  }\n\n  function popTarget () {\n    targetStack.pop();\n    Dep.target = targetStack[targetStack.length - 1];\n  }\n\n  /*  */\n\n  var VNode = function VNode (\n    tag,\n    data,\n    children,\n    text,\n    elm,\n    context,\n    componentOptions,\n    asyncFactory\n  ) {\n    this.tag = tag;\n    this.data = data;\n    this.children = children;\n    this.text = text;\n    this.elm = elm;\n    this.ns = undefined;\n    this.context = context;\n    this.fnContext = undefined;\n    this.fnOptions = undefined;\n    this.fnScopeId = undefined;\n    this.key = data && data.key;\n    this.componentOptions = componentOptions;\n    this.componentInstance = undefined;\n    this.parent = undefined;\n    this.raw = false;\n    this.isStatic = false;\n    this.isRootInsert = true;\n    this.isComment = false;\n    this.isCloned = false;\n    this.isOnce = false;\n    this.asyncFactory = asyncFactory;\n    this.asyncMeta = undefined;\n    this.isAsyncPlaceholder = false;\n  };\n\n  var prototypeAccessors = { child: { configurable: true } };\n\n  // DEPRECATED: alias for componentInstance for backwards compat.\n  /* istanbul ignore next */\n  prototypeAccessors.child.get = function () {\n    return this.componentInstance\n  };\n\n  Object.defineProperties( VNode.prototype, prototypeAccessors );\n\n  var createEmptyVNode = function (text) {\n    if ( text === void 0 ) text = '';\n\n    var node = new VNode();\n    node.text = text;\n    node.isComment = true;\n    return node\n  };\n\n  function createTextVNode (val) {\n    return new VNode(undefined, undefined, undefined, String(val))\n  }\n\n  // optimized shallow clone\n  // used for static nodes and slot nodes because they may be reused across\n  // multiple renders, cloning them avoids errors when DOM manipulations rely\n  // on their elm reference.\n  function cloneVNode (vnode) {\n    var cloned = new VNode(\n      vnode.tag,\n      vnode.data,\n      // #7975\n      // clone children array to avoid mutating original in case of cloning\n      // a child.\n      vnode.children && vnode.children.slice(),\n      vnode.text,\n      vnode.elm,\n      vnode.context,\n      vnode.componentOptions,\n      vnode.asyncFactory\n    );\n    cloned.ns = vnode.ns;\n    cloned.isStatic = vnode.isStatic;\n    cloned.key = vnode.key;\n    cloned.isComment = vnode.isComment;\n    cloned.fnContext = vnode.fnContext;\n    cloned.fnOptions = vnode.fnOptions;\n    cloned.fnScopeId = vnode.fnScopeId;\n    cloned.asyncMeta = vnode.asyncMeta;\n    cloned.isCloned = true;\n    return cloned\n  }\n\n  /*\n   * not type checking this file because flow doesn't play well with\n   * dynamically accessing methods on Array prototype\n   */\n\n  var arrayProto = Array.prototype;\n  var arrayMethods = Object.create(arrayProto);\n\n  var methodsToPatch = [\n    'push',\n    'pop',\n    'shift',\n    'unshift',\n    'splice',\n    'sort',\n    'reverse'\n  ];\n\n  /**\n   * Intercept mutating methods and emit events\n   */\n  methodsToPatch.forEach(function (method) {\n    // cache original method\n    var original = arrayProto[method];\n    def(arrayMethods, method, function mutator () {\n      var args = [], len = arguments.length;\n      while ( len-- ) args[ len ] = arguments[ len ];\n\n      var result = original.apply(this, args);\n      var ob = this.__ob__;\n      var inserted;\n      switch (method) {\n        case 'push':\n        case 'unshift':\n          inserted = args;\n          break\n        case 'splice':\n          inserted = args.slice(2);\n          break\n      }\n      if (inserted) { ob.observeArray(inserted); }\n      // notify change\n      ob.dep.notify();\n      return result\n    });\n  });\n\n  /*  */\n\n  var arrayKeys = Object.getOwnPropertyNames(arrayMethods);\n\n  /**\n   * In some cases we may want to disable observation inside a component's\n   * update computation.\n   */\n  var shouldObserve = true;\n\n  function toggleObserving (value) {\n    shouldObserve = value;\n  }\n\n  /**\n   * Observer class that is attached to each observed\n   * object. Once attached, the observer converts the target\n   * object's property keys into getter/setters that\n   * collect dependencies and dispatch updates.\n   */\n  var Observer = function Observer (value) {\n    this.value = value;\n    this.dep = new Dep();\n    this.vmCount = 0;\n    def(value, '__ob__', this);\n    if (Array.isArray(value)) {\n      if (hasProto) {\n        protoAugment(value, arrayMethods);\n      } else {\n        copyAugment(value, arrayMethods, arrayKeys);\n      }\n      this.observeArray(value);\n    } else {\n      this.walk(value);\n    }\n  };\n\n  /**\n   * Walk through all properties and convert them into\n   * getter/setters. This method should only be called when\n   * value type is Object.\n   */\n  Observer.prototype.walk = function walk (obj) {\n    var keys = Object.keys(obj);\n    for (var i = 0; i < keys.length; i++) {\n      defineReactive$$1(obj, keys[i]);\n    }\n  };\n\n  /**\n   * Observe a list of Array items.\n   */\n  Observer.prototype.observeArray = function observeArray (items) {\n    for (var i = 0, l = items.length; i < l; i++) {\n      observe(items[i]);\n    }\n  };\n\n  // helpers\n\n  /**\n   * Augment a target Object or Array by intercepting\n   * the prototype chain using __proto__\n   */\n  function protoAugment (target, src) {\n    /* eslint-disable no-proto */\n    target.__proto__ = src;\n    /* eslint-enable no-proto */\n  }\n\n  /**\n   * Augment a target Object or Array by defining\n   * hidden properties.\n   */\n  /* istanbul ignore next */\n  function copyAugment (target, src, keys) {\n    for (var i = 0, l = keys.length; i < l; i++) {\n      var key = keys[i];\n      def(target, key, src[key]);\n    }\n  }\n\n  /**\n   * Attempt to create an observer instance for a value,\n   * returns the new observer if successfully observed,\n   * or the existing observer if the value already has one.\n   */\n  function observe (value, asRootData) {\n    if (!isObject(value) || value instanceof VNode) {\n      return\n    }\n    var ob;\n    if (hasOwn(value, '__ob__') && value.__ob__ instanceof Observer) {\n      ob = value.__ob__;\n    } else if (\n      shouldObserve &&\n      !isServerRendering() &&\n      (Array.isArray(value) || isPlainObject(value)) &&\n      Object.isExtensible(value) &&\n      !value._isVue\n    ) {\n      ob = new Observer(value);\n    }\n    if (asRootData && ob) {\n      ob.vmCount++;\n    }\n    return ob\n  }\n\n  /**\n   * Define a reactive property on an Object.\n   */\n  function defineReactive$$1 (\n    obj,\n    key,\n    val,\n    customSetter,\n    shallow\n  ) {\n    var dep = new Dep();\n\n    var property = Object.getOwnPropertyDescriptor(obj, key);\n    if (property && property.configurable === false) {\n      return\n    }\n\n    // cater for pre-defined getter/setters\n    var getter = property && property.get;\n    var setter = property && property.set;\n    if ((!getter || setter) && arguments.length === 2) {\n      val = obj[key];\n    }\n\n    var childOb = !shallow && observe(val);\n    Object.defineProperty(obj, key, {\n      enumerable: true,\n      configurable: true,\n      get: function reactiveGetter () {\n        var value = getter ? getter.call(obj) : val;\n        if (Dep.target) {\n          dep.depend();\n          if (childOb) {\n            childOb.dep.depend();\n            if (Array.isArray(value)) {\n              dependArray(value);\n            }\n          }\n        }\n        return value\n      },\n      set: function reactiveSetter (newVal) {\n        var value = getter ? getter.call(obj) : val;\n        /* eslint-disable no-self-compare */\n        if (newVal === value || (newVal !== newVal && value !== value)) {\n          return\n        }\n        /* eslint-enable no-self-compare */\n        if (customSetter) {\n          customSetter();\n        }\n        // #7981: for accessor properties without setter\n        if (getter && !setter) { return }\n        if (setter) {\n          setter.call(obj, newVal);\n        } else {\n          val = newVal;\n        }\n        childOb = !shallow && observe(newVal);\n        dep.notify();\n      }\n    });\n  }\n\n  /**\n   * Set a property on an object. Adds the new property and\n   * triggers change notification if the property doesn't\n   * already exist.\n   */\n  function set (target, key, val) {\n    if (isUndef(target) || isPrimitive(target)\n    ) {\n      warn((\"Cannot set reactive property on undefined, null, or primitive value: \" + ((target))));\n    }\n    if (Array.isArray(target) && isValidArrayIndex(key)) {\n      target.length = Math.max(target.length, key);\n      target.splice(key, 1, val);\n      return val\n    }\n    if (key in target && !(key in Object.prototype)) {\n      target[key] = val;\n      return val\n    }\n    var ob = (target).__ob__;\n    if (target._isVue || (ob && ob.vmCount)) {\n      warn(\n        'Avoid adding reactive properties to a Vue instance or its root $data ' +\n        'at runtime - declare it upfront in the data option.'\n      );\n      return val\n    }\n    if (!ob) {\n      target[key] = val;\n      return val\n    }\n    defineReactive$$1(ob.value, key, val);\n    ob.dep.notify();\n    return val\n  }\n\n  /**\n   * Delete a property and trigger change if necessary.\n   */\n  function del (target, key) {\n    if (isUndef(target) || isPrimitive(target)\n    ) {\n      warn((\"Cannot delete reactive property on undefined, null, or primitive value: \" + ((target))));\n    }\n    if (Array.isArray(target) && isValidArrayIndex(key)) {\n      target.splice(key, 1);\n      return\n    }\n    var ob = (target).__ob__;\n    if (target._isVue || (ob && ob.vmCount)) {\n      warn(\n        'Avoid deleting properties on a Vue instance or its root $data ' +\n        '- just set it to null.'\n      );\n      return\n    }\n    if (!hasOwn(target, key)) {\n      return\n    }\n    delete target[key];\n    if (!ob) {\n      return\n    }\n    ob.dep.notify();\n  }\n\n  /**\n   * Collect dependencies on array elements when the array is touched, since\n   * we cannot intercept array element access like property getters.\n   */\n  function dependArray (value) {\n    for (var e = (void 0), i = 0, l = value.length; i < l; i++) {\n      e = value[i];\n      e && e.__ob__ && e.__ob__.dep.depend();\n      if (Array.isArray(e)) {\n        dependArray(e);\n      }\n    }\n  }\n\n  /*  */\n\n  /**\n   * Option overwriting strategies are functions that handle\n   * how to merge a parent option value and a child option\n   * value into the final value.\n   */\n  var strats = config.optionMergeStrategies;\n\n  /**\n   * Options with restrictions\n   */\n  {\n    strats.el = strats.propsData = function (parent, child, vm, key) {\n      if (!vm) {\n        warn(\n          \"option \\\"\" + key + \"\\\" can only be used during instance \" +\n          'creation with the `new` keyword.'\n        );\n      }\n      return defaultStrat(parent, child)\n    };\n  }\n\n  /**\n   * Helper that recursively merges two data objects together.\n   */\n  function mergeData (to, from) {\n    if (!from) { return to }\n    var key, toVal, fromVal;\n\n    var keys = hasSymbol\n      ? Reflect.ownKeys(from)\n      : Object.keys(from);\n\n    for (var i = 0; i < keys.length; i++) {\n      key = keys[i];\n      // in case the object is already observed...\n      if (key === '__ob__') { continue }\n      toVal = to[key];\n      fromVal = from[key];\n      if (!hasOwn(to, key)) {\n        set(to, key, fromVal);\n      } else if (\n        toVal !== fromVal &&\n        isPlainObject(toVal) &&\n        isPlainObject(fromVal)\n      ) {\n        mergeData(toVal, fromVal);\n      }\n    }\n    return to\n  }\n\n  /**\n   * Data\n   */\n  function mergeDataOrFn (\n    parentVal,\n    childVal,\n    vm\n  ) {\n    if (!vm) {\n      // in a Vue.extend merge, both should be functions\n      if (!childVal) {\n        return parentVal\n      }\n      if (!parentVal) {\n        return childVal\n      }\n      // when parentVal & childVal are both present,\n      // we need to return a function that returns the\n      // merged result of both functions... no need to\n      // check if parentVal is a function here because\n      // it has to be a function to pass previous merges.\n      return function mergedDataFn () {\n        return mergeData(\n          typeof childVal === 'function' ? childVal.call(this, this) : childVal,\n          typeof parentVal === 'function' ? parentVal.call(this, this) : parentVal\n        )\n      }\n    } else {\n      return function mergedInstanceDataFn () {\n        // instance merge\n        var instanceData = typeof childVal === 'function'\n          ? childVal.call(vm, vm)\n          : childVal;\n        var defaultData = typeof parentVal === 'function'\n          ? parentVal.call(vm, vm)\n          : parentVal;\n        if (instanceData) {\n          return mergeData(instanceData, defaultData)\n        } else {\n          return defaultData\n        }\n      }\n    }\n  }\n\n  strats.data = function (\n    parentVal,\n    childVal,\n    vm\n  ) {\n    if (!vm) {\n      if (childVal && typeof childVal !== 'function') {\n        warn(\n          'The \"data\" option should be a function ' +\n          'that returns a per-instance value in component ' +\n          'definitions.',\n          vm\n        );\n\n        return parentVal\n      }\n      return mergeDataOrFn(parentVal, childVal)\n    }\n\n    return mergeDataOrFn(parentVal, childVal, vm)\n  };\n\n  /**\n   * Hooks and props are merged as arrays.\n   */\n  function mergeHook (\n    parentVal,\n    childVal\n  ) {\n    var res = childVal\n      ? parentVal\n        ? parentVal.concat(childVal)\n        : Array.isArray(childVal)\n          ? childVal\n          : [childVal]\n      : parentVal;\n    return res\n      ? dedupeHooks(res)\n      : res\n  }\n\n  function dedupeHooks (hooks) {\n    var res = [];\n    for (var i = 0; i < hooks.length; i++) {\n      if (res.indexOf(hooks[i]) === -1) {\n        res.push(hooks[i]);\n      }\n    }\n    return res\n  }\n\n  LIFECYCLE_HOOKS.forEach(function (hook) {\n    strats[hook] = mergeHook;\n  });\n\n  /**\n   * Assets\n   *\n   * When a vm is present (instance creation), we need to do\n   * a three-way merge between constructor options, instance\n   * options and parent options.\n   */\n  function mergeAssets (\n    parentVal,\n    childVal,\n    vm,\n    key\n  ) {\n    var res = Object.create(parentVal || null);\n    if (childVal) {\n      assertObjectType(key, childVal, vm);\n      return extend(res, childVal)\n    } else {\n      return res\n    }\n  }\n\n  ASSET_TYPES.forEach(function (type) {\n    strats[type + 's'] = mergeAssets;\n  });\n\n  /**\n   * Watchers.\n   *\n   * Watchers hashes should not overwrite one\n   * another, so we merge them as arrays.\n   */\n  strats.watch = function (\n    parentVal,\n    childVal,\n    vm,\n    key\n  ) {\n    // work around Firefox's Object.prototype.watch...\n    if (parentVal === nativeWatch) { parentVal = undefined; }\n    if (childVal === nativeWatch) { childVal = undefined; }\n    /* istanbul ignore if */\n    if (!childVal) { return Object.create(parentVal || null) }\n    {\n      assertObjectType(key, childVal, vm);\n    }\n    if (!parentVal) { return childVal }\n    var ret = {};\n    extend(ret, parentVal);\n    for (var key$1 in childVal) {\n      var parent = ret[key$1];\n      var child = childVal[key$1];\n      if (parent && !Array.isArray(parent)) {\n        parent = [parent];\n      }\n      ret[key$1] = parent\n        ? parent.concat(child)\n        : Array.isArray(child) ? child : [child];\n    }\n    return ret\n  };\n\n  /**\n   * Other object hashes.\n   */\n  strats.props =\n  strats.methods =\n  strats.inject =\n  strats.computed = function (\n    parentVal,\n    childVal,\n    vm,\n    key\n  ) {\n    if (childVal && \"development\" !== 'production') {\n      assertObjectType(key, childVal, vm);\n    }\n    if (!parentVal) { return childVal }\n    var ret = Object.create(null);\n    extend(ret, parentVal);\n    if (childVal) { extend(ret, childVal); }\n    return ret\n  };\n  strats.provide = mergeDataOrFn;\n\n  /**\n   * Default strategy.\n   */\n  var defaultStrat = function (parentVal, childVal) {\n    return childVal === undefined\n      ? parentVal\n      : childVal\n  };\n\n  /**\n   * Validate component names\n   */\n  function checkComponents (options) {\n    for (var key in options.components) {\n      validateComponentName(key);\n    }\n  }\n\n  function validateComponentName (name) {\n    if (!new RegExp((\"^[a-zA-Z][\\\\-\\\\.0-9_\" + (unicodeRegExp.source) + \"]*$\")).test(name)) {\n      warn(\n        'Invalid component name: \"' + name + '\". Component names ' +\n        'should conform to valid custom element name in html5 specification.'\n      );\n    }\n    if (isBuiltInTag(name) || config.isReservedTag(name)) {\n      warn(\n        'Do not use built-in or reserved HTML elements as component ' +\n        'id: ' + name\n      );\n    }\n  }\n\n  /**\n   * Ensure all props option syntax are normalized into the\n   * Object-based format.\n   */\n  function normalizeProps (options, vm) {\n    var props = options.props;\n    if (!props) { return }\n    var res = {};\n    var i, val, name;\n    if (Array.isArray(props)) {\n      i = props.length;\n      while (i--) {\n        val = props[i];\n        if (typeof val === 'string') {\n          name = camelize(val);\n          res[name] = { type: null };\n        } else {\n          warn('props must be strings when using array syntax.');\n        }\n      }\n    } else if (isPlainObject(props)) {\n      for (var key in props) {\n        val = props[key];\n        name = camelize(key);\n        res[name] = isPlainObject(val)\n          ? val\n          : { type: val };\n      }\n    } else {\n      warn(\n        \"Invalid value for option \\\"props\\\": expected an Array or an Object, \" +\n        \"but got \" + (toRawType(props)) + \".\",\n        vm\n      );\n    }\n    options.props = res;\n  }\n\n  /**\n   * Normalize all injections into Object-based format\n   */\n  function normalizeInject (options, vm) {\n    var inject = options.inject;\n    if (!inject) { return }\n    var normalized = options.inject = {};\n    if (Array.isArray(inject)) {\n      for (var i = 0; i < inject.length; i++) {\n        normalized[inject[i]] = { from: inject[i] };\n      }\n    } else if (isPlainObject(inject)) {\n      for (var key in inject) {\n        var val = inject[key];\n        normalized[key] = isPlainObject(val)\n          ? extend({ from: key }, val)\n          : { from: val };\n      }\n    } else {\n      warn(\n        \"Invalid value for option \\\"inject\\\": expected an Array or an Object, \" +\n        \"but got \" + (toRawType(inject)) + \".\",\n        vm\n      );\n    }\n  }\n\n  /**\n   * Normalize raw function directives into object format.\n   */\n  function normalizeDirectives (options) {\n    var dirs = options.directives;\n    if (dirs) {\n      for (var key in dirs) {\n        var def$$1 = dirs[key];\n        if (typeof def$$1 === 'function') {\n          dirs[key] = { bind: def$$1, update: def$$1 };\n        }\n      }\n    }\n  }\n\n  function assertObjectType (name, value, vm) {\n    if (!isPlainObject(value)) {\n      warn(\n        \"Invalid value for option \\\"\" + name + \"\\\": expected an Object, \" +\n        \"but got \" + (toRawType(value)) + \".\",\n        vm\n      );\n    }\n  }\n\n  /**\n   * Merge two option objects into a new one.\n   * Core utility used in both instantiation and inheritance.\n   */\n  function mergeOptions (\n    parent,\n    child,\n    vm\n  ) {\n    {\n      checkComponents(child);\n    }\n\n    if (typeof child === 'function') {\n      child = child.options;\n    }\n\n    normalizeProps(child, vm);\n    normalizeInject(child, vm);\n    normalizeDirectives(child);\n\n    // Apply extends and mixins on the child options,\n    // but only if it is a raw options object that isn't\n    // the result of another mergeOptions call.\n    // Only merged options has the _base property.\n    if (!child._base) {\n      if (child.extends) {\n        parent = mergeOptions(parent, child.extends, vm);\n      }\n      if (child.mixins) {\n        for (var i = 0, l = child.mixins.length; i < l; i++) {\n          parent = mergeOptions(parent, child.mixins[i], vm);\n        }\n      }\n    }\n\n    var options = {};\n    var key;\n    for (key in parent) {\n      mergeField(key);\n    }\n    for (key in child) {\n      if (!hasOwn(parent, key)) {\n        mergeField(key);\n      }\n    }\n    function mergeField (key) {\n      var strat = strats[key] || defaultStrat;\n      options[key] = strat(parent[key], child[key], vm, key);\n    }\n    return options\n  }\n\n  /**\n   * Resolve an asset.\n   * This function is used because child instances need access\n   * to assets defined in its ancestor chain.\n   */\n  function resolveAsset (\n    options,\n    type,\n    id,\n    warnMissing\n  ) {\n    /* istanbul ignore if */\n    if (typeof id !== 'string') {\n      return\n    }\n    var assets = options[type];\n    // check local registration variations first\n    if (hasOwn(assets, id)) { return assets[id] }\n    var camelizedId = camelize(id);\n    if (hasOwn(assets, camelizedId)) { return assets[camelizedId] }\n    var PascalCaseId = capitalize(camelizedId);\n    if (hasOwn(assets, PascalCaseId)) { return assets[PascalCaseId] }\n    // fallback to prototype chain\n    var res = assets[id] || assets[camelizedId] || assets[PascalCaseId];\n    if (warnMissing && !res) {\n      warn(\n        'Failed to resolve ' + type.slice(0, -1) + ': ' + id,\n        options\n      );\n    }\n    return res\n  }\n\n  /*  */\n\n\n\n  function validateProp (\n    key,\n    propOptions,\n    propsData,\n    vm\n  ) {\n    var prop = propOptions[key];\n    var absent = !hasOwn(propsData, key);\n    var value = propsData[key];\n    // boolean casting\n    var booleanIndex = getTypeIndex(Boolean, prop.type);\n    if (booleanIndex > -1) {\n      if (absent && !hasOwn(prop, 'default')) {\n        value = false;\n      } else if (value === '' || value === hyphenate(key)) {\n        // only cast empty string / same name to boolean if\n        // boolean has higher priority\n        var stringIndex = getTypeIndex(String, prop.type);\n        if (stringIndex < 0 || booleanIndex < stringIndex) {\n          value = true;\n        }\n      }\n    }\n    // check default value\n    if (value === undefined) {\n      value = getPropDefaultValue(vm, prop, key);\n      // since the default value is a fresh copy,\n      // make sure to observe it.\n      var prevShouldObserve = shouldObserve;\n      toggleObserving(true);\n      observe(value);\n      toggleObserving(prevShouldObserve);\n    }\n    {\n      assertProp(prop, key, value, vm, absent);\n    }\n    return value\n  }\n\n  /**\n   * Get the default value of a prop.\n   */\n  function getPropDefaultValue (vm, prop, key) {\n    // no default, return undefined\n    if (!hasOwn(prop, 'default')) {\n      return undefined\n    }\n    var def = prop.default;\n    // warn against non-factory defaults for Object & Array\n    if (isObject(def)) {\n      warn(\n        'Invalid default value for prop \"' + key + '\": ' +\n        'Props with type Object/Array must use a factory function ' +\n        'to return the default value.',\n        vm\n      );\n    }\n    // the raw prop value was also undefined from previous render,\n    // return previous default value to avoid unnecessary watcher trigger\n    if (vm && vm.$options.propsData &&\n      vm.$options.propsData[key] === undefined &&\n      vm._props[key] !== undefined\n    ) {\n      return vm._props[key]\n    }\n    // call factory function for non-Function types\n    // a value is Function if its prototype is function even across different execution context\n    return typeof def === 'function' && getType(prop.type) !== 'Function'\n      ? def.call(vm)\n      : def\n  }\n\n  /**\n   * Assert whether a prop is valid.\n   */\n  function assertProp (\n    prop,\n    name,\n    value,\n    vm,\n    absent\n  ) {\n    if (prop.required && absent) {\n      warn(\n        'Missing required prop: \"' + name + '\"',\n        vm\n      );\n      return\n    }\n    if (value == null && !prop.required) {\n      return\n    }\n    var type = prop.type;\n    var valid = !type || type === true;\n    var expectedTypes = [];\n    if (type) {\n      if (!Array.isArray(type)) {\n        type = [type];\n      }\n      for (var i = 0; i < type.length && !valid; i++) {\n        var assertedType = assertType(value, type[i]);\n        expectedTypes.push(assertedType.expectedType || '');\n        valid = assertedType.valid;\n      }\n    }\n\n    if (!valid) {\n      warn(\n        getInvalidTypeMessage(name, value, expectedTypes),\n        vm\n      );\n      return\n    }\n    var validator = prop.validator;\n    if (validator) {\n      if (!validator(value)) {\n        warn(\n          'Invalid prop: custom validator check failed for prop \"' + name + '\".',\n          vm\n        );\n      }\n    }\n  }\n\n  var simpleCheckRE = /^(String|Number|Boolean|Function|Symbol)$/;\n\n  function assertType (value, type) {\n    var valid;\n    var expectedType = getType(type);\n    if (simpleCheckRE.test(expectedType)) {\n      var t = typeof value;\n      valid = t === expectedType.toLowerCase();\n      // for primitive wrapper objects\n      if (!valid && t === 'object') {\n        valid = value instanceof type;\n      }\n    } else if (expectedType === 'Object') {\n      valid = isPlainObject(value);\n    } else if (expectedType === 'Array') {\n      valid = Array.isArray(value);\n    } else {\n      valid = value instanceof type;\n    }\n    return {\n      valid: valid,\n      expectedType: expectedType\n    }\n  }\n\n  /**\n   * Use function string name to check built-in types,\n   * because a simple equality check will fail when running\n   * across different vms / iframes.\n   */\n  function getType (fn) {\n    var match = fn && fn.toString().match(/^\\s*function (\\w+)/);\n    return match ? match[1] : ''\n  }\n\n  function isSameType (a, b) {\n    return getType(a) === getType(b)\n  }\n\n  function getTypeIndex (type, expectedTypes) {\n    if (!Array.isArray(expectedTypes)) {\n      return isSameType(expectedTypes, type) ? 0 : -1\n    }\n    for (var i = 0, len = expectedTypes.length; i < len; i++) {\n      if (isSameType(expectedTypes[i], type)) {\n        return i\n      }\n    }\n    return -1\n  }\n\n  function getInvalidTypeMessage (name, value, expectedTypes) {\n    var message = \"Invalid prop: type check failed for prop \\\"\" + name + \"\\\".\" +\n      \" Expected \" + (expectedTypes.map(capitalize).join(', '));\n    var expectedType = expectedTypes[0];\n    var receivedType = toRawType(value);\n    var expectedValue = styleValue(value, expectedType);\n    var receivedValue = styleValue(value, receivedType);\n    // check if we need to specify expected value\n    if (expectedTypes.length === 1 &&\n        isExplicable(expectedType) &&\n        !isBoolean(expectedType, receivedType)) {\n      message += \" with value \" + expectedValue;\n    }\n    message += \", got \" + receivedType + \" \";\n    // check if we need to specify received value\n    if (isExplicable(receivedType)) {\n      message += \"with value \" + receivedValue + \".\";\n    }\n    return message\n  }\n\n  function styleValue (value, type) {\n    if (type === 'String') {\n      return (\"\\\"\" + value + \"\\\"\")\n    } else if (type === 'Number') {\n      return (\"\" + (Number(value)))\n    } else {\n      return (\"\" + value)\n    }\n  }\n\n  function isExplicable (value) {\n    var explicitTypes = ['string', 'number', 'boolean'];\n    return explicitTypes.some(function (elem) { return value.toLowerCase() === elem; })\n  }\n\n  function isBoolean () {\n    var args = [], len = arguments.length;\n    while ( len-- ) args[ len ] = arguments[ len ];\n\n    return args.some(function (elem) { return elem.toLowerCase() === 'boolean'; })\n  }\n\n  /*  */\n\n  function handleError (err, vm, info) {\n    // Deactivate deps tracking while processing error handler to avoid possible infinite rendering.\n    // See: https://github.com/vuejs/vuex/issues/1505\n    pushTarget();\n    try {\n      if (vm) {\n        var cur = vm;\n        while ((cur = cur.$parent)) {\n          var hooks = cur.$options.errorCaptured;\n          if (hooks) {\n            for (var i = 0; i < hooks.length; i++) {\n              try {\n                var capture = hooks[i].call(cur, err, vm, info) === false;\n                if (capture) { return }\n              } catch (e) {\n                globalHandleError(e, cur, 'errorCaptured hook');\n              }\n            }\n          }\n        }\n      }\n      globalHandleError(err, vm, info);\n    } finally {\n      popTarget();\n    }\n  }\n\n  function invokeWithErrorHandling (\n    handler,\n    context,\n    args,\n    vm,\n    info\n  ) {\n    var res;\n    try {\n      res = args ? handler.apply(context, args) : handler.call(context);\n      if (res && !res._isVue && isPromise(res) && !res._handled) {\n        res.catch(function (e) { return handleError(e, vm, info + \" (Promise/async)\"); });\n        // issue #9511\n        // avoid catch triggering multiple times when nested calls\n        res._handled = true;\n      }\n    } catch (e) {\n      handleError(e, vm, info);\n    }\n    return res\n  }\n\n  function globalHandleError (err, vm, info) {\n    if (config.errorHandler) {\n      try {\n        return config.errorHandler.call(null, err, vm, info)\n      } catch (e) {\n        // if the user intentionally throws the original error in the handler,\n        // do not log it twice\n        if (e !== err) {\n          logError(e, null, 'config.errorHandler');\n        }\n      }\n    }\n    logError(err, vm, info);\n  }\n\n  function logError (err, vm, info) {\n    {\n      warn((\"Error in \" + info + \": \\\"\" + (err.toString()) + \"\\\"\"), vm);\n    }\n    /* istanbul ignore else */\n    if ((inBrowser || inWeex) && typeof console !== 'undefined') {\n      console.error(err);\n    } else {\n      throw err\n    }\n  }\n\n  /*  */\n\n  var isUsingMicroTask = false;\n\n  var callbacks = [];\n  var pending = false;\n\n  function flushCallbacks () {\n    pending = false;\n    var copies = callbacks.slice(0);\n    callbacks.length = 0;\n    for (var i = 0; i < copies.length; i++) {\n      copies[i]();\n    }\n  }\n\n  // Here we have async deferring wrappers using microtasks.\n  // In 2.5 we used (macro) tasks (in combination with microtasks).\n  // However, it has subtle problems when state is changed right before repaint\n  // (e.g. #6813, out-in transitions).\n  // Also, using (macro) tasks in event handler would cause some weird behaviors\n  // that cannot be circumvented (e.g. #7109, #7153, #7546, #7834, #8109).\n  // So we now use microtasks everywhere, again.\n  // A major drawback of this tradeoff is that there are some scenarios\n  // where microtasks have too high a priority and fire in between supposedly\n  // sequential events (e.g. #4521, #6690, which have workarounds)\n  // or even between bubbling of the same event (#6566).\n  var timerFunc;\n\n  // The nextTick behavior leverages the microtask queue, which can be accessed\n  // via either native Promise.then or MutationObserver.\n  // MutationObserver has wider support, however it is seriously bugged in\n  // UIWebView in iOS >= 9.3.3 when triggered in touch event handlers. It\n  // completely stops working after triggering a few times... so, if native\n  // Promise is available, we will use it:\n  /* istanbul ignore next, $flow-disable-line */\n  if (typeof Promise !== 'undefined' && isNative(Promise)) {\n    var p = Promise.resolve();\n    timerFunc = function () {\n      p.then(flushCallbacks);\n      // In problematic UIWebViews, Promise.then doesn't completely break, but\n      // it can get stuck in a weird state where callbacks are pushed into the\n      // microtask queue but the queue isn't being flushed, until the browser\n      // needs to do some other work, e.g. handle a timer. Therefore we can\n      // \"force\" the microtask queue to be flushed by adding an empty timer.\n      if (isIOS) { setTimeout(noop); }\n    };\n    isUsingMicroTask = true;\n  } else if (!isIE && typeof MutationObserver !== 'undefined' && (\n    isNative(MutationObserver) ||\n    // PhantomJS and iOS 7.x\n    MutationObserver.toString() === '[object MutationObserverConstructor]'\n  )) {\n    // Use MutationObserver where native Promise is not available,\n    // e.g. PhantomJS, iOS7, Android 4.4\n    // (#6466 MutationObserver is unreliable in IE11)\n    var counter = 1;\n    var observer = new MutationObserver(flushCallbacks);\n    var textNode = document.createTextNode(String(counter));\n    observer.observe(textNode, {\n      characterData: true\n    });\n    timerFunc = function () {\n      counter = (counter + 1) % 2;\n      textNode.data = String(counter);\n    };\n    isUsingMicroTask = true;\n  } else if (typeof setImmediate !== 'undefined' && isNative(setImmediate)) {\n    // Fallback to setImmediate.\n    // Technically it leverages the (macro) task queue,\n    // but it is still a better choice than setTimeout.\n    timerFunc = function () {\n      setImmediate(flushCallbacks);\n    };\n  } else {\n    // Fallback to setTimeout.\n    timerFunc = function () {\n      setTimeout(flushCallbacks, 0);\n    };\n  }\n\n  function nextTick (cb, ctx) {\n    var _resolve;\n    callbacks.push(function () {\n      if (cb) {\n        try {\n          cb.call(ctx);\n        } catch (e) {\n          handleError(e, ctx, 'nextTick');\n        }\n      } else if (_resolve) {\n        _resolve(ctx);\n      }\n    });\n    if (!pending) {\n      pending = true;\n      timerFunc();\n    }\n    // $flow-disable-line\n    if (!cb && typeof Promise !== 'undefined') {\n      return new Promise(function (resolve) {\n        _resolve = resolve;\n      })\n    }\n  }\n\n  /*  */\n\n  var mark;\n  var measure;\n\n  {\n    var perf = inBrowser && window.performance;\n    /* istanbul ignore if */\n    if (\n      perf &&\n      perf.mark &&\n      perf.measure &&\n      perf.clearMarks &&\n      perf.clearMeasures\n    ) {\n      mark = function (tag) { return perf.mark(tag); };\n      measure = function (name, startTag, endTag) {\n        perf.measure(name, startTag, endTag);\n        perf.clearMarks(startTag);\n        perf.clearMarks(endTag);\n        // perf.clearMeasures(name)\n      };\n    }\n  }\n\n  /* not type checking this file because flow doesn't play well with Proxy */\n\n  var initProxy;\n\n  {\n    var allowedGlobals = makeMap(\n      'Infinity,undefined,NaN,isFinite,isNaN,' +\n      'parseFloat,parseInt,decodeURI,decodeURIComponent,encodeURI,encodeURIComponent,' +\n      'Math,Number,Date,Array,Object,Boolean,String,RegExp,Map,Set,JSON,Intl,' +\n      'require' // for Webpack/Browserify\n    );\n\n    var warnNonPresent = function (target, key) {\n      warn(\n        \"Property or method \\\"\" + key + \"\\\" is not defined on the instance but \" +\n        'referenced during render. Make sure that this property is reactive, ' +\n        'either in the data option, or for class-based components, by ' +\n        'initializing the property. ' +\n        'See: https://vuejs.org/v2/guide/reactivity.html#Declaring-Reactive-Properties.',\n        target\n      );\n    };\n\n    var warnReservedPrefix = function (target, key) {\n      warn(\n        \"Property \\\"\" + key + \"\\\" must be accessed with \\\"$data.\" + key + \"\\\" because \" +\n        'properties starting with \"$\" or \"_\" are not proxied in the Vue instance to ' +\n        'prevent conflicts with Vue internals. ' +\n        'See: https://vuejs.org/v2/api/#data',\n        target\n      );\n    };\n\n    var hasProxy =\n      typeof Proxy !== 'undefined' && isNative(Proxy);\n\n    if (hasProxy) {\n      var isBuiltInModifier = makeMap('stop,prevent,self,ctrl,shift,alt,meta,exact');\n      config.keyCodes = new Proxy(config.keyCodes, {\n        set: function set (target, key, value) {\n          if (isBuiltInModifier(key)) {\n            warn((\"Avoid overwriting built-in modifier in config.keyCodes: .\" + key));\n            return false\n          } else {\n            target[key] = value;\n            return true\n          }\n        }\n      });\n    }\n\n    var hasHandler = {\n      has: function has (target, key) {\n        var has = key in target;\n        var isAllowed = allowedGlobals(key) ||\n          (typeof key === 'string' && key.charAt(0) === '_' && !(key in target.$data));\n        if (!has && !isAllowed) {\n          if (key in target.$data) { warnReservedPrefix(target, key); }\n          else { warnNonPresent(target, key); }\n        }\n        return has || !isAllowed\n      }\n    };\n\n    var getHandler = {\n      get: function get (target, key) {\n        if (typeof key === 'string' && !(key in target)) {\n          if (key in target.$data) { warnReservedPrefix(target, key); }\n          else { warnNonPresent(target, key); }\n        }\n        return target[key]\n      }\n    };\n\n    initProxy = function initProxy (vm) {\n      if (hasProxy) {\n        // determine which proxy handler to use\n        var options = vm.$options;\n        var handlers = options.render && options.render._withStripped\n          ? getHandler\n          : hasHandler;\n        vm._renderProxy = new Proxy(vm, handlers);\n      } else {\n        vm._renderProxy = vm;\n      }\n    };\n  }\n\n  /*  */\n\n  var seenObjects = new _Set();\n\n  /**\n   * Recursively traverse an object to evoke all converted\n   * getters, so that every nested property inside the object\n   * is collected as a \"deep\" dependency.\n   */\n  function traverse (val) {\n    _traverse(val, seenObjects);\n    seenObjects.clear();\n  }\n\n  function _traverse (val, seen) {\n    var i, keys;\n    var isA = Array.isArray(val);\n    if ((!isA && !isObject(val)) || Object.isFrozen(val) || val instanceof VNode) {\n      return\n    }\n    if (val.__ob__) {\n      var depId = val.__ob__.dep.id;\n      if (seen.has(depId)) {\n        return\n      }\n      seen.add(depId);\n    }\n    if (isA) {\n      i = val.length;\n      while (i--) { _traverse(val[i], seen); }\n    } else {\n      keys = Object.keys(val);\n      i = keys.length;\n      while (i--) { _traverse(val[keys[i]], seen); }\n    }\n  }\n\n  /*  */\n\n  var normalizeEvent = cached(function (name) {\n    var passive = name.charAt(0) === '&';\n    name = passive ? name.slice(1) : name;\n    var once$$1 = name.charAt(0) === '~'; // Prefixed last, checked first\n    name = once$$1 ? name.slice(1) : name;\n    var capture = name.charAt(0) === '!';\n    name = capture ? name.slice(1) : name;\n    return {\n      name: name,\n      once: once$$1,\n      capture: capture,\n      passive: passive\n    }\n  });\n\n  function createFnInvoker (fns, vm) {\n    function invoker () {\n      var arguments$1 = arguments;\n\n      var fns = invoker.fns;\n      if (Array.isArray(fns)) {\n        var cloned = fns.slice();\n        for (var i = 0; i < cloned.length; i++) {\n          invokeWithErrorHandling(cloned[i], null, arguments$1, vm, \"v-on handler\");\n        }\n      } else {\n        // return handler return value for single handlers\n        return invokeWithErrorHandling(fns, null, arguments, vm, \"v-on handler\")\n      }\n    }\n    invoker.fns = fns;\n    return invoker\n  }\n\n  function updateListeners (\n    on,\n    oldOn,\n    add,\n    remove$$1,\n    createOnceHandler,\n    vm\n  ) {\n    var name, def$$1, cur, old, event;\n    for (name in on) {\n      def$$1 = cur = on[name];\n      old = oldOn[name];\n      event = normalizeEvent(name);\n      if (isUndef(cur)) {\n        warn(\n          \"Invalid handler for event \\\"\" + (event.name) + \"\\\": got \" + String(cur),\n          vm\n        );\n      } else if (isUndef(old)) {\n        if (isUndef(cur.fns)) {\n          cur = on[name] = createFnInvoker(cur, vm);\n        }\n        if (isTrue(event.once)) {\n          cur = on[name] = createOnceHandler(event.name, cur, event.capture);\n        }\n        add(event.name, cur, event.capture, event.passive, event.params);\n      } else if (cur !== old) {\n        old.fns = cur;\n        on[name] = old;\n      }\n    }\n    for (name in oldOn) {\n      if (isUndef(on[name])) {\n        event = normalizeEvent(name);\n        remove$$1(event.name, oldOn[name], event.capture);\n      }\n    }\n  }\n\n  /*  */\n\n  function mergeVNodeHook (def, hookKey, hook) {\n    if (def instanceof VNode) {\n      def = def.data.hook || (def.data.hook = {});\n    }\n    var invoker;\n    var oldHook = def[hookKey];\n\n    function wrappedHook () {\n      hook.apply(this, arguments);\n      // important: remove merged hook to ensure it's called only once\n      // and prevent memory leak\n      remove(invoker.fns, wrappedHook);\n    }\n\n    if (isUndef(oldHook)) {\n      // no existing hook\n      invoker = createFnInvoker([wrappedHook]);\n    } else {\n      /* istanbul ignore if */\n      if (isDef(oldHook.fns) && isTrue(oldHook.merged)) {\n        // already a merged invoker\n        invoker = oldHook;\n        invoker.fns.push(wrappedHook);\n      } else {\n        // existing plain hook\n        invoker = createFnInvoker([oldHook, wrappedHook]);\n      }\n    }\n\n    invoker.merged = true;\n    def[hookKey] = invoker;\n  }\n\n  /*  */\n\n  function extractPropsFromVNodeData (\n    data,\n    Ctor,\n    tag\n  ) {\n    // we are only extracting raw values here.\n    // validation and default values are handled in the child\n    // component itself.\n    var propOptions = Ctor.options.props;\n    if (isUndef(propOptions)) {\n      return\n    }\n    var res = {};\n    var attrs = data.attrs;\n    var props = data.props;\n    if (isDef(attrs) || isDef(props)) {\n      for (var key in propOptions) {\n        var altKey = hyphenate(key);\n        {\n          var keyInLowerCase = key.toLowerCase();\n          if (\n            key !== keyInLowerCase &&\n            attrs && hasOwn(attrs, keyInLowerCase)\n          ) {\n            tip(\n              \"Prop \\\"\" + keyInLowerCase + \"\\\" is passed to component \" +\n              (formatComponentName(tag || Ctor)) + \", but the declared prop name is\" +\n              \" \\\"\" + key + \"\\\". \" +\n              \"Note that HTML attributes are case-insensitive and camelCased \" +\n              \"props need to use their kebab-case equivalents when using in-DOM \" +\n              \"templates. You should probably use \\\"\" + altKey + \"\\\" instead of \\\"\" + key + \"\\\".\"\n            );\n          }\n        }\n        checkProp(res, props, key, altKey, true) ||\n        checkProp(res, attrs, key, altKey, false);\n      }\n    }\n    return res\n  }\n\n  function checkProp (\n    res,\n    hash,\n    key,\n    altKey,\n    preserve\n  ) {\n    if (isDef(hash)) {\n      if (hasOwn(hash, key)) {\n        res[key] = hash[key];\n        if (!preserve) {\n          delete hash[key];\n        }\n        return true\n      } else if (hasOwn(hash, altKey)) {\n        res[key] = hash[altKey];\n        if (!preserve) {\n          delete hash[altKey];\n        }\n        return true\n      }\n    }\n    return false\n  }\n\n  /*  */\n\n  // The template compiler attempts to minimize the need for normalization by\n  // statically analyzing the template at compile time.\n  //\n  // For plain HTML markup, normalization can be completely skipped because the\n  // generated render function is guaranteed to return Array<VNode>. There are\n  // two cases where extra normalization is needed:\n\n  // 1. When the children contains components - because a functional component\n  // may return an Array instead of a single root. In this case, just a simple\n  // normalization is needed - if any child is an Array, we flatten the whole\n  // thing with Array.prototype.concat. It is guaranteed to be only 1-level deep\n  // because functional components already normalize their own children.\n  function simpleNormalizeChildren (children) {\n    for (var i = 0; i < children.length; i++) {\n      if (Array.isArray(children[i])) {\n        return Array.prototype.concat.apply([], children)\n      }\n    }\n    return children\n  }\n\n  // 2. When the children contains constructs that always generated nested Arrays,\n  // e.g. <template>, <slot>, v-for, or when the children is provided by user\n  // with hand-written render functions / JSX. In such cases a full normalization\n  // is needed to cater to all possible types of children values.\n  function normalizeChildren (children) {\n    return isPrimitive(children)\n      ? [createTextVNode(children)]\n      : Array.isArray(children)\n        ? normalizeArrayChildren(children)\n        : undefined\n  }\n\n  function isTextNode (node) {\n    return isDef(node) && isDef(node.text) && isFalse(node.isComment)\n  }\n\n  function normalizeArrayChildren (children, nestedIndex) {\n    var res = [];\n    var i, c, lastIndex, last;\n    for (i = 0; i < children.length; i++) {\n      c = children[i];\n      if (isUndef(c) || typeof c === 'boolean') { continue }\n      lastIndex = res.length - 1;\n      last = res[lastIndex];\n      //  nested\n      if (Array.isArray(c)) {\n        if (c.length > 0) {\n          c = normalizeArrayChildren(c, ((nestedIndex || '') + \"_\" + i));\n          // merge adjacent text nodes\n          if (isTextNode(c[0]) && isTextNode(last)) {\n            res[lastIndex] = createTextVNode(last.text + (c[0]).text);\n            c.shift();\n          }\n          res.push.apply(res, c);\n        }\n      } else if (isPrimitive(c)) {\n        if (isTextNode(last)) {\n          // merge adjacent text nodes\n          // this is necessary for SSR hydration because text nodes are\n          // essentially merged when rendered to HTML strings\n          res[lastIndex] = createTextVNode(last.text + c);\n        } else if (c !== '') {\n          // convert primitive to vnode\n          res.push(createTextVNode(c));\n        }\n      } else {\n        if (isTextNode(c) && isTextNode(last)) {\n          // merge adjacent text nodes\n          res[lastIndex] = createTextVNode(last.text + c.text);\n        } else {\n          // default key for nested array children (likely generated by v-for)\n          if (isTrue(children._isVList) &&\n            isDef(c.tag) &&\n            isUndef(c.key) &&\n            isDef(nestedIndex)) {\n            c.key = \"__vlist\" + nestedIndex + \"_\" + i + \"__\";\n          }\n          res.push(c);\n        }\n      }\n    }\n    return res\n  }\n\n  /*  */\n\n  function initProvide (vm) {\n    var provide = vm.$options.provide;\n    if (provide) {\n      vm._provided = typeof provide === 'function'\n        ? provide.call(vm)\n        : provide;\n    }\n  }\n\n  function initInjections (vm) {\n    var result = resolveInject(vm.$options.inject, vm);\n    if (result) {\n      toggleObserving(false);\n      Object.keys(result).forEach(function (key) {\n        /* istanbul ignore else */\n        {\n          defineReactive$$1(vm, key, result[key], function () {\n            warn(\n              \"Avoid mutating an injected value directly since the changes will be \" +\n              \"overwritten whenever the provided component re-renders. \" +\n              \"injection being mutated: \\\"\" + key + \"\\\"\",\n              vm\n            );\n          });\n        }\n      });\n      toggleObserving(true);\n    }\n  }\n\n  function resolveInject (inject, vm) {\n    if (inject) {\n      // inject is :any because flow is not smart enough to figure out cached\n      var result = Object.create(null);\n      var keys = hasSymbol\n        ? Reflect.ownKeys(inject)\n        : Object.keys(inject);\n\n      for (var i = 0; i < keys.length; i++) {\n        var key = keys[i];\n        // #6574 in case the inject object is observed...\n        if (key === '__ob__') { continue }\n        var provideKey = inject[key].from;\n        var source = vm;\n        while (source) {\n          if (source._provided && hasOwn(source._provided, provideKey)) {\n            result[key] = source._provided[provideKey];\n            break\n          }\n          source = source.$parent;\n        }\n        if (!source) {\n          if ('default' in inject[key]) {\n            var provideDefault = inject[key].default;\n            result[key] = typeof provideDefault === 'function'\n              ? provideDefault.call(vm)\n              : provideDefault;\n          } else {\n            warn((\"Injection \\\"\" + key + \"\\\" not found\"), vm);\n          }\n        }\n      }\n      return result\n    }\n  }\n\n  /*  */\n\n\n\n  /**\n   * Runtime helper for resolving raw children VNodes into a slot object.\n   */\n  function resolveSlots (\n    children,\n    context\n  ) {\n    if (!children || !children.length) {\n      return {}\n    }\n    var slots = {};\n    for (var i = 0, l = children.length; i < l; i++) {\n      var child = children[i];\n      var data = child.data;\n      // remove slot attribute if the node is resolved as a Vue slot node\n      if (data && data.attrs && data.attrs.slot) {\n        delete data.attrs.slot;\n      }\n      // named slots should only be respected if the vnode was rendered in the\n      // same context.\n      if ((child.context === context || child.fnContext === context) &&\n        data && data.slot != null\n      ) {\n        var name = data.slot;\n        var slot = (slots[name] || (slots[name] = []));\n        if (child.tag === 'template') {\n          slot.push.apply(slot, child.children || []);\n        } else {\n          slot.push(child);\n        }\n      } else {\n        (slots.default || (slots.default = [])).push(child);\n      }\n    }\n    // ignore slots that contains only whitespace\n    for (var name$1 in slots) {\n      if (slots[name$1].every(isWhitespace)) {\n        delete slots[name$1];\n      }\n    }\n    return slots\n  }\n\n  function isWhitespace (node) {\n    return (node.isComment && !node.asyncFactory) || node.text === ' '\n  }\n\n  /*  */\n\n  function normalizeScopedSlots (\n    slots,\n    normalSlots,\n    prevSlots\n  ) {\n    var res;\n    var hasNormalSlots = Object.keys(normalSlots).length > 0;\n    var isStable = slots ? !!slots.$stable : !hasNormalSlots;\n    var key = slots && slots.$key;\n    if (!slots) {\n      res = {};\n    } else if (slots._normalized) {\n      // fast path 1: child component re-render only, parent did not change\n      return slots._normalized\n    } else if (\n      isStable &&\n      prevSlots &&\n      prevSlots !== emptyObject &&\n      key === prevSlots.$key &&\n      !hasNormalSlots &&\n      !prevSlots.$hasNormal\n    ) {\n      // fast path 2: stable scoped slots w/ no normal slots to proxy,\n      // only need to normalize once\n      return prevSlots\n    } else {\n      res = {};\n      for (var key$1 in slots) {\n        if (slots[key$1] && key$1[0] !== '$') {\n          res[key$1] = normalizeScopedSlot(normalSlots, key$1, slots[key$1]);\n        }\n      }\n    }\n    // expose normal slots on scopedSlots\n    for (var key$2 in normalSlots) {\n      if (!(key$2 in res)) {\n        res[key$2] = proxyNormalSlot(normalSlots, key$2);\n      }\n    }\n    // avoriaz seems to mock a non-extensible $scopedSlots object\n    // and when that is passed down this would cause an error\n    if (slots && Object.isExtensible(slots)) {\n      (slots)._normalized = res;\n    }\n    def(res, '$stable', isStable);\n    def(res, '$key', key);\n    def(res, '$hasNormal', hasNormalSlots);\n    return res\n  }\n\n  function normalizeScopedSlot(normalSlots, key, fn) {\n    var normalized = function () {\n      var res = arguments.length ? fn.apply(null, arguments) : fn({});\n      res = res && typeof res === 'object' && !Array.isArray(res)\n        ? [res] // single vnode\n        : normalizeChildren(res);\n      return res && (\n        res.length === 0 ||\n        (res.length === 1 && res[0].isComment) // #9658\n      ) ? undefined\n        : res\n    };\n    // this is a slot using the new v-slot syntax without scope. although it is\n    // compiled as a scoped slot, render fn users would expect it to be present\n    // on this.$slots because the usage is semantically a normal slot.\n    if (fn.proxy) {\n      Object.defineProperty(normalSlots, key, {\n        get: normalized,\n        enumerable: true,\n        configurable: true\n      });\n    }\n    return normalized\n  }\n\n  function proxyNormalSlot(slots, key) {\n    return function () { return slots[key]; }\n  }\n\n  /*  */\n\n  /**\n   * Runtime helper for rendering v-for lists.\n   */\n  function renderList (\n    val,\n    render\n  ) {\n    var ret, i, l, keys, key;\n    if (Array.isArray(val) || typeof val === 'string') {\n      ret = new Array(val.length);\n      for (i = 0, l = val.length; i < l; i++) {\n        ret[i] = render(val[i], i);\n      }\n    } else if (typeof val === 'number') {\n      ret = new Array(val);\n      for (i = 0; i < val; i++) {\n        ret[i] = render(i + 1, i);\n      }\n    } else if (isObject(val)) {\n      if (hasSymbol && val[Symbol.iterator]) {\n        ret = [];\n        var iterator = val[Symbol.iterator]();\n        var result = iterator.next();\n        while (!result.done) {\n          ret.push(render(result.value, ret.length));\n          result = iterator.next();\n        }\n      } else {\n        keys = Object.keys(val);\n        ret = new Array(keys.length);\n        for (i = 0, l = keys.length; i < l; i++) {\n          key = keys[i];\n          ret[i] = render(val[key], key, i);\n        }\n      }\n    }\n    if (!isDef(ret)) {\n      ret = [];\n    }\n    (ret)._isVList = true;\n    return ret\n  }\n\n  /*  */\n\n  /**\n   * Runtime helper for rendering <slot>\n   */\n  function renderSlot (\n    name,\n    fallback,\n    props,\n    bindObject\n  ) {\n    var scopedSlotFn = this.$scopedSlots[name];\n    var nodes;\n    if (scopedSlotFn) { // scoped slot\n      props = props || {};\n      if (bindObject) {\n        if (!isObject(bindObject)) {\n          warn(\n            'slot v-bind without argument expects an Object',\n            this\n          );\n        }\n        props = extend(extend({}, bindObject), props);\n      }\n      nodes = scopedSlotFn(props) || fallback;\n    } else {\n      nodes = this.$slots[name] || fallback;\n    }\n\n    var target = props && props.slot;\n    if (target) {\n      return this.$createElement('template', { slot: target }, nodes)\n    } else {\n      return nodes\n    }\n  }\n\n  /*  */\n\n  /**\n   * Runtime helper for resolving filters\n   */\n  function resolveFilter (id) {\n    return resolveAsset(this.$options, 'filters', id, true) || identity\n  }\n\n  /*  */\n\n  function isKeyNotMatch (expect, actual) {\n    if (Array.isArray(expect)) {\n      return expect.indexOf(actual) === -1\n    } else {\n      return expect !== actual\n    }\n  }\n\n  /**\n   * Runtime helper for checking keyCodes from config.\n   * exposed as Vue.prototype._k\n   * passing in eventKeyName as last argument separately for backwards compat\n   */\n  function checkKeyCodes (\n    eventKeyCode,\n    key,\n    builtInKeyCode,\n    eventKeyName,\n    builtInKeyName\n  ) {\n    var mappedKeyCode = config.keyCodes[key] || builtInKeyCode;\n    if (builtInKeyName && eventKeyName && !config.keyCodes[key]) {\n      return isKeyNotMatch(builtInKeyName, eventKeyName)\n    } else if (mappedKeyCode) {\n      return isKeyNotMatch(mappedKeyCode, eventKeyCode)\n    } else if (eventKeyName) {\n      return hyphenate(eventKeyName) !== key\n    }\n  }\n\n  /*  */\n\n  /**\n   * Runtime helper for merging v-bind=\"object\" into a VNode's data.\n   */\n  function bindObjectProps (\n    data,\n    tag,\n    value,\n    asProp,\n    isSync\n  ) {\n    if (value) {\n      if (!isObject(value)) {\n        warn(\n          'v-bind without argument expects an Object or Array value',\n          this\n        );\n      } else {\n        if (Array.isArray(value)) {\n          value = toObject(value);\n        }\n        var hash;\n        var loop = function ( key ) {\n          if (\n            key === 'class' ||\n            key === 'style' ||\n            isReservedAttribute(key)\n          ) {\n            hash = data;\n          } else {\n            var type = data.attrs && data.attrs.type;\n            hash = asProp || config.mustUseProp(tag, type, key)\n              ? data.domProps || (data.domProps = {})\n              : data.attrs || (data.attrs = {});\n          }\n          var camelizedKey = camelize(key);\n          var hyphenatedKey = hyphenate(key);\n          if (!(camelizedKey in hash) && !(hyphenatedKey in hash)) {\n            hash[key] = value[key];\n\n            if (isSync) {\n              var on = data.on || (data.on = {});\n              on[(\"update:\" + key)] = function ($event) {\n                value[key] = $event;\n              };\n            }\n          }\n        };\n\n        for (var key in value) loop( key );\n      }\n    }\n    return data\n  }\n\n  /*  */\n\n  /**\n   * Runtime helper for rendering static trees.\n   */\n  function renderStatic (\n    index,\n    isInFor\n  ) {\n    var cached = this._staticTrees || (this._staticTrees = []);\n    var tree = cached[index];\n    // if has already-rendered static tree and not inside v-for,\n    // we can reuse the same tree.\n    if (tree && !isInFor) {\n      return tree\n    }\n    // otherwise, render a fresh tree.\n    tree = cached[index] = this.$options.staticRenderFns[index].call(\n      this._renderProxy,\n      null,\n      this // for render fns generated for functional component templates\n    );\n    markStatic(tree, (\"__static__\" + index), false);\n    return tree\n  }\n\n  /**\n   * Runtime helper for v-once.\n   * Effectively it means marking the node as static with a unique key.\n   */\n  function markOnce (\n    tree,\n    index,\n    key\n  ) {\n    markStatic(tree, (\"__once__\" + index + (key ? (\"_\" + key) : \"\")), true);\n    return tree\n  }\n\n  function markStatic (\n    tree,\n    key,\n    isOnce\n  ) {\n    if (Array.isArray(tree)) {\n      for (var i = 0; i < tree.length; i++) {\n        if (tree[i] && typeof tree[i] !== 'string') {\n          markStaticNode(tree[i], (key + \"_\" + i), isOnce);\n        }\n      }\n    } else {\n      markStaticNode(tree, key, isOnce);\n    }\n  }\n\n  function markStaticNode (node, key, isOnce) {\n    node.isStatic = true;\n    node.key = key;\n    node.isOnce = isOnce;\n  }\n\n  /*  */\n\n  function bindObjectListeners (data, value) {\n    if (value) {\n      if (!isPlainObject(value)) {\n        warn(\n          'v-on without argument expects an Object value',\n          this\n        );\n      } else {\n        var on = data.on = data.on ? extend({}, data.on) : {};\n        for (var key in value) {\n          var existing = on[key];\n          var ours = value[key];\n          on[key] = existing ? [].concat(existing, ours) : ours;\n        }\n      }\n    }\n    return data\n  }\n\n  /*  */\n\n  function resolveScopedSlots (\n    fns, // see flow/vnode\n    res,\n    // the following are added in 2.6\n    hasDynamicKeys,\n    contentHashKey\n  ) {\n    res = res || { $stable: !hasDynamicKeys };\n    for (var i = 0; i < fns.length; i++) {\n      var slot = fns[i];\n      if (Array.isArray(slot)) {\n        resolveScopedSlots(slot, res, hasDynamicKeys);\n      } else if (slot) {\n        // marker for reverse proxying v-slot without scope on this.$slots\n        if (slot.proxy) {\n          slot.fn.proxy = true;\n        }\n        res[slot.key] = slot.fn;\n      }\n    }\n    if (contentHashKey) {\n      (res).$key = contentHashKey;\n    }\n    return res\n  }\n\n  /*  */\n\n  function bindDynamicKeys (baseObj, values) {\n    for (var i = 0; i < values.length; i += 2) {\n      var key = values[i];\n      if (typeof key === 'string' && key) {\n        baseObj[values[i]] = values[i + 1];\n      } else if (key !== '' && key !== null) {\n        // null is a special value for explicitly removing a binding\n        warn(\n          (\"Invalid value for dynamic directive argument (expected string or null): \" + key),\n          this\n        );\n      }\n    }\n    return baseObj\n  }\n\n  // helper to dynamically append modifier runtime markers to event names.\n  // ensure only append when value is already string, otherwise it will be cast\n  // to string and cause the type check to miss.\n  function prependModifier (value, symbol) {\n    return typeof value === 'string' ? symbol + value : value\n  }\n\n  /*  */\n\n  function installRenderHelpers (target) {\n    target._o = markOnce;\n    target._n = toNumber;\n    target._s = toString;\n    target._l = renderList;\n    target._t = renderSlot;\n    target._q = looseEqual;\n    target._i = looseIndexOf;\n    target._m = renderStatic;\n    target._f = resolveFilter;\n    target._k = checkKeyCodes;\n    target._b = bindObjectProps;\n    target._v = createTextVNode;\n    target._e = createEmptyVNode;\n    target._u = resolveScopedSlots;\n    target._g = bindObjectListeners;\n    target._d = bindDynamicKeys;\n    target._p = prependModifier;\n  }\n\n  /*  */\n\n  function FunctionalRenderContext (\n    data,\n    props,\n    children,\n    parent,\n    Ctor\n  ) {\n    var this$1 = this;\n\n    var options = Ctor.options;\n    // ensure the createElement function in functional components\n    // gets a unique context - this is necessary for correct named slot check\n    var contextVm;\n    if (hasOwn(parent, '_uid')) {\n      contextVm = Object.create(parent);\n      // $flow-disable-line\n      contextVm._original = parent;\n    } else {\n      // the context vm passed in is a functional context as well.\n      // in this case we want to make sure we are able to get a hold to the\n      // real context instance.\n      contextVm = parent;\n      // $flow-disable-line\n      parent = parent._original;\n    }\n    var isCompiled = isTrue(options._compiled);\n    var needNormalization = !isCompiled;\n\n    this.data = data;\n    this.props = props;\n    this.children = children;\n    this.parent = parent;\n    this.listeners = data.on || emptyObject;\n    this.injections = resolveInject(options.inject, parent);\n    this.slots = function () {\n      if (!this$1.$slots) {\n        normalizeScopedSlots(\n          data.scopedSlots,\n          this$1.$slots = resolveSlots(children, parent)\n        );\n      }\n      return this$1.$slots\n    };\n\n    Object.defineProperty(this, 'scopedSlots', ({\n      enumerable: true,\n      get: function get () {\n        return normalizeScopedSlots(data.scopedSlots, this.slots())\n      }\n    }));\n\n    // support for compiled functional template\n    if (isCompiled) {\n      // exposing $options for renderStatic()\n      this.$options = options;\n      // pre-resolve slots for renderSlot()\n      this.$slots = this.slots();\n      this.$scopedSlots = normalizeScopedSlots(data.scopedSlots, this.$slots);\n    }\n\n    if (options._scopeId) {\n      this._c = function (a, b, c, d) {\n        var vnode = createElement(contextVm, a, b, c, d, needNormalization);\n        if (vnode && !Array.isArray(vnode)) {\n          vnode.fnScopeId = options._scopeId;\n          vnode.fnContext = parent;\n        }\n        return vnode\n      };\n    } else {\n      this._c = function (a, b, c, d) { return createElement(contextVm, a, b, c, d, needNormalization); };\n    }\n  }\n\n  installRenderHelpers(FunctionalRenderContext.prototype);\n\n  function createFunctionalComponent (\n    Ctor,\n    propsData,\n    data,\n    contextVm,\n    children\n  ) {\n    var options = Ctor.options;\n    var props = {};\n    var propOptions = options.props;\n    if (isDef(propOptions)) {\n      for (var key in propOptions) {\n        props[key] = validateProp(key, propOptions, propsData || emptyObject);\n      }\n    } else {\n      if (isDef(data.attrs)) { mergeProps(props, data.attrs); }\n      if (isDef(data.props)) { mergeProps(props, data.props); }\n    }\n\n    var renderContext = new FunctionalRenderContext(\n      data,\n      props,\n      children,\n      contextVm,\n      Ctor\n    );\n\n    var vnode = options.render.call(null, renderContext._c, renderContext);\n\n    if (vnode instanceof VNode) {\n      return cloneAndMarkFunctionalResult(vnode, data, renderContext.parent, options, renderContext)\n    } else if (Array.isArray(vnode)) {\n      var vnodes = normalizeChildren(vnode) || [];\n      var res = new Array(vnodes.length);\n      for (var i = 0; i < vnodes.length; i++) {\n        res[i] = cloneAndMarkFunctionalResult(vnodes[i], data, renderContext.parent, options, renderContext);\n      }\n      return res\n    }\n  }\n\n  function cloneAndMarkFunctionalResult (vnode, data, contextVm, options, renderContext) {\n    // #7817 clone node before setting fnContext, otherwise if the node is reused\n    // (e.g. it was from a cached normal slot) the fnContext causes named slots\n    // that should not be matched to match.\n    var clone = cloneVNode(vnode);\n    clone.fnContext = contextVm;\n    clone.fnOptions = options;\n    {\n      (clone.devtoolsMeta = clone.devtoolsMeta || {}).renderContext = renderContext;\n    }\n    if (data.slot) {\n      (clone.data || (clone.data = {})).slot = data.slot;\n    }\n    return clone\n  }\n\n  function mergeProps (to, from) {\n    for (var key in from) {\n      to[camelize(key)] = from[key];\n    }\n  }\n\n  /*  */\n\n  /*  */\n\n  /*  */\n\n  /*  */\n\n  // inline hooks to be invoked on component VNodes during patch\n  var componentVNodeHooks = {\n    init: function init (vnode, hydrating) {\n      if (\n        vnode.componentInstance &&\n        !vnode.componentInstance._isDestroyed &&\n        vnode.data.keepAlive\n      ) {\n        // kept-alive components, treat as a patch\n        var mountedNode = vnode; // work around flow\n        componentVNodeHooks.prepatch(mountedNode, mountedNode);\n      } else {\n        var child = vnode.componentInstance = createComponentInstanceForVnode(\n          vnode,\n          activeInstance\n        );\n        child.$mount(hydrating ? vnode.elm : undefined, hydrating);\n      }\n    },\n\n    prepatch: function prepatch (oldVnode, vnode) {\n      var options = vnode.componentOptions;\n      var child = vnode.componentInstance = oldVnode.componentInstance;\n      updateChildComponent(\n        child,\n        options.propsData, // updated props\n        options.listeners, // updated listeners\n        vnode, // new parent vnode\n        options.children // new children\n      );\n    },\n\n    insert: function insert (vnode) {\n      var context = vnode.context;\n      var componentInstance = vnode.componentInstance;\n      if (!componentInstance._isMounted) {\n        componentInstance._isMounted = true;\n        callHook(componentInstance, 'mounted');\n      }\n      if (vnode.data.keepAlive) {\n        if (context._isMounted) {\n          // vue-router#1212\n          // During updates, a kept-alive component's child components may\n          // change, so directly walking the tree here may call activated hooks\n          // on incorrect children. Instead we push them into a queue which will\n          // be processed after the whole patch process ended.\n          queueActivatedComponent(componentInstance);\n        } else {\n          activateChildComponent(componentInstance, true /* direct */);\n        }\n      }\n    },\n\n    destroy: function destroy (vnode) {\n      var componentInstance = vnode.componentInstance;\n      if (!componentInstance._isDestroyed) {\n        if (!vnode.data.keepAlive) {\n          componentInstance.$destroy();\n        } else {\n          deactivateChildComponent(componentInstance, true /* direct */);\n        }\n      }\n    }\n  };\n\n  var hooksToMerge = Object.keys(componentVNodeHooks);\n\n  function createComponent (\n    Ctor,\n    data,\n    context,\n    children,\n    tag\n  ) {\n    if (isUndef(Ctor)) {\n      return\n    }\n\n    var baseCtor = context.$options._base;\n\n    // plain options object: turn it into a constructor\n    if (isObject(Ctor)) {\n      Ctor = baseCtor.extend(Ctor);\n    }\n\n    // if at this stage it's not a constructor or an async component factory,\n    // reject.\n    if (typeof Ctor !== 'function') {\n      {\n        warn((\"Invalid Component definition: \" + (String(Ctor))), context);\n      }\n      return\n    }\n\n    // async component\n    var asyncFactory;\n    if (isUndef(Ctor.cid)) {\n      asyncFactory = Ctor;\n      Ctor = resolveAsyncComponent(asyncFactory, baseCtor);\n      if (Ctor === undefined) {\n        // return a placeholder node for async component, which is rendered\n        // as a comment node but preserves all the raw information for the node.\n        // the information will be used for async server-rendering and hydration.\n        return createAsyncPlaceholder(\n          asyncFactory,\n          data,\n          context,\n          children,\n          tag\n        )\n      }\n    }\n\n    data = data || {};\n\n    // resolve constructor options in case global mixins are applied after\n    // component constructor creation\n    resolveConstructorOptions(Ctor);\n\n    // transform component v-model data into props & events\n    if (isDef(data.model)) {\n      transformModel(Ctor.options, data);\n    }\n\n    // extract props\n    var propsData = extractPropsFromVNodeData(data, Ctor, tag);\n\n    // functional component\n    if (isTrue(Ctor.options.functional)) {\n      return createFunctionalComponent(Ctor, propsData, data, context, children)\n    }\n\n    // extract listeners, since these needs to be treated as\n    // child component listeners instead of DOM listeners\n    var listeners = data.on;\n    // replace with listeners with .native modifier\n    // so it gets processed during parent component patch.\n    data.on = data.nativeOn;\n\n    if (isTrue(Ctor.options.abstract)) {\n      // abstract components do not keep anything\n      // other than props & listeners & slot\n\n      // work around flow\n      var slot = data.slot;\n      data = {};\n      if (slot) {\n        data.slot = slot;\n      }\n    }\n\n    // install component management hooks onto the placeholder node\n    installComponentHooks(data);\n\n    // return a placeholder vnode\n    var name = Ctor.options.name || tag;\n    var vnode = new VNode(\n      (\"vue-component-\" + (Ctor.cid) + (name ? (\"-\" + name) : '')),\n      data, undefined, undefined, undefined, context,\n      { Ctor: Ctor, propsData: propsData, listeners: listeners, tag: tag, children: children },\n      asyncFactory\n    );\n\n    return vnode\n  }\n\n  function createComponentInstanceForVnode (\n    vnode, // we know it's MountedComponentVNode but flow doesn't\n    parent // activeInstance in lifecycle state\n  ) {\n    var options = {\n      _isComponent: true,\n      _parentVnode: vnode,\n      parent: parent\n    };\n    // check inline-template render functions\n    var inlineTemplate = vnode.data.inlineTemplate;\n    if (isDef(inlineTemplate)) {\n      options.render = inlineTemplate.render;\n      options.staticRenderFns = inlineTemplate.staticRenderFns;\n    }\n    return new vnode.componentOptions.Ctor(options)\n  }\n\n  function installComponentHooks (data) {\n    var hooks = data.hook || (data.hook = {});\n    for (var i = 0; i < hooksToMerge.length; i++) {\n      var key = hooksToMerge[i];\n      var existing = hooks[key];\n      var toMerge = componentVNodeHooks[key];\n      if (existing !== toMerge && !(existing && existing._merged)) {\n        hooks[key] = existing ? mergeHook$1(toMerge, existing) : toMerge;\n      }\n    }\n  }\n\n  function mergeHook$1 (f1, f2) {\n    var merged = function (a, b) {\n      // flow complains about extra args which is why we use any\n      f1(a, b);\n      f2(a, b);\n    };\n    merged._merged = true;\n    return merged\n  }\n\n  // transform component v-model info (value and callback) into\n  // prop and event handler respectively.\n  function transformModel (options, data) {\n    var prop = (options.model && options.model.prop) || 'value';\n    var event = (options.model && options.model.event) || 'input'\n    ;(data.attrs || (data.attrs = {}))[prop] = data.model.value;\n    var on = data.on || (data.on = {});\n    var existing = on[event];\n    var callback = data.model.callback;\n    if (isDef(existing)) {\n      if (\n        Array.isArray(existing)\n          ? existing.indexOf(callback) === -1\n          : existing !== callback\n      ) {\n        on[event] = [callback].concat(existing);\n      }\n    } else {\n      on[event] = callback;\n    }\n  }\n\n  /*  */\n\n  var SIMPLE_NORMALIZE = 1;\n  var ALWAYS_NORMALIZE = 2;\n\n  // wrapper function for providing a more flexible interface\n  // without getting yelled at by flow\n  function createElement (\n    context,\n    tag,\n    data,\n    children,\n    normalizationType,\n    alwaysNormalize\n  ) {\n    if (Array.isArray(data) || isPrimitive(data)) {\n      normalizationType = children;\n      children = data;\n      data = undefined;\n    }\n    if (isTrue(alwaysNormalize)) {\n      normalizationType = ALWAYS_NORMALIZE;\n    }\n    return _createElement(context, tag, data, children, normalizationType)\n  }\n\n  function _createElement (\n    context,\n    tag,\n    data,\n    children,\n    normalizationType\n  ) {\n    if (isDef(data) && isDef((data).__ob__)) {\n      warn(\n        \"Avoid using observed data object as vnode data: \" + (JSON.stringify(data)) + \"\\n\" +\n        'Always create fresh vnode data objects in each render!',\n        context\n      );\n      return createEmptyVNode()\n    }\n    // object syntax in v-bind\n    if (isDef(data) && isDef(data.is)) {\n      tag = data.is;\n    }\n    if (!tag) {\n      // in case of component :is set to falsy value\n      return createEmptyVNode()\n    }\n    // warn against non-primitive key\n    if (isDef(data) && isDef(data.key) && !isPrimitive(data.key)\n    ) {\n      {\n        warn(\n          'Avoid using non-primitive value as key, ' +\n          'use string/number value instead.',\n          context\n        );\n      }\n    }\n    // support single function children as default scoped slot\n    if (Array.isArray(children) &&\n      typeof children[0] === 'function'\n    ) {\n      data = data || {};\n      data.scopedSlots = { default: children[0] };\n      children.length = 0;\n    }\n    if (normalizationType === ALWAYS_NORMALIZE) {\n      children = normalizeChildren(children);\n    } else if (normalizationType === SIMPLE_NORMALIZE) {\n      children = simpleNormalizeChildren(children);\n    }\n    var vnode, ns;\n    if (typeof tag === 'string') {\n      var Ctor;\n      ns = (context.$vnode && context.$vnode.ns) || config.getTagNamespace(tag);\n      if (config.isReservedTag(tag)) {\n        // platform built-in elements\n        if (isDef(data) && isDef(data.nativeOn)) {\n          warn(\n            (\"The .native modifier for v-on is only valid on components but it was used on <\" + tag + \">.\"),\n            context\n          );\n        }\n        vnode = new VNode(\n          config.parsePlatformTagName(tag), data, children,\n          undefined, undefined, context\n        );\n      } else if ((!data || !data.pre) && isDef(Ctor = resolveAsset(context.$options, 'components', tag))) {\n        // component\n        vnode = createComponent(Ctor, data, context, children, tag);\n      } else {\n        // unknown or unlisted namespaced elements\n        // check at runtime because it may get assigned a namespace when its\n        // parent normalizes children\n        vnode = new VNode(\n          tag, data, children,\n          undefined, undefined, context\n        );\n      }\n    } else {\n      // direct component options / constructor\n      vnode = createComponent(tag, data, context, children);\n    }\n    if (Array.isArray(vnode)) {\n      return vnode\n    } else if (isDef(vnode)) {\n      if (isDef(ns)) { applyNS(vnode, ns); }\n      if (isDef(data)) { registerDeepBindings(data); }\n      return vnode\n    } else {\n      return createEmptyVNode()\n    }\n  }\n\n  function applyNS (vnode, ns, force) {\n    vnode.ns = ns;\n    if (vnode.tag === 'foreignObject') {\n      // use default namespace inside foreignObject\n      ns = undefined;\n      force = true;\n    }\n    if (isDef(vnode.children)) {\n      for (var i = 0, l = vnode.children.length; i < l; i++) {\n        var child = vnode.children[i];\n        if (isDef(child.tag) && (\n          isUndef(child.ns) || (isTrue(force) && child.tag !== 'svg'))) {\n          applyNS(child, ns, force);\n        }\n      }\n    }\n  }\n\n  // ref #5318\n  // necessary to ensure parent re-render when deep bindings like :style and\n  // :class are used on slot nodes\n  function registerDeepBindings (data) {\n    if (isObject(data.style)) {\n      traverse(data.style);\n    }\n    if (isObject(data.class)) {\n      traverse(data.class);\n    }\n  }\n\n  /*  */\n\n  function initRender (vm) {\n    vm._vnode = null; // the root of the child tree\n    vm._staticTrees = null; // v-once cached trees\n    var options = vm.$options;\n    var parentVnode = vm.$vnode = options._parentVnode; // the placeholder node in parent tree\n    var renderContext = parentVnode && parentVnode.context;\n    vm.$slots = resolveSlots(options._renderChildren, renderContext);\n    vm.$scopedSlots = emptyObject;\n    // bind the createElement fn to this instance\n    // so that we get proper render context inside it.\n    // args order: tag, data, children, normalizationType, alwaysNormalize\n    // internal version is used by render functions compiled from templates\n    vm._c = function (a, b, c, d) { return createElement(vm, a, b, c, d, false); };\n    // normalization is always applied for the public version, used in\n    // user-written render functions.\n    vm.$createElement = function (a, b, c, d) { return createElement(vm, a, b, c, d, true); };\n\n    // $attrs & $listeners are exposed for easier HOC creation.\n    // they need to be reactive so that HOCs using them are always updated\n    var parentData = parentVnode && parentVnode.data;\n\n    /* istanbul ignore else */\n    {\n      defineReactive$$1(vm, '$attrs', parentData && parentData.attrs || emptyObject, function () {\n        !isUpdatingChildComponent && warn(\"$attrs is readonly.\", vm);\n      }, true);\n      defineReactive$$1(vm, '$listeners', options._parentListeners || emptyObject, function () {\n        !isUpdatingChildComponent && warn(\"$listeners is readonly.\", vm);\n      }, true);\n    }\n  }\n\n  var currentRenderingInstance = null;\n\n  function renderMixin (Vue) {\n    // install runtime convenience helpers\n    installRenderHelpers(Vue.prototype);\n\n    Vue.prototype.$nextTick = function (fn) {\n      return nextTick(fn, this)\n    };\n\n    Vue.prototype._render = function () {\n      var vm = this;\n      var ref = vm.$options;\n      var render = ref.render;\n      var _parentVnode = ref._parentVnode;\n\n      if (_parentVnode) {\n        vm.$scopedSlots = normalizeScopedSlots(\n          _parentVnode.data.scopedSlots,\n          vm.$slots,\n          vm.$scopedSlots\n        );\n      }\n\n      // set parent vnode. this allows render functions to have access\n      // to the data on the placeholder node.\n      vm.$vnode = _parentVnode;\n      // render self\n      var vnode;\n      try {\n        // There's no need to maintain a stack because all render fns are called\n        // separately from one another. Nested component's render fns are called\n        // when parent component is patched.\n        currentRenderingInstance = vm;\n        vnode = render.call(vm._renderProxy, vm.$createElement);\n      } catch (e) {\n        handleError(e, vm, \"render\");\n        // return error render result,\n        // or previous vnode to prevent render error causing blank component\n        /* istanbul ignore else */\n        if (vm.$options.renderError) {\n          try {\n            vnode = vm.$options.renderError.call(vm._renderProxy, vm.$createElement, e);\n          } catch (e) {\n            handleError(e, vm, \"renderError\");\n            vnode = vm._vnode;\n          }\n        } else {\n          vnode = vm._vnode;\n        }\n      } finally {\n        currentRenderingInstance = null;\n      }\n      // if the returned array contains only a single node, allow it\n      if (Array.isArray(vnode) && vnode.length === 1) {\n        vnode = vnode[0];\n      }\n      // return empty vnode in case the render function errored out\n      if (!(vnode instanceof VNode)) {\n        if (Array.isArray(vnode)) {\n          warn(\n            'Multiple root nodes returned from render function. Render function ' +\n            'should return a single root node.',\n            vm\n          );\n        }\n        vnode = createEmptyVNode();\n      }\n      // set parent\n      vnode.parent = _parentVnode;\n      return vnode\n    };\n  }\n\n  /*  */\n\n  function ensureCtor (comp, base) {\n    if (\n      comp.__esModule ||\n      (hasSymbol && comp[Symbol.toStringTag] === 'Module')\n    ) {\n      comp = comp.default;\n    }\n    return isObject(comp)\n      ? base.extend(comp)\n      : comp\n  }\n\n  function createAsyncPlaceholder (\n    factory,\n    data,\n    context,\n    children,\n    tag\n  ) {\n    var node = createEmptyVNode();\n    node.asyncFactory = factory;\n    node.asyncMeta = { data: data, context: context, children: children, tag: tag };\n    return node\n  }\n\n  function resolveAsyncComponent (\n    factory,\n    baseCtor\n  ) {\n    if (isTrue(factory.error) && isDef(factory.errorComp)) {\n      return factory.errorComp\n    }\n\n    if (isDef(factory.resolved)) {\n      return factory.resolved\n    }\n\n    var owner = currentRenderingInstance;\n    if (owner && isDef(factory.owners) && factory.owners.indexOf(owner) === -1) {\n      // already pending\n      factory.owners.push(owner);\n    }\n\n    if (isTrue(factory.loading) && isDef(factory.loadingComp)) {\n      return factory.loadingComp\n    }\n\n    if (owner && !isDef(factory.owners)) {\n      var owners = factory.owners = [owner];\n      var sync = true;\n      var timerLoading = null;\n      var timerTimeout = null\n\n      ;(owner).$on('hook:destroyed', function () { return remove(owners, owner); });\n\n      var forceRender = function (renderCompleted) {\n        for (var i = 0, l = owners.length; i < l; i++) {\n          (owners[i]).$forceUpdate();\n        }\n\n        if (renderCompleted) {\n          owners.length = 0;\n          if (timerLoading !== null) {\n            clearTimeout(timerLoading);\n            timerLoading = null;\n          }\n          if (timerTimeout !== null) {\n            clearTimeout(timerTimeout);\n            timerTimeout = null;\n          }\n        }\n      };\n\n      var resolve = once(function (res) {\n        // cache resolved\n        factory.resolved = ensureCtor(res, baseCtor);\n        // invoke callbacks only if this is not a synchronous resolve\n        // (async resolves are shimmed as synchronous during SSR)\n        if (!sync) {\n          forceRender(true);\n        } else {\n          owners.length = 0;\n        }\n      });\n\n      var reject = once(function (reason) {\n        warn(\n          \"Failed to resolve async component: \" + (String(factory)) +\n          (reason ? (\"\\nReason: \" + reason) : '')\n        );\n        if (isDef(factory.errorComp)) {\n          factory.error = true;\n          forceRender(true);\n        }\n      });\n\n      var res = factory(resolve, reject);\n\n      if (isObject(res)) {\n        if (isPromise(res)) {\n          // () => Promise\n          if (isUndef(factory.resolved)) {\n            res.then(resolve, reject);\n          }\n        } else if (isPromise(res.component)) {\n          res.component.then(resolve, reject);\n\n          if (isDef(res.error)) {\n            factory.errorComp = ensureCtor(res.error, baseCtor);\n          }\n\n          if (isDef(res.loading)) {\n            factory.loadingComp = ensureCtor(res.loading, baseCtor);\n            if (res.delay === 0) {\n              factory.loading = true;\n            } else {\n              timerLoading = setTimeout(function () {\n                timerLoading = null;\n                if (isUndef(factory.resolved) && isUndef(factory.error)) {\n                  factory.loading = true;\n                  forceRender(false);\n                }\n              }, res.delay || 200);\n            }\n          }\n\n          if (isDef(res.timeout)) {\n            timerTimeout = setTimeout(function () {\n              timerTimeout = null;\n              if (isUndef(factory.resolved)) {\n                reject(\n                  \"timeout (\" + (res.timeout) + \"ms)\"\n                );\n              }\n            }, res.timeout);\n          }\n        }\n      }\n\n      sync = false;\n      // return in case resolved synchronously\n      return factory.loading\n        ? factory.loadingComp\n        : factory.resolved\n    }\n  }\n\n  /*  */\n\n  function isAsyncPlaceholder (node) {\n    return node.isComment && node.asyncFactory\n  }\n\n  /*  */\n\n  function getFirstComponentChild (children) {\n    if (Array.isArray(children)) {\n      for (var i = 0; i < children.length; i++) {\n        var c = children[i];\n        if (isDef(c) && (isDef(c.componentOptions) || isAsyncPlaceholder(c))) {\n          return c\n        }\n      }\n    }\n  }\n\n  /*  */\n\n  /*  */\n\n  function initEvents (vm) {\n    vm._events = Object.create(null);\n    vm._hasHookEvent = false;\n    // init parent attached events\n    var listeners = vm.$options._parentListeners;\n    if (listeners) {\n      updateComponentListeners(vm, listeners);\n    }\n  }\n\n  var target;\n\n  function add (event, fn) {\n    target.$on(event, fn);\n  }\n\n  function remove$1 (event, fn) {\n    target.$off(event, fn);\n  }\n\n  function createOnceHandler (event, fn) {\n    var _target = target;\n    return function onceHandler () {\n      var res = fn.apply(null, arguments);\n      if (res !== null) {\n        _target.$off(event, onceHandler);\n      }\n    }\n  }\n\n  function updateComponentListeners (\n    vm,\n    listeners,\n    oldListeners\n  ) {\n    target = vm;\n    updateListeners(listeners, oldListeners || {}, add, remove$1, createOnceHandler, vm);\n    target = undefined;\n  }\n\n  function eventsMixin (Vue) {\n    var hookRE = /^hook:/;\n    Vue.prototype.$on = function (event, fn) {\n      var vm = this;\n      if (Array.isArray(event)) {\n        for (var i = 0, l = event.length; i < l; i++) {\n          vm.$on(event[i], fn);\n        }\n      } else {\n        (vm._events[event] || (vm._events[event] = [])).push(fn);\n        // optimize hook:event cost by using a boolean flag marked at registration\n        // instead of a hash lookup\n        if (hookRE.test(event)) {\n          vm._hasHookEvent = true;\n        }\n      }\n      return vm\n    };\n\n    Vue.prototype.$once = function (event, fn) {\n      var vm = this;\n      function on () {\n        vm.$off(event, on);\n        fn.apply(vm, arguments);\n      }\n      on.fn = fn;\n      vm.$on(event, on);\n      return vm\n    };\n\n    Vue.prototype.$off = function (event, fn) {\n      var vm = this;\n      // all\n      if (!arguments.length) {\n        vm._events = Object.create(null);\n        return vm\n      }\n      // array of events\n      if (Array.isArray(event)) {\n        for (var i$1 = 0, l = event.length; i$1 < l; i$1++) {\n          vm.$off(event[i$1], fn);\n        }\n        return vm\n      }\n      // specific event\n      var cbs = vm._events[event];\n      if (!cbs) {\n        return vm\n      }\n      if (!fn) {\n        vm._events[event] = null;\n        return vm\n      }\n      // specific handler\n      var cb;\n      var i = cbs.length;\n      while (i--) {\n        cb = cbs[i];\n        if (cb === fn || cb.fn === fn) {\n          cbs.splice(i, 1);\n          break\n        }\n      }\n      return vm\n    };\n\n    Vue.prototype.$emit = function (event) {\n      var vm = this;\n      {\n        var lowerCaseEvent = event.toLowerCase();\n        if (lowerCaseEvent !== event && vm._events[lowerCaseEvent]) {\n          tip(\n            \"Event \\\"\" + lowerCaseEvent + \"\\\" is emitted in component \" +\n            (formatComponentName(vm)) + \" but the handler is registered for \\\"\" + event + \"\\\". \" +\n            \"Note that HTML attributes are case-insensitive and you cannot use \" +\n            \"v-on to listen to camelCase events when using in-DOM templates. \" +\n            \"You should probably use \\\"\" + (hyphenate(event)) + \"\\\" instead of \\\"\" + event + \"\\\".\"\n          );\n        }\n      }\n      var cbs = vm._events[event];\n      if (cbs) {\n        cbs = cbs.length > 1 ? toArray(cbs) : cbs;\n        var args = toArray(arguments, 1);\n        var info = \"event handler for \\\"\" + event + \"\\\"\";\n        for (var i = 0, l = cbs.length; i < l; i++) {\n          invokeWithErrorHandling(cbs[i], vm, args, vm, info);\n        }\n      }\n      return vm\n    };\n  }\n\n  /*  */\n\n  var activeInstance = null;\n  var isUpdatingChildComponent = false;\n\n  function setActiveInstance(vm) {\n    var prevActiveInstance = activeInstance;\n    activeInstance = vm;\n    return function () {\n      activeInstance = prevActiveInstance;\n    }\n  }\n\n  function initLifecycle (vm) {\n    var options = vm.$options;\n\n    // locate first non-abstract parent\n    var parent = options.parent;\n    if (parent && !options.abstract) {\n      while (parent.$options.abstract && parent.$parent) {\n        parent = parent.$parent;\n      }\n      parent.$children.push(vm);\n    }\n\n    vm.$parent = parent;\n    vm.$root = parent ? parent.$root : vm;\n\n    vm.$children = [];\n    vm.$refs = {};\n\n    vm._watcher = null;\n    vm._inactive = null;\n    vm._directInactive = false;\n    vm._isMounted = false;\n    vm._isDestroyed = false;\n    vm._isBeingDestroyed = false;\n  }\n\n  function lifecycleMixin (Vue) {\n    Vue.prototype._update = function (vnode, hydrating) {\n      var vm = this;\n      var prevEl = vm.$el;\n      var prevVnode = vm._vnode;\n      var restoreActiveInstance = setActiveInstance(vm);\n      vm._vnode = vnode;\n      // Vue.prototype.__patch__ is injected in entry points\n      // based on the rendering backend used.\n      if (!prevVnode) {\n        // initial render\n        vm.$el = vm.__patch__(vm.$el, vnode, hydrating, false /* removeOnly */);\n      } else {\n        // updates\n        vm.$el = vm.__patch__(prevVnode, vnode);\n      }\n      restoreActiveInstance();\n      // update __vue__ reference\n      if (prevEl) {\n        prevEl.__vue__ = null;\n      }\n      if (vm.$el) {\n        vm.$el.__vue__ = vm;\n      }\n      // if parent is an HOC, update its $el as well\n      if (vm.$vnode && vm.$parent && vm.$vnode === vm.$parent._vnode) {\n        vm.$parent.$el = vm.$el;\n      }\n      // updated hook is called by the scheduler to ensure that children are\n      // updated in a parent's updated hook.\n    };\n\n    Vue.prototype.$forceUpdate = function () {\n      var vm = this;\n      if (vm._watcher) {\n        vm._watcher.update();\n      }\n    };\n\n    Vue.prototype.$destroy = function () {\n      var vm = this;\n      if (vm._isBeingDestroyed) {\n        return\n      }\n      callHook(vm, 'beforeDestroy');\n      vm._isBeingDestroyed = true;\n      // remove self from parent\n      var parent = vm.$parent;\n      if (parent && !parent._isBeingDestroyed && !vm.$options.abstract) {\n        remove(parent.$children, vm);\n      }\n      // teardown watchers\n      if (vm._watcher) {\n        vm._watcher.teardown();\n      }\n      var i = vm._watchers.length;\n      while (i--) {\n        vm._watchers[i].teardown();\n      }\n      // remove reference from data ob\n      // frozen object may not have observer.\n      if (vm._data.__ob__) {\n        vm._data.__ob__.vmCount--;\n      }\n      // call the last hook...\n      vm._isDestroyed = true;\n      // invoke destroy hooks on current rendered tree\n      vm.__patch__(vm._vnode, null);\n      // fire destroyed hook\n      callHook(vm, 'destroyed');\n      // turn off all instance listeners.\n      vm.$off();\n      // remove __vue__ reference\n      if (vm.$el) {\n        vm.$el.__vue__ = null;\n      }\n      // release circular reference (#6759)\n      if (vm.$vnode) {\n        vm.$vnode.parent = null;\n      }\n    };\n  }\n\n  function mountComponent (\n    vm,\n    el,\n    hydrating\n  ) {\n    vm.$el = el;\n    if (!vm.$options.render) {\n      vm.$options.render = createEmptyVNode;\n      {\n        /* istanbul ignore if */\n        if ((vm.$options.template && vm.$options.template.charAt(0) !== '#') ||\n          vm.$options.el || el) {\n          warn(\n            'You are using the runtime-only build of Vue where the template ' +\n            'compiler is not available. Either pre-compile the templates into ' +\n            'render functions, or use the compiler-included build.',\n            vm\n          );\n        } else {\n          warn(\n            'Failed to mount component: template or render function not defined.',\n            vm\n          );\n        }\n      }\n    }\n    callHook(vm, 'beforeMount');\n\n    var updateComponent;\n    /* istanbul ignore if */\n    if (config.performance && mark) {\n      updateComponent = function () {\n        var name = vm._name;\n        var id = vm._uid;\n        var startTag = \"vue-perf-start:\" + id;\n        var endTag = \"vue-perf-end:\" + id;\n\n        mark(startTag);\n        var vnode = vm._render();\n        mark(endTag);\n        measure((\"vue \" + name + \" render\"), startTag, endTag);\n\n        mark(startTag);\n        vm._update(vnode, hydrating);\n        mark(endTag);\n        measure((\"vue \" + name + \" patch\"), startTag, endTag);\n      };\n    } else {\n      updateComponent = function () {\n        vm._update(vm._render(), hydrating);\n      };\n    }\n\n    // we set this to vm._watcher inside the watcher's constructor\n    // since the watcher's initial patch may call $forceUpdate (e.g. inside child\n    // component's mounted hook), which relies on vm._watcher being already defined\n    new Watcher(vm, updateComponent, noop, {\n      before: function before () {\n        if (vm._isMounted && !vm._isDestroyed) {\n          callHook(vm, 'beforeUpdate');\n        }\n      }\n    }, true /* isRenderWatcher */);\n    hydrating = false;\n\n    // manually mounted instance, call mounted on self\n    // mounted is called for render-created child components in its inserted hook\n    if (vm.$vnode == null) {\n      vm._isMounted = true;\n      callHook(vm, 'mounted');\n    }\n    return vm\n  }\n\n  function updateChildComponent (\n    vm,\n    propsData,\n    listeners,\n    parentVnode,\n    renderChildren\n  ) {\n    {\n      isUpdatingChildComponent = true;\n    }\n\n    // determine whether component has slot children\n    // we need to do this before overwriting $options._renderChildren.\n\n    // check if there are dynamic scopedSlots (hand-written or compiled but with\n    // dynamic slot names). Static scoped slots compiled from template has the\n    // \"$stable\" marker.\n    var newScopedSlots = parentVnode.data.scopedSlots;\n    var oldScopedSlots = vm.$scopedSlots;\n    var hasDynamicScopedSlot = !!(\n      (newScopedSlots && !newScopedSlots.$stable) ||\n      (oldScopedSlots !== emptyObject && !oldScopedSlots.$stable) ||\n      (newScopedSlots && vm.$scopedSlots.$key !== newScopedSlots.$key)\n    );\n\n    // Any static slot children from the parent may have changed during parent's\n    // update. Dynamic scoped slots may also have changed. In such cases, a forced\n    // update is necessary to ensure correctness.\n    var needsForceUpdate = !!(\n      renderChildren ||               // has new static slots\n      vm.$options._renderChildren ||  // has old static slots\n      hasDynamicScopedSlot\n    );\n\n    vm.$options._parentVnode = parentVnode;\n    vm.$vnode = parentVnode; // update vm's placeholder node without re-render\n\n    if (vm._vnode) { // update child tree's parent\n      vm._vnode.parent = parentVnode;\n    }\n    vm.$options._renderChildren = renderChildren;\n\n    // update $attrs and $listeners hash\n    // these are also reactive so they may trigger child update if the child\n    // used them during render\n    vm.$attrs = parentVnode.data.attrs || emptyObject;\n    vm.$listeners = listeners || emptyObject;\n\n    // update props\n    if (propsData && vm.$options.props) {\n      toggleObserving(false);\n      var props = vm._props;\n      var propKeys = vm.$options._propKeys || [];\n      for (var i = 0; i < propKeys.length; i++) {\n        var key = propKeys[i];\n        var propOptions = vm.$options.props; // wtf flow?\n        props[key] = validateProp(key, propOptions, propsData, vm);\n      }\n      toggleObserving(true);\n      // keep a copy of raw propsData\n      vm.$options.propsData = propsData;\n    }\n\n    // update listeners\n    listeners = listeners || emptyObject;\n    var oldListeners = vm.$options._parentListeners;\n    vm.$options._parentListeners = listeners;\n    updateComponentListeners(vm, listeners, oldListeners);\n\n    // resolve slots + force update if has children\n    if (needsForceUpdate) {\n      vm.$slots = resolveSlots(renderChildren, parentVnode.context);\n      vm.$forceUpdate();\n    }\n\n    {\n      isUpdatingChildComponent = false;\n    }\n  }\n\n  function isInInactiveTree (vm) {\n    while (vm && (vm = vm.$parent)) {\n      if (vm._inactive) { return true }\n    }\n    return false\n  }\n\n  function activateChildComponent (vm, direct) {\n    if (direct) {\n      vm._directInactive = false;\n      if (isInInactiveTree(vm)) {\n        return\n      }\n    } else if (vm._directInactive) {\n      return\n    }\n    if (vm._inactive || vm._inactive === null) {\n      vm._inactive = false;\n      for (var i = 0; i < vm.$children.length; i++) {\n        activateChildComponent(vm.$children[i]);\n      }\n      callHook(vm, 'activated');\n    }\n  }\n\n  function deactivateChildComponent (vm, direct) {\n    if (direct) {\n      vm._directInactive = true;\n      if (isInInactiveTree(vm)) {\n        return\n      }\n    }\n    if (!vm._inactive) {\n      vm._inactive = true;\n      for (var i = 0; i < vm.$children.length; i++) {\n        deactivateChildComponent(vm.$children[i]);\n      }\n      callHook(vm, 'deactivated');\n    }\n  }\n\n  function callHook (vm, hook) {\n    // #7573 disable dep collection when invoking lifecycle hooks\n    pushTarget();\n    var handlers = vm.$options[hook];\n    var info = hook + \" hook\";\n    if (handlers) {\n      for (var i = 0, j = handlers.length; i < j; i++) {\n        invokeWithErrorHandling(handlers[i], vm, null, vm, info);\n      }\n    }\n    if (vm._hasHookEvent) {\n      vm.$emit('hook:' + hook);\n    }\n    popTarget();\n  }\n\n  /*  */\n\n  var MAX_UPDATE_COUNT = 100;\n\n  var queue = [];\n  var activatedChildren = [];\n  var has = {};\n  var circular = {};\n  var waiting = false;\n  var flushing = false;\n  var index = 0;\n\n  /**\n   * Reset the scheduler's state.\n   */\n  function resetSchedulerState () {\n    index = queue.length = activatedChildren.length = 0;\n    has = {};\n    {\n      circular = {};\n    }\n    waiting = flushing = false;\n  }\n\n  // Async edge case #6566 requires saving the timestamp when event listeners are\n  // attached. However, calling performance.now() has a perf overhead especially\n  // if the page has thousands of event listeners. Instead, we take a timestamp\n  // every time the scheduler flushes and use that for all event listeners\n  // attached during that flush.\n  var currentFlushTimestamp = 0;\n\n  // Async edge case fix requires storing an event listener's attach timestamp.\n  var getNow = Date.now;\n\n  // Determine what event timestamp the browser is using. Annoyingly, the\n  // timestamp can either be hi-res (relative to page load) or low-res\n  // (relative to UNIX epoch), so in order to compare time we have to use the\n  // same timestamp type when saving the flush timestamp.\n  // All IE versions use low-res event timestamps, and have problematic clock\n  // implementations (#9632)\n  if (inBrowser && !isIE) {\n    var performance = window.performance;\n    if (\n      performance &&\n      typeof performance.now === 'function' &&\n      getNow() > document.createEvent('Event').timeStamp\n    ) {\n      // if the event timestamp, although evaluated AFTER the Date.now(), is\n      // smaller than it, it means the event is using a hi-res timestamp,\n      // and we need to use the hi-res version for event listener timestamps as\n      // well.\n      getNow = function () { return performance.now(); };\n    }\n  }\n\n  /**\n   * Flush both queues and run the watchers.\n   */\n  function flushSchedulerQueue () {\n    currentFlushTimestamp = getNow();\n    flushing = true;\n    var watcher, id;\n\n    // Sort queue before flush.\n    // This ensures that:\n    // 1. Components are updated from parent to child. (because parent is always\n    //    created before the child)\n    // 2. A component's user watchers are run before its render watcher (because\n    //    user watchers are created before the render watcher)\n    // 3. If a component is destroyed during a parent component's watcher run,\n    //    its watchers can be skipped.\n    queue.sort(function (a, b) { return a.id - b.id; });\n\n    // do not cache length because more watchers might be pushed\n    // as we run existing watchers\n    for (index = 0; index < queue.length; index++) {\n      watcher = queue[index];\n      if (watcher.before) {\n        watcher.before();\n      }\n      id = watcher.id;\n      has[id] = null;\n      watcher.run();\n      // in dev build, check and stop circular updates.\n      if (has[id] != null) {\n        circular[id] = (circular[id] || 0) + 1;\n        if (circular[id] > MAX_UPDATE_COUNT) {\n          warn(\n            'You may have an infinite update loop ' + (\n              watcher.user\n                ? (\"in watcher with expression \\\"\" + (watcher.expression) + \"\\\"\")\n                : \"in a component render function.\"\n            ),\n            watcher.vm\n          );\n          break\n        }\n      }\n    }\n\n    // keep copies of post queues before resetting state\n    var activatedQueue = activatedChildren.slice();\n    var updatedQueue = queue.slice();\n\n    resetSchedulerState();\n\n    // call component updated and activated hooks\n    callActivatedHooks(activatedQueue);\n    callUpdatedHooks(updatedQueue);\n\n    // devtool hook\n    /* istanbul ignore if */\n    if (devtools && config.devtools) {\n      devtools.emit('flush');\n    }\n  }\n\n  function callUpdatedHooks (queue) {\n    var i = queue.length;\n    while (i--) {\n      var watcher = queue[i];\n      var vm = watcher.vm;\n      if (vm._watcher === watcher && vm._isMounted && !vm._isDestroyed) {\n        callHook(vm, 'updated');\n      }\n    }\n  }\n\n  /**\n   * Queue a kept-alive component that was activated during patch.\n   * The queue will be processed after the entire tree has been patched.\n   */\n  function queueActivatedComponent (vm) {\n    // setting _inactive to false here so that a render function can\n    // rely on checking whether it's in an inactive tree (e.g. router-view)\n    vm._inactive = false;\n    activatedChildren.push(vm);\n  }\n\n  function callActivatedHooks (queue) {\n    for (var i = 0; i < queue.length; i++) {\n      queue[i]._inactive = true;\n      activateChildComponent(queue[i], true /* true */);\n    }\n  }\n\n  /**\n   * Push a watcher into the watcher queue.\n   * Jobs with duplicate IDs will be skipped unless it's\n   * pushed when the queue is being flushed.\n   */\n  function queueWatcher (watcher) {\n    var id = watcher.id;\n    if (has[id] == null) {\n      has[id] = true;\n      if (!flushing) {\n        queue.push(watcher);\n      } else {\n        // if already flushing, splice the watcher based on its id\n        // if already past its id, it will be run next immediately.\n        var i = queue.length - 1;\n        while (i > index && queue[i].id > watcher.id) {\n          i--;\n        }\n        queue.splice(i + 1, 0, watcher);\n      }\n      // queue the flush\n      if (!waiting) {\n        waiting = true;\n\n        if (!config.async) {\n          flushSchedulerQueue();\n          return\n        }\n        nextTick(flushSchedulerQueue);\n      }\n    }\n  }\n\n  /*  */\n\n\n\n  var uid$2 = 0;\n\n  /**\n   * A watcher parses an expression, collects dependencies,\n   * and fires callback when the expression value changes.\n   * This is used for both the $watch() api and directives.\n   */\n  var Watcher = function Watcher (\n    vm,\n    expOrFn,\n    cb,\n    options,\n    isRenderWatcher\n  ) {\n    this.vm = vm;\n    if (isRenderWatcher) {\n      vm._watcher = this;\n    }\n    vm._watchers.push(this);\n    // options\n    if (options) {\n      this.deep = !!options.deep;\n      this.user = !!options.user;\n      this.lazy = !!options.lazy;\n      this.sync = !!options.sync;\n      this.before = options.before;\n    } else {\n      this.deep = this.user = this.lazy = this.sync = false;\n    }\n    this.cb = cb;\n    this.id = ++uid$2; // uid for batching\n    this.active = true;\n    this.dirty = this.lazy; // for lazy watchers\n    this.deps = [];\n    this.newDeps = [];\n    this.depIds = new _Set();\n    this.newDepIds = new _Set();\n    this.expression = expOrFn.toString();\n    // parse expression for getter\n    if (typeof expOrFn === 'function') {\n      this.getter = expOrFn;\n    } else {\n      this.getter = parsePath(expOrFn);\n      if (!this.getter) {\n        this.getter = noop;\n        warn(\n          \"Failed watching path: \\\"\" + expOrFn + \"\\\" \" +\n          'Watcher only accepts simple dot-delimited paths. ' +\n          'For full control, use a function instead.',\n          vm\n        );\n      }\n    }\n    this.value = this.lazy\n      ? undefined\n      : this.get();\n  };\n\n  /**\n   * Evaluate the getter, and re-collect dependencies.\n   */\n  Watcher.prototype.get = function get () {\n    pushTarget(this);\n    var value;\n    var vm = this.vm;\n    try {\n      value = this.getter.call(vm, vm);\n    } catch (e) {\n      if (this.user) {\n        handleError(e, vm, (\"getter for watcher \\\"\" + (this.expression) + \"\\\"\"));\n      } else {\n        throw e\n      }\n    } finally {\n      // \"touch\" every property so they are all tracked as\n      // dependencies for deep watching\n      if (this.deep) {\n        traverse(value);\n      }\n      popTarget();\n      this.cleanupDeps();\n    }\n    return value\n  };\n\n  /**\n   * Add a dependency to this directive.\n   */\n  Watcher.prototype.addDep = function addDep (dep) {\n    var id = dep.id;\n    if (!this.newDepIds.has(id)) {\n      this.newDepIds.add(id);\n      this.newDeps.push(dep);\n      if (!this.depIds.has(id)) {\n        dep.addSub(this);\n      }\n    }\n  };\n\n  /**\n   * Clean up for dependency collection.\n   */\n  Watcher.prototype.cleanupDeps = function cleanupDeps () {\n    var i = this.deps.length;\n    while (i--) {\n      var dep = this.deps[i];\n      if (!this.newDepIds.has(dep.id)) {\n        dep.removeSub(this);\n      }\n    }\n    var tmp = this.depIds;\n    this.depIds = this.newDepIds;\n    this.newDepIds = tmp;\n    this.newDepIds.clear();\n    tmp = this.deps;\n    this.deps = this.newDeps;\n    this.newDeps = tmp;\n    this.newDeps.length = 0;\n  };\n\n  /**\n   * Subscriber interface.\n   * Will be called when a dependency changes.\n   */\n  Watcher.prototype.update = function update () {\n    /* istanbul ignore else */\n    if (this.lazy) {\n      this.dirty = true;\n    } else if (this.sync) {\n      this.run();\n    } else {\n      queueWatcher(this);\n    }\n  };\n\n  /**\n   * Scheduler job interface.\n   * Will be called by the scheduler.\n   */\n  Watcher.prototype.run = function run () {\n    if (this.active) {\n      var value = this.get();\n      if (\n        value !== this.value ||\n        // Deep watchers and watchers on Object/Arrays should fire even\n        // when the value is the same, because the value may\n        // have mutated.\n        isObject(value) ||\n        this.deep\n      ) {\n        // set new value\n        var oldValue = this.value;\n        this.value = value;\n        if (this.user) {\n          try {\n            this.cb.call(this.vm, value, oldValue);\n          } catch (e) {\n            handleError(e, this.vm, (\"callback for watcher \\\"\" + (this.expression) + \"\\\"\"));\n          }\n        } else {\n          this.cb.call(this.vm, value, oldValue);\n        }\n      }\n    }\n  };\n\n  /**\n   * Evaluate the value of the watcher.\n   * This only gets called for lazy watchers.\n   */\n  Watcher.prototype.evaluate = function evaluate () {\n    this.value = this.get();\n    this.dirty = false;\n  };\n\n  /**\n   * Depend on all deps collected by this watcher.\n   */\n  Watcher.prototype.depend = function depend () {\n    var i = this.deps.length;\n    while (i--) {\n      this.deps[i].depend();\n    }\n  };\n\n  /**\n   * Remove self from all dependencies' subscriber list.\n   */\n  Watcher.prototype.teardown = function teardown () {\n    if (this.active) {\n      // remove self from vm's watcher list\n      // this is a somewhat expensive operation so we skip it\n      // if the vm is being destroyed.\n      if (!this.vm._isBeingDestroyed) {\n        remove(this.vm._watchers, this);\n      }\n      var i = this.deps.length;\n      while (i--) {\n        this.deps[i].removeSub(this);\n      }\n      this.active = false;\n    }\n  };\n\n  /*  */\n\n  var sharedPropertyDefinition = {\n    enumerable: true,\n    configurable: true,\n    get: noop,\n    set: noop\n  };\n\n  function proxy (target, sourceKey, key) {\n    sharedPropertyDefinition.get = function proxyGetter () {\n      return this[sourceKey][key]\n    };\n    sharedPropertyDefinition.set = function proxySetter (val) {\n      this[sourceKey][key] = val;\n    };\n    Object.defineProperty(target, key, sharedPropertyDefinition);\n  }\n\n  function initState (vm) {\n    vm._watchers = [];\n    var opts = vm.$options;\n    if (opts.props) { initProps(vm, opts.props); }\n    if (opts.methods) { initMethods(vm, opts.methods); }\n    if (opts.data) {\n      initData(vm);\n    } else {\n      observe(vm._data = {}, true /* asRootData */);\n    }\n    if (opts.computed) { initComputed(vm, opts.computed); }\n    if (opts.watch && opts.watch !== nativeWatch) {\n      initWatch(vm, opts.watch);\n    }\n  }\n\n  function initProps (vm, propsOptions) {\n    var propsData = vm.$options.propsData || {};\n    var props = vm._props = {};\n    // cache prop keys so that future props updates can iterate using Array\n    // instead of dynamic object key enumeration.\n    var keys = vm.$options._propKeys = [];\n    var isRoot = !vm.$parent;\n    // root instance props should be converted\n    if (!isRoot) {\n      toggleObserving(false);\n    }\n    var loop = function ( key ) {\n      keys.push(key);\n      var value = validateProp(key, propsOptions, propsData, vm);\n      /* istanbul ignore else */\n      {\n        var hyphenatedKey = hyphenate(key);\n        if (isReservedAttribute(hyphenatedKey) ||\n            config.isReservedAttr(hyphenatedKey)) {\n          warn(\n            (\"\\\"\" + hyphenatedKey + \"\\\" is a reserved attribute and cannot be used as component prop.\"),\n            vm\n          );\n        }\n        defineReactive$$1(props, key, value, function () {\n          if (!isRoot && !isUpdatingChildComponent) {\n            warn(\n              \"Avoid mutating a prop directly since the value will be \" +\n              \"overwritten whenever the parent component re-renders. \" +\n              \"Instead, use a data or computed property based on the prop's \" +\n              \"value. Prop being mutated: \\\"\" + key + \"\\\"\",\n              vm\n            );\n          }\n        });\n      }\n      // static props are already proxied on the component's prototype\n      // during Vue.extend(). We only need to proxy props defined at\n      // instantiation here.\n      if (!(key in vm)) {\n        proxy(vm, \"_props\", key);\n      }\n    };\n\n    for (var key in propsOptions) loop( key );\n    toggleObserving(true);\n  }\n\n  function initData (vm) {\n    var data = vm.$options.data;\n    data = vm._data = typeof data === 'function'\n      ? getData(data, vm)\n      : data || {};\n    if (!isPlainObject(data)) {\n      data = {};\n      warn(\n        'data functions should return an object:\\n' +\n        'https://vuejs.org/v2/guide/components.html#data-Must-Be-a-Function',\n        vm\n      );\n    }\n    // proxy data on instance\n    var keys = Object.keys(data);\n    var props = vm.$options.props;\n    var methods = vm.$options.methods;\n    var i = keys.length;\n    while (i--) {\n      var key = keys[i];\n      {\n        if (methods && hasOwn(methods, key)) {\n          warn(\n            (\"Method \\\"\" + key + \"\\\" has already been defined as a data property.\"),\n            vm\n          );\n        }\n      }\n      if (props && hasOwn(props, key)) {\n        warn(\n          \"The data property \\\"\" + key + \"\\\" is already declared as a prop. \" +\n          \"Use prop default value instead.\",\n          vm\n        );\n      } else if (!isReserved(key)) {\n        proxy(vm, \"_data\", key);\n      }\n    }\n    // observe data\n    observe(data, true /* asRootData */);\n  }\n\n  function getData (data, vm) {\n    // #7573 disable dep collection when invoking data getters\n    pushTarget();\n    try {\n      return data.call(vm, vm)\n    } catch (e) {\n      handleError(e, vm, \"data()\");\n      return {}\n    } finally {\n      popTarget();\n    }\n  }\n\n  var computedWatcherOptions = { lazy: true };\n\n  function initComputed (vm, computed) {\n    // $flow-disable-line\n    var watchers = vm._computedWatchers = Object.create(null);\n    // computed properties are just getters during SSR\n    var isSSR = isServerRendering();\n\n    for (var key in computed) {\n      var userDef = computed[key];\n      var getter = typeof userDef === 'function' ? userDef : userDef.get;\n      if (getter == null) {\n        warn(\n          (\"Getter is missing for computed property \\\"\" + key + \"\\\".\"),\n          vm\n        );\n      }\n\n      if (!isSSR) {\n        // create internal watcher for the computed property.\n        watchers[key] = new Watcher(\n          vm,\n          getter || noop,\n          noop,\n          computedWatcherOptions\n        );\n      }\n\n      // component-defined computed properties are already defined on the\n      // component prototype. We only need to define computed properties defined\n      // at instantiation here.\n      if (!(key in vm)) {\n        defineComputed(vm, key, userDef);\n      } else {\n        if (key in vm.$data) {\n          warn((\"The computed property \\\"\" + key + \"\\\" is already defined in data.\"), vm);\n        } else if (vm.$options.props && key in vm.$options.props) {\n          warn((\"The computed property \\\"\" + key + \"\\\" is already defined as a prop.\"), vm);\n        }\n      }\n    }\n  }\n\n  function defineComputed (\n    target,\n    key,\n    userDef\n  ) {\n    var shouldCache = !isServerRendering();\n    if (typeof userDef === 'function') {\n      sharedPropertyDefinition.get = shouldCache\n        ? createComputedGetter(key)\n        : createGetterInvoker(userDef);\n      sharedPropertyDefinition.set = noop;\n    } else {\n      sharedPropertyDefinition.get = userDef.get\n        ? shouldCache && userDef.cache !== false\n          ? createComputedGetter(key)\n          : createGetterInvoker(userDef.get)\n        : noop;\n      sharedPropertyDefinition.set = userDef.set || noop;\n    }\n    if (sharedPropertyDefinition.set === noop) {\n      sharedPropertyDefinition.set = function () {\n        warn(\n          (\"Computed property \\\"\" + key + \"\\\" was assigned to but it has no setter.\"),\n          this\n        );\n      };\n    }\n    Object.defineProperty(target, key, sharedPropertyDefinition);\n  }\n\n  function createComputedGetter (key) {\n    return function computedGetter () {\n      var watcher = this._computedWatchers && this._computedWatchers[key];\n      if (watcher) {\n        if (watcher.dirty) {\n          watcher.evaluate();\n        }\n        if (Dep.target) {\n          watcher.depend();\n        }\n        return watcher.value\n      }\n    }\n  }\n\n  function createGetterInvoker(fn) {\n    return function computedGetter () {\n      return fn.call(this, this)\n    }\n  }\n\n  function initMethods (vm, methods) {\n    var props = vm.$options.props;\n    for (var key in methods) {\n      {\n        if (typeof methods[key] !== 'function') {\n          warn(\n            \"Method \\\"\" + key + \"\\\" has type \\\"\" + (typeof methods[key]) + \"\\\" in the component definition. \" +\n            \"Did you reference the function correctly?\",\n            vm\n          );\n        }\n        if (props && hasOwn(props, key)) {\n          warn(\n            (\"Method \\\"\" + key + \"\\\" has already been defined as a prop.\"),\n            vm\n          );\n        }\n        if ((key in vm) && isReserved(key)) {\n          warn(\n            \"Method \\\"\" + key + \"\\\" conflicts with an existing Vue instance method. \" +\n            \"Avoid defining component methods that start with _ or $.\"\n          );\n        }\n      }\n      vm[key] = typeof methods[key] !== 'function' ? noop : bind(methods[key], vm);\n    }\n  }\n\n  function initWatch (vm, watch) {\n    for (var key in watch) {\n      var handler = watch[key];\n      if (Array.isArray(handler)) {\n        for (var i = 0; i < handler.length; i++) {\n          createWatcher(vm, key, handler[i]);\n        }\n      } else {\n        createWatcher(vm, key, handler);\n      }\n    }\n  }\n\n  function createWatcher (\n    vm,\n    expOrFn,\n    handler,\n    options\n  ) {\n    if (isPlainObject(handler)) {\n      options = handler;\n      handler = handler.handler;\n    }\n    if (typeof handler === 'string') {\n      handler = vm[handler];\n    }\n    return vm.$watch(expOrFn, handler, options)\n  }\n\n  function stateMixin (Vue) {\n    // flow somehow has problems with directly declared definition object\n    // when using Object.defineProperty, so we have to procedurally build up\n    // the object here.\n    var dataDef = {};\n    dataDef.get = function () { return this._data };\n    var propsDef = {};\n    propsDef.get = function () { return this._props };\n    {\n      dataDef.set = function () {\n        warn(\n          'Avoid replacing instance root $data. ' +\n          'Use nested data properties instead.',\n          this\n        );\n      };\n      propsDef.set = function () {\n        warn(\"$props is readonly.\", this);\n      };\n    }\n    Object.defineProperty(Vue.prototype, '$data', dataDef);\n    Object.defineProperty(Vue.prototype, '$props', propsDef);\n\n    Vue.prototype.$set = set;\n    Vue.prototype.$delete = del;\n\n    Vue.prototype.$watch = function (\n      expOrFn,\n      cb,\n      options\n    ) {\n      var vm = this;\n      if (isPlainObject(cb)) {\n        return createWatcher(vm, expOrFn, cb, options)\n      }\n      options = options || {};\n      options.user = true;\n      var watcher = new Watcher(vm, expOrFn, cb, options);\n      if (options.immediate) {\n        try {\n          cb.call(vm, watcher.value);\n        } catch (error) {\n          handleError(error, vm, (\"callback for immediate watcher \\\"\" + (watcher.expression) + \"\\\"\"));\n        }\n      }\n      return function unwatchFn () {\n        watcher.teardown();\n      }\n    };\n  }\n\n  /*  */\n\n  var uid$3 = 0;\n\n  function initMixin (Vue) {\n    Vue.prototype._init = function (options) {\n      var vm = this;\n      // a uid\n      vm._uid = uid$3++;\n\n      var startTag, endTag;\n      /* istanbul ignore if */\n      if (config.performance && mark) {\n        startTag = \"vue-perf-start:\" + (vm._uid);\n        endTag = \"vue-perf-end:\" + (vm._uid);\n        mark(startTag);\n      }\n\n      // a flag to avoid this being observed\n      vm._isVue = true;\n      // merge options\n      if (options && options._isComponent) {\n        // optimize internal component instantiation\n        // since dynamic options merging is pretty slow, and none of the\n        // internal component options needs special treatment.\n        initInternalComponent(vm, options);\n      } else {\n        vm.$options = mergeOptions(\n          resolveConstructorOptions(vm.constructor),\n          options || {},\n          vm\n        );\n      }\n      /* istanbul ignore else */\n      {\n        initProxy(vm);\n      }\n      // expose real self\n      vm._self = vm;\n      initLifecycle(vm);\n      initEvents(vm);\n      initRender(vm);\n      callHook(vm, 'beforeCreate');\n      initInjections(vm); // resolve injections before data/props\n      initState(vm);\n      initProvide(vm); // resolve provide after data/props\n      callHook(vm, 'created');\n\n      /* istanbul ignore if */\n      if (config.performance && mark) {\n        vm._name = formatComponentName(vm, false);\n        mark(endTag);\n        measure((\"vue \" + (vm._name) + \" init\"), startTag, endTag);\n      }\n\n      if (vm.$options.el) {\n        vm.$mount(vm.$options.el);\n      }\n    };\n  }\n\n  function initInternalComponent (vm, options) {\n    var opts = vm.$options = Object.create(vm.constructor.options);\n    // doing this because it's faster than dynamic enumeration.\n    var parentVnode = options._parentVnode;\n    opts.parent = options.parent;\n    opts._parentVnode = parentVnode;\n\n    var vnodeComponentOptions = parentVnode.componentOptions;\n    opts.propsData = vnodeComponentOptions.propsData;\n    opts._parentListeners = vnodeComponentOptions.listeners;\n    opts._renderChildren = vnodeComponentOptions.children;\n    opts._componentTag = vnodeComponentOptions.tag;\n\n    if (options.render) {\n      opts.render = options.render;\n      opts.staticRenderFns = options.staticRenderFns;\n    }\n  }\n\n  function resolveConstructorOptions (Ctor) {\n    var options = Ctor.options;\n    if (Ctor.super) {\n      var superOptions = resolveConstructorOptions(Ctor.super);\n      var cachedSuperOptions = Ctor.superOptions;\n      if (superOptions !== cachedSuperOptions) {\n        // super option changed,\n        // need to resolve new options.\n        Ctor.superOptions = superOptions;\n        // check if there are any late-modified/attached options (#4976)\n        var modifiedOptions = resolveModifiedOptions(Ctor);\n        // update base extend options\n        if (modifiedOptions) {\n          extend(Ctor.extendOptions, modifiedOptions);\n        }\n        options = Ctor.options = mergeOptions(superOptions, Ctor.extendOptions);\n        if (options.name) {\n          options.components[options.name] = Ctor;\n        }\n      }\n    }\n    return options\n  }\n\n  function resolveModifiedOptions (Ctor) {\n    var modified;\n    var latest = Ctor.options;\n    var sealed = Ctor.sealedOptions;\n    for (var key in latest) {\n      if (latest[key] !== sealed[key]) {\n        if (!modified) { modified = {}; }\n        modified[key] = latest[key];\n      }\n    }\n    return modified\n  }\n\n  function Vue (options) {\n    if (!(this instanceof Vue)\n    ) {\n      warn('Vue is a constructor and should be called with the `new` keyword');\n    }\n    this._init(options);\n  }\n\n  initMixin(Vue);\n  stateMixin(Vue);\n  eventsMixin(Vue);\n  lifecycleMixin(Vue);\n  renderMixin(Vue);\n\n  /*  */\n\n  function initUse (Vue) {\n    Vue.use = function (plugin) {\n      var installedPlugins = (this._installedPlugins || (this._installedPlugins = []));\n      if (installedPlugins.indexOf(plugin) > -1) {\n        return this\n      }\n\n      // additional parameters\n      var args = toArray(arguments, 1);\n      args.unshift(this);\n      if (typeof plugin.install === 'function') {\n        plugin.install.apply(plugin, args);\n      } else if (typeof plugin === 'function') {\n        plugin.apply(null, args);\n      }\n      installedPlugins.push(plugin);\n      return this\n    };\n  }\n\n  /*  */\n\n  function initMixin$1 (Vue) {\n    Vue.mixin = function (mixin) {\n      this.options = mergeOptions(this.options, mixin);\n      return this\n    };\n  }\n\n  /*  */\n\n  function initExtend (Vue) {\n    /**\n     * Each instance constructor, including Vue, has a unique\n     * cid. This enables us to create wrapped \"child\n     * constructors\" for prototypal inheritance and cache them.\n     */\n    Vue.cid = 0;\n    var cid = 1;\n\n    /**\n     * Class inheritance\n     */\n    Vue.extend = function (extendOptions) {\n      extendOptions = extendOptions || {};\n      var Super = this;\n      var SuperId = Super.cid;\n      var cachedCtors = extendOptions._Ctor || (extendOptions._Ctor = {});\n      if (cachedCtors[SuperId]) {\n        return cachedCtors[SuperId]\n      }\n\n      var name = extendOptions.name || Super.options.name;\n      if (name) {\n        validateComponentName(name);\n      }\n\n      var Sub = function VueComponent (options) {\n        this._init(options);\n      };\n      Sub.prototype = Object.create(Super.prototype);\n      Sub.prototype.constructor = Sub;\n      Sub.cid = cid++;\n      Sub.options = mergeOptions(\n        Super.options,\n        extendOptions\n      );\n      Sub['super'] = Super;\n\n      // For props and computed properties, we define the proxy getters on\n      // the Vue instances at extension time, on the extended prototype. This\n      // avoids Object.defineProperty calls for each instance created.\n      if (Sub.options.props) {\n        initProps$1(Sub);\n      }\n      if (Sub.options.computed) {\n        initComputed$1(Sub);\n      }\n\n      // allow further extension/mixin/plugin usage\n      Sub.extend = Super.extend;\n      Sub.mixin = Super.mixin;\n      Sub.use = Super.use;\n\n      // create asset registers, so extended classes\n      // can have their private assets too.\n      ASSET_TYPES.forEach(function (type) {\n        Sub[type] = Super[type];\n      });\n      // enable recursive self-lookup\n      if (name) {\n        Sub.options.components[name] = Sub;\n      }\n\n      // keep a reference to the super options at extension time.\n      // later at instantiation we can check if Super's options have\n      // been updated.\n      Sub.superOptions = Super.options;\n      Sub.extendOptions = extendOptions;\n      Sub.sealedOptions = extend({}, Sub.options);\n\n      // cache constructor\n      cachedCtors[SuperId] = Sub;\n      return Sub\n    };\n  }\n\n  function initProps$1 (Comp) {\n    var props = Comp.options.props;\n    for (var key in props) {\n      proxy(Comp.prototype, \"_props\", key);\n    }\n  }\n\n  function initComputed$1 (Comp) {\n    var computed = Comp.options.computed;\n    for (var key in computed) {\n      defineComputed(Comp.prototype, key, computed[key]);\n    }\n  }\n\n  /*  */\n\n  function initAssetRegisters (Vue) {\n    /**\n     * Create asset registration methods.\n     */\n    ASSET_TYPES.forEach(function (type) {\n      Vue[type] = function (\n        id,\n        definition\n      ) {\n        if (!definition) {\n          return this.options[type + 's'][id]\n        } else {\n          /* istanbul ignore if */\n          if (type === 'component') {\n            validateComponentName(id);\n          }\n          if (type === 'component' && isPlainObject(definition)) {\n            definition.name = definition.name || id;\n            definition = this.options._base.extend(definition);\n          }\n          if (type === 'directive' && typeof definition === 'function') {\n            definition = { bind: definition, update: definition };\n          }\n          this.options[type + 's'][id] = definition;\n          return definition\n        }\n      };\n    });\n  }\n\n  /*  */\n\n\n\n  function getComponentName (opts) {\n    return opts && (opts.Ctor.options.name || opts.tag)\n  }\n\n  function matches (pattern, name) {\n    if (Array.isArray(pattern)) {\n      return pattern.indexOf(name) > -1\n    } else if (typeof pattern === 'string') {\n      return pattern.split(',').indexOf(name) > -1\n    } else if (isRegExp(pattern)) {\n      return pattern.test(name)\n    }\n    /* istanbul ignore next */\n    return false\n  }\n\n  function pruneCache (keepAliveInstance, filter) {\n    var cache = keepAliveInstance.cache;\n    var keys = keepAliveInstance.keys;\n    var _vnode = keepAliveInstance._vnode;\n    for (var key in cache) {\n      var cachedNode = cache[key];\n      if (cachedNode) {\n        var name = getComponentName(cachedNode.componentOptions);\n        if (name && !filter(name)) {\n          pruneCacheEntry(cache, key, keys, _vnode);\n        }\n      }\n    }\n  }\n\n  function pruneCacheEntry (\n    cache,\n    key,\n    keys,\n    current\n  ) {\n    var cached$$1 = cache[key];\n    if (cached$$1 && (!current || cached$$1.tag !== current.tag)) {\n      cached$$1.componentInstance.$destroy();\n    }\n    cache[key] = null;\n    remove(keys, key);\n  }\n\n  var patternTypes = [String, RegExp, Array];\n\n  var KeepAlive = {\n    name: 'keep-alive',\n    abstract: true,\n\n    props: {\n      include: patternTypes,\n      exclude: patternTypes,\n      max: [String, Number]\n    },\n\n    created: function created () {\n      this.cache = Object.create(null);\n      this.keys = [];\n    },\n\n    destroyed: function destroyed () {\n      for (var key in this.cache) {\n        pruneCacheEntry(this.cache, key, this.keys);\n      }\n    },\n\n    mounted: function mounted () {\n      var this$1 = this;\n\n      this.$watch('include', function (val) {\n        pruneCache(this$1, function (name) { return matches(val, name); });\n      });\n      this.$watch('exclude', function (val) {\n        pruneCache(this$1, function (name) { return !matches(val, name); });\n      });\n    },\n\n    render: function render () {\n      var slot = this.$slots.default;\n      var vnode = getFirstComponentChild(slot);\n      var componentOptions = vnode && vnode.componentOptions;\n      if (componentOptions) {\n        // check pattern\n        var name = getComponentName(componentOptions);\n        var ref = this;\n        var include = ref.include;\n        var exclude = ref.exclude;\n        if (\n          // not included\n          (include && (!name || !matches(include, name))) ||\n          // excluded\n          (exclude && name && matches(exclude, name))\n        ) {\n          return vnode\n        }\n\n        var ref$1 = this;\n        var cache = ref$1.cache;\n        var keys = ref$1.keys;\n        var key = vnode.key == null\n          // same constructor may get registered as different local components\n          // so cid alone is not enough (#3269)\n          ? componentOptions.Ctor.cid + (componentOptions.tag ? (\"::\" + (componentOptions.tag)) : '')\n          : vnode.key;\n        if (cache[key]) {\n          vnode.componentInstance = cache[key].componentInstance;\n          // make current key freshest\n          remove(keys, key);\n          keys.push(key);\n        } else {\n          cache[key] = vnode;\n          keys.push(key);\n          // prune oldest entry\n          if (this.max && keys.length > parseInt(this.max)) {\n            pruneCacheEntry(cache, keys[0], keys, this._vnode);\n          }\n        }\n\n        vnode.data.keepAlive = true;\n      }\n      return vnode || (slot && slot[0])\n    }\n  };\n\n  var builtInComponents = {\n    KeepAlive: KeepAlive\n  };\n\n  /*  */\n\n  function initGlobalAPI (Vue) {\n    // config\n    var configDef = {};\n    configDef.get = function () { return config; };\n    {\n      configDef.set = function () {\n        warn(\n          'Do not replace the Vue.config object, set individual fields instead.'\n        );\n      };\n    }\n    Object.defineProperty(Vue, 'config', configDef);\n\n    // exposed util methods.\n    // NOTE: these are not considered part of the public API - avoid relying on\n    // them unless you are aware of the risk.\n    Vue.util = {\n      warn: warn,\n      extend: extend,\n      mergeOptions: mergeOptions,\n      defineReactive: defineReactive$$1\n    };\n\n    Vue.set = set;\n    Vue.delete = del;\n    Vue.nextTick = nextTick;\n\n    // 2.6 explicit observable API\n    Vue.observable = function (obj) {\n      observe(obj);\n      return obj\n    };\n\n    Vue.options = Object.create(null);\n    ASSET_TYPES.forEach(function (type) {\n      Vue.options[type + 's'] = Object.create(null);\n    });\n\n    // this is used to identify the \"base\" constructor to extend all plain-object\n    // components with in Weex's multi-instance scenarios.\n    Vue.options._base = Vue;\n\n    extend(Vue.options.components, builtInComponents);\n\n    initUse(Vue);\n    initMixin$1(Vue);\n    initExtend(Vue);\n    initAssetRegisters(Vue);\n  }\n\n  initGlobalAPI(Vue);\n\n  Object.defineProperty(Vue.prototype, '$isServer', {\n    get: isServerRendering\n  });\n\n  Object.defineProperty(Vue.prototype, '$ssrContext', {\n    get: function get () {\n      /* istanbul ignore next */\n      return this.$vnode && this.$vnode.ssrContext\n    }\n  });\n\n  // expose FunctionalRenderContext for ssr runtime helper installation\n  Object.defineProperty(Vue, 'FunctionalRenderContext', {\n    value: FunctionalRenderContext\n  });\n\n  Vue.version = '2.6.11';\n\n  /*  */\n\n  // these are reserved for web because they are directly compiled away\n  // during template compilation\n  var isReservedAttr = makeMap('style,class');\n\n  // attributes that should be using props for binding\n  var acceptValue = makeMap('input,textarea,option,select,progress');\n  var mustUseProp = function (tag, type, attr) {\n    return (\n      (attr === 'value' && acceptValue(tag)) && type !== 'button' ||\n      (attr === 'selected' && tag === 'option') ||\n      (attr === 'checked' && tag === 'input') ||\n      (attr === 'muted' && tag === 'video')\n    )\n  };\n\n  var isEnumeratedAttr = makeMap('contenteditable,draggable,spellcheck');\n\n  var isValidContentEditableValue = makeMap('events,caret,typing,plaintext-only');\n\n  var convertEnumeratedValue = function (key, value) {\n    return isFalsyAttrValue(value) || value === 'false'\n      ? 'false'\n      // allow arbitrary string value for contenteditable\n      : key === 'contenteditable' && isValidContentEditableValue(value)\n        ? value\n        : 'true'\n  };\n\n  var isBooleanAttr = makeMap(\n    'allowfullscreen,async,autofocus,autoplay,checked,compact,controls,declare,' +\n    'default,defaultchecked,defaultmuted,defaultselected,defer,disabled,' +\n    'enabled,formnovalidate,hidden,indeterminate,inert,ismap,itemscope,loop,multiple,' +\n    'muted,nohref,noresize,noshade,novalidate,nowrap,open,pauseonexit,readonly,' +\n    'required,reversed,scoped,seamless,selected,sortable,translate,' +\n    'truespeed,typemustmatch,visible'\n  );\n\n  var xlinkNS = 'http://www.w3.org/1999/xlink';\n\n  var isXlink = function (name) {\n    return name.charAt(5) === ':' && name.slice(0, 5) === 'xlink'\n  };\n\n  var getXlinkProp = function (name) {\n    return isXlink(name) ? name.slice(6, name.length) : ''\n  };\n\n  var isFalsyAttrValue = function (val) {\n    return val == null || val === false\n  };\n\n  /*  */\n\n  function genClassForVnode (vnode) {\n    var data = vnode.data;\n    var parentNode = vnode;\n    var childNode = vnode;\n    while (isDef(childNode.componentInstance)) {\n      childNode = childNode.componentInstance._vnode;\n      if (childNode && childNode.data) {\n        data = mergeClassData(childNode.data, data);\n      }\n    }\n    while (isDef(parentNode = parentNode.parent)) {\n      if (parentNode && parentNode.data) {\n        data = mergeClassData(data, parentNode.data);\n      }\n    }\n    return renderClass(data.staticClass, data.class)\n  }\n\n  function mergeClassData (child, parent) {\n    return {\n      staticClass: concat(child.staticClass, parent.staticClass),\n      class: isDef(child.class)\n        ? [child.class, parent.class]\n        : parent.class\n    }\n  }\n\n  function renderClass (\n    staticClass,\n    dynamicClass\n  ) {\n    if (isDef(staticClass) || isDef(dynamicClass)) {\n      return concat(staticClass, stringifyClass(dynamicClass))\n    }\n    /* istanbul ignore next */\n    return ''\n  }\n\n  function concat (a, b) {\n    return a ? b ? (a + ' ' + b) : a : (b || '')\n  }\n\n  function stringifyClass (value) {\n    if (Array.isArray(value)) {\n      return stringifyArray(value)\n    }\n    if (isObject(value)) {\n      return stringifyObject(value)\n    }\n    if (typeof value === 'string') {\n      return value\n    }\n    /* istanbul ignore next */\n    return ''\n  }\n\n  function stringifyArray (value) {\n    var res = '';\n    var stringified;\n    for (var i = 0, l = value.length; i < l; i++) {\n      if (isDef(stringified = stringifyClass(value[i])) && stringified !== '') {\n        if (res) { res += ' '; }\n        res += stringified;\n      }\n    }\n    return res\n  }\n\n  function stringifyObject (value) {\n    var res = '';\n    for (var key in value) {\n      if (value[key]) {\n        if (res) { res += ' '; }\n        res += key;\n      }\n    }\n    return res\n  }\n\n  /*  */\n\n  var namespaceMap = {\n    svg: 'http://www.w3.org/2000/svg',\n    math: 'http://www.w3.org/1998/Math/MathML'\n  };\n\n  var isHTMLTag = makeMap(\n    'html,body,base,head,link,meta,style,title,' +\n    'address,article,aside,footer,header,h1,h2,h3,h4,h5,h6,hgroup,nav,section,' +\n    'div,dd,dl,dt,figcaption,figure,picture,hr,img,li,main,ol,p,pre,ul,' +\n    'a,b,abbr,bdi,bdo,br,cite,code,data,dfn,em,i,kbd,mark,q,rp,rt,rtc,ruby,' +\n    's,samp,small,span,strong,sub,sup,time,u,var,wbr,area,audio,map,track,video,' +\n    'embed,object,param,source,canvas,script,noscript,del,ins,' +\n    'caption,col,colgroup,table,thead,tbody,td,th,tr,' +\n    'button,datalist,fieldset,form,input,label,legend,meter,optgroup,option,' +\n    'output,progress,select,textarea,' +\n    'details,dialog,menu,menuitem,summary,' +\n    'content,element,shadow,template,blockquote,iframe,tfoot'\n  );\n\n  // this map is intentionally selective, only covering SVG elements that may\n  // contain child elements.\n  var isSVG = makeMap(\n    'svg,animate,circle,clippath,cursor,defs,desc,ellipse,filter,font-face,' +\n    'foreignObject,g,glyph,image,line,marker,mask,missing-glyph,path,pattern,' +\n    'polygon,polyline,rect,switch,symbol,text,textpath,tspan,use,view',\n    true\n  );\n\n  var isPreTag = function (tag) { return tag === 'pre'; };\n\n  var isReservedTag = function (tag) {\n    return isHTMLTag(tag) || isSVG(tag)\n  };\n\n  function getTagNamespace (tag) {\n    if (isSVG(tag)) {\n      return 'svg'\n    }\n    // basic support for MathML\n    // note it doesn't support other MathML elements being component roots\n    if (tag === 'math') {\n      return 'math'\n    }\n  }\n\n  var unknownElementCache = Object.create(null);\n  function isUnknownElement (tag) {\n    /* istanbul ignore if */\n    if (!inBrowser) {\n      return true\n    }\n    if (isReservedTag(tag)) {\n      return false\n    }\n    tag = tag.toLowerCase();\n    /* istanbul ignore if */\n    if (unknownElementCache[tag] != null) {\n      return unknownElementCache[tag]\n    }\n    var el = document.createElement(tag);\n    if (tag.indexOf('-') > -1) {\n      // http://stackoverflow.com/a/28210364/1070244\n      return (unknownElementCache[tag] = (\n        el.constructor === window.HTMLUnknownElement ||\n        el.constructor === window.HTMLElement\n      ))\n    } else {\n      return (unknownElementCache[tag] = /HTMLUnknownElement/.test(el.toString()))\n    }\n  }\n\n  var isTextInputType = makeMap('text,number,password,search,email,tel,url');\n\n  /*  */\n\n  /**\n   * Query an element selector if it's not an element already.\n   */\n  function query (el) {\n    if (typeof el === 'string') {\n      var selected = document.querySelector(el);\n      if (!selected) {\n        warn(\n          'Cannot find element: ' + el\n        );\n        return document.createElement('div')\n      }\n      return selected\n    } else {\n      return el\n    }\n  }\n\n  /*  */\n\n  function createElement$1 (tagName, vnode) {\n    var elm = document.createElement(tagName);\n    if (tagName !== 'select') {\n      return elm\n    }\n    // false or null will remove the attribute but undefined will not\n    if (vnode.data && vnode.data.attrs && vnode.data.attrs.multiple !== undefined) {\n      elm.setAttribute('multiple', 'multiple');\n    }\n    return elm\n  }\n\n  function createElementNS (namespace, tagName) {\n    return document.createElementNS(namespaceMap[namespace], tagName)\n  }\n\n  function createTextNode (text) {\n    return document.createTextNode(text)\n  }\n\n  function createComment (text) {\n    return document.createComment(text)\n  }\n\n  function insertBefore (parentNode, newNode, referenceNode) {\n    parentNode.insertBefore(newNode, referenceNode);\n  }\n\n  function removeChild (node, child) {\n    node.removeChild(child);\n  }\n\n  function appendChild (node, child) {\n    node.appendChild(child);\n  }\n\n  function parentNode (node) {\n    return node.parentNode\n  }\n\n  function nextSibling (node) {\n    return node.nextSibling\n  }\n\n  function tagName (node) {\n    return node.tagName\n  }\n\n  function setTextContent (node, text) {\n    node.textContent = text;\n  }\n\n  function setStyleScope (node, scopeId) {\n    node.setAttribute(scopeId, '');\n  }\n\n  var nodeOps = /*#__PURE__*/Object.freeze({\n    createElement: createElement$1,\n    createElementNS: createElementNS,\n    createTextNode: createTextNode,\n    createComment: createComment,\n    insertBefore: insertBefore,\n    removeChild: removeChild,\n    appendChild: appendChild,\n    parentNode: parentNode,\n    nextSibling: nextSibling,\n    tagName: tagName,\n    setTextContent: setTextContent,\n    setStyleScope: setStyleScope\n  });\n\n  /*  */\n\n  var ref = {\n    create: function create (_, vnode) {\n      registerRef(vnode);\n    },\n    update: function update (oldVnode, vnode) {\n      if (oldVnode.data.ref !== vnode.data.ref) {\n        registerRef(oldVnode, true);\n        registerRef(vnode);\n      }\n    },\n    destroy: function destroy (vnode) {\n      registerRef(vnode, true);\n    }\n  };\n\n  function registerRef (vnode, isRemoval) {\n    var key = vnode.data.ref;\n    if (!isDef(key)) { return }\n\n    var vm = vnode.context;\n    var ref = vnode.componentInstance || vnode.elm;\n    var refs = vm.$refs;\n    if (isRemoval) {\n      if (Array.isArray(refs[key])) {\n        remove(refs[key], ref);\n      } else if (refs[key] === ref) {\n        refs[key] = undefined;\n      }\n    } else {\n      if (vnode.data.refInFor) {\n        if (!Array.isArray(refs[key])) {\n          refs[key] = [ref];\n        } else if (refs[key].indexOf(ref) < 0) {\n          // $flow-disable-line\n          refs[key].push(ref);\n        }\n      } else {\n        refs[key] = ref;\n      }\n    }\n  }\n\n  /**\n   * Virtual DOM patching algorithm based on Snabbdom by\n   * Simon Friis Vindum (@paldepind)\n   * Licensed under the MIT License\n   * https://github.com/paldepind/snabbdom/blob/master/LICENSE\n   *\n   * modified by Evan You (@yyx990803)\n   *\n   * Not type-checking this because this file is perf-critical and the cost\n   * of making flow understand it is not worth it.\n   */\n\n  var emptyNode = new VNode('', {}, []);\n\n  var hooks = ['create', 'activate', 'update', 'remove', 'destroy'];\n\n  function sameVnode (a, b) {\n    return (\n      a.key === b.key && (\n        (\n          a.tag === b.tag &&\n          a.isComment === b.isComment &&\n          isDef(a.data) === isDef(b.data) &&\n          sameInputType(a, b)\n        ) || (\n          isTrue(a.isAsyncPlaceholder) &&\n          a.asyncFactory === b.asyncFactory &&\n          isUndef(b.asyncFactory.error)\n        )\n      )\n    )\n  }\n\n  function sameInputType (a, b) {\n    if (a.tag !== 'input') { return true }\n    var i;\n    var typeA = isDef(i = a.data) && isDef(i = i.attrs) && i.type;\n    var typeB = isDef(i = b.data) && isDef(i = i.attrs) && i.type;\n    return typeA === typeB || isTextInputType(typeA) && isTextInputType(typeB)\n  }\n\n  function createKeyToOldIdx (children, beginIdx, endIdx) {\n    var i, key;\n    var map = {};\n    for (i = beginIdx; i <= endIdx; ++i) {\n      key = children[i].key;\n      if (isDef(key)) { map[key] = i; }\n    }\n    return map\n  }\n\n  function createPatchFunction (backend) {\n    var i, j;\n    var cbs = {};\n\n    var modules = backend.modules;\n    var nodeOps = backend.nodeOps;\n\n    for (i = 0; i < hooks.length; ++i) {\n      cbs[hooks[i]] = [];\n      for (j = 0; j < modules.length; ++j) {\n        if (isDef(modules[j][hooks[i]])) {\n          cbs[hooks[i]].push(modules[j][hooks[i]]);\n        }\n      }\n    }\n\n    function emptyNodeAt (elm) {\n      return new VNode(nodeOps.tagName(elm).toLowerCase(), {}, [], undefined, elm)\n    }\n\n    function createRmCb (childElm, listeners) {\n      function remove$$1 () {\n        if (--remove$$1.listeners === 0) {\n          removeNode(childElm);\n        }\n      }\n      remove$$1.listeners = listeners;\n      return remove$$1\n    }\n\n    function removeNode (el) {\n      var parent = nodeOps.parentNode(el);\n      // element may have already been removed due to v-html / v-text\n      if (isDef(parent)) {\n        nodeOps.removeChild(parent, el);\n      }\n    }\n\n    function isUnknownElement$$1 (vnode, inVPre) {\n      return (\n        !inVPre &&\n        !vnode.ns &&\n        !(\n          config.ignoredElements.length &&\n          config.ignoredElements.some(function (ignore) {\n            return isRegExp(ignore)\n              ? ignore.test(vnode.tag)\n              : ignore === vnode.tag\n          })\n        ) &&\n        config.isUnknownElement(vnode.tag)\n      )\n    }\n\n    var creatingElmInVPre = 0;\n\n    function createElm (\n      vnode,\n      insertedVnodeQueue,\n      parentElm,\n      refElm,\n      nested,\n      ownerArray,\n      index\n    ) {\n      if (isDef(vnode.elm) && isDef(ownerArray)) {\n        // This vnode was used in a previous render!\n        // now it's used as a new node, overwriting its elm would cause\n        // potential patch errors down the road when it's used as an insertion\n        // reference node. Instead, we clone the node on-demand before creating\n        // associated DOM element for it.\n        vnode = ownerArray[index] = cloneVNode(vnode);\n      }\n\n      vnode.isRootInsert = !nested; // for transition enter check\n      if (createComponent(vnode, insertedVnodeQueue, parentElm, refElm)) {\n        return\n      }\n\n      var data = vnode.data;\n      var children = vnode.children;\n      var tag = vnode.tag;\n      if (isDef(tag)) {\n        {\n          if (data && data.pre) {\n            creatingElmInVPre++;\n          }\n          if (isUnknownElement$$1(vnode, creatingElmInVPre)) {\n            warn(\n              'Unknown custom element: <' + tag + '> - did you ' +\n              'register the component correctly? For recursive components, ' +\n              'make sure to provide the \"name\" option.',\n              vnode.context\n            );\n          }\n        }\n\n        vnode.elm = vnode.ns\n          ? nodeOps.createElementNS(vnode.ns, tag)\n          : nodeOps.createElement(tag, vnode);\n        setScope(vnode);\n\n        /* istanbul ignore if */\n        {\n          createChildren(vnode, children, insertedVnodeQueue);\n          if (isDef(data)) {\n            invokeCreateHooks(vnode, insertedVnodeQueue);\n          }\n          insert(parentElm, vnode.elm, refElm);\n        }\n\n        if (data && data.pre) {\n          creatingElmInVPre--;\n        }\n      } else if (isTrue(vnode.isComment)) {\n        vnode.elm = nodeOps.createComment(vnode.text);\n        insert(parentElm, vnode.elm, refElm);\n      } else {\n        vnode.elm = nodeOps.createTextNode(vnode.text);\n        insert(parentElm, vnode.elm, refElm);\n      }\n    }\n\n    function createComponent (vnode, insertedVnodeQueue, parentElm, refElm) {\n      var i = vnode.data;\n      if (isDef(i)) {\n        var isReactivated = isDef(vnode.componentInstance) && i.keepAlive;\n        if (isDef(i = i.hook) && isDef(i = i.init)) {\n          i(vnode, false /* hydrating */);\n        }\n        // after calling the init hook, if the vnode is a child component\n        // it should've created a child instance and mounted it. the child\n        // component also has set the placeholder vnode's elm.\n        // in that case we can just return the element and be done.\n        if (isDef(vnode.componentInstance)) {\n          initComponent(vnode, insertedVnodeQueue);\n          insert(parentElm, vnode.elm, refElm);\n          if (isTrue(isReactivated)) {\n            reactivateComponent(vnode, insertedVnodeQueue, parentElm, refElm);\n          }\n          return true\n        }\n      }\n    }\n\n    function initComponent (vnode, insertedVnodeQueue) {\n      if (isDef(vnode.data.pendingInsert)) {\n        insertedVnodeQueue.push.apply(insertedVnodeQueue, vnode.data.pendingInsert);\n        vnode.data.pendingInsert = null;\n      }\n      vnode.elm = vnode.componentInstance.$el;\n      if (isPatchable(vnode)) {\n        invokeCreateHooks(vnode, insertedVnodeQueue);\n        setScope(vnode);\n      } else {\n        // empty component root.\n        // skip all element-related modules except for ref (#3455)\n        registerRef(vnode);\n        // make sure to invoke the insert hook\n        insertedVnodeQueue.push(vnode);\n      }\n    }\n\n    function reactivateComponent (vnode, insertedVnodeQueue, parentElm, refElm) {\n      var i;\n      // hack for #4339: a reactivated component with inner transition\n      // does not trigger because the inner node's created hooks are not called\n      // again. It's not ideal to involve module-specific logic in here but\n      // there doesn't seem to be a better way to do it.\n      var innerNode = vnode;\n      while (innerNode.componentInstance) {\n        innerNode = innerNode.componentInstance._vnode;\n        if (isDef(i = innerNode.data) && isDef(i = i.transition)) {\n          for (i = 0; i < cbs.activate.length; ++i) {\n            cbs.activate[i](emptyNode, innerNode);\n          }\n          insertedVnodeQueue.push(innerNode);\n          break\n        }\n      }\n      // unlike a newly created component,\n      // a reactivated keep-alive component doesn't insert itself\n      insert(parentElm, vnode.elm, refElm);\n    }\n\n    function insert (parent, elm, ref$$1) {\n      if (isDef(parent)) {\n        if (isDef(ref$$1)) {\n          if (nodeOps.parentNode(ref$$1) === parent) {\n            nodeOps.insertBefore(parent, elm, ref$$1);\n          }\n        } else {\n          nodeOps.appendChild(parent, elm);\n        }\n      }\n    }\n\n    function createChildren (vnode, children, insertedVnodeQueue) {\n      if (Array.isArray(children)) {\n        {\n          checkDuplicateKeys(children);\n        }\n        for (var i = 0; i < children.length; ++i) {\n          createElm(children[i], insertedVnodeQueue, vnode.elm, null, true, children, i);\n        }\n      } else if (isPrimitive(vnode.text)) {\n        nodeOps.appendChild(vnode.elm, nodeOps.createTextNode(String(vnode.text)));\n      }\n    }\n\n    function isPatchable (vnode) {\n      while (vnode.componentInstance) {\n        vnode = vnode.componentInstance._vnode;\n      }\n      return isDef(vnode.tag)\n    }\n\n    function invokeCreateHooks (vnode, insertedVnodeQueue) {\n      for (var i$1 = 0; i$1 < cbs.create.length; ++i$1) {\n        cbs.create[i$1](emptyNode, vnode);\n      }\n      i = vnode.data.hook; // Reuse variable\n      if (isDef(i)) {\n        if (isDef(i.create)) { i.create(emptyNode, vnode); }\n        if (isDef(i.insert)) { insertedVnodeQueue.push(vnode); }\n      }\n    }\n\n    // set scope id attribute for scoped CSS.\n    // this is implemented as a special case to avoid the overhead\n    // of going through the normal attribute patching process.\n    function setScope (vnode) {\n      var i;\n      if (isDef(i = vnode.fnScopeId)) {\n        nodeOps.setStyleScope(vnode.elm, i);\n      } else {\n        var ancestor = vnode;\n        while (ancestor) {\n          if (isDef(i = ancestor.context) && isDef(i = i.$options._scopeId)) {\n            nodeOps.setStyleScope(vnode.elm, i);\n          }\n          ancestor = ancestor.parent;\n        }\n      }\n      // for slot content they should also get the scopeId from the host instance.\n      if (isDef(i = activeInstance) &&\n        i !== vnode.context &&\n        i !== vnode.fnContext &&\n        isDef(i = i.$options._scopeId)\n      ) {\n        nodeOps.setStyleScope(vnode.elm, i);\n      }\n    }\n\n    function addVnodes (parentElm, refElm, vnodes, startIdx, endIdx, insertedVnodeQueue) {\n      for (; startIdx <= endIdx; ++startIdx) {\n        createElm(vnodes[startIdx], insertedVnodeQueue, parentElm, refElm, false, vnodes, startIdx);\n      }\n    }\n\n    function invokeDestroyHook (vnode) {\n      var i, j;\n      var data = vnode.data;\n      if (isDef(data)) {\n        if (isDef(i = data.hook) && isDef(i = i.destroy)) { i(vnode); }\n        for (i = 0; i < cbs.destroy.length; ++i) { cbs.destroy[i](vnode); }\n      }\n      if (isDef(i = vnode.children)) {\n        for (j = 0; j < vnode.children.length; ++j) {\n          invokeDestroyHook(vnode.children[j]);\n        }\n      }\n    }\n\n    function removeVnodes (vnodes, startIdx, endIdx) {\n      for (; startIdx <= endIdx; ++startIdx) {\n        var ch = vnodes[startIdx];\n        if (isDef(ch)) {\n          if (isDef(ch.tag)) {\n            removeAndInvokeRemoveHook(ch);\n            invokeDestroyHook(ch);\n          } else { // Text node\n            removeNode(ch.elm);\n          }\n        }\n      }\n    }\n\n    function removeAndInvokeRemoveHook (vnode, rm) {\n      if (isDef(rm) || isDef(vnode.data)) {\n        var i;\n        var listeners = cbs.remove.length + 1;\n        if (isDef(rm)) {\n          // we have a recursively passed down rm callback\n          // increase the listeners count\n          rm.listeners += listeners;\n        } else {\n          // directly removing\n          rm = createRmCb(vnode.elm, listeners);\n        }\n        // recursively invoke hooks on child component root node\n        if (isDef(i = vnode.componentInstance) && isDef(i = i._vnode) && isDef(i.data)) {\n          removeAndInvokeRemoveHook(i, rm);\n        }\n        for (i = 0; i < cbs.remove.length; ++i) {\n          cbs.remove[i](vnode, rm);\n        }\n        if (isDef(i = vnode.data.hook) && isDef(i = i.remove)) {\n          i(vnode, rm);\n        } else {\n          rm();\n        }\n      } else {\n        removeNode(vnode.elm);\n      }\n    }\n\n    function updateChildren (parentElm, oldCh, newCh, insertedVnodeQueue, removeOnly) {\n      var oldStartIdx = 0;\n      var newStartIdx = 0;\n      var oldEndIdx = oldCh.length - 1;\n      var oldStartVnode = oldCh[0];\n      var oldEndVnode = oldCh[oldEndIdx];\n      var newEndIdx = newCh.length - 1;\n      var newStartVnode = newCh[0];\n      var newEndVnode = newCh[newEndIdx];\n      var oldKeyToIdx, idxInOld, vnodeToMove, refElm;\n\n      // removeOnly is a special flag used only by <transition-group>\n      // to ensure removed elements stay in correct relative positions\n      // during leaving transitions\n      var canMove = !removeOnly;\n\n      {\n        checkDuplicateKeys(newCh);\n      }\n\n      while (oldStartIdx <= oldEndIdx && newStartIdx <= newEndIdx) {\n        if (isUndef(oldStartVnode)) {\n          oldStartVnode = oldCh[++oldStartIdx]; // Vnode has been moved left\n        } else if (isUndef(oldEndVnode)) {\n          oldEndVnode = oldCh[--oldEndIdx];\n        } else if (sameVnode(oldStartVnode, newStartVnode)) {\n          patchVnode(oldStartVnode, newStartVnode, insertedVnodeQueue, newCh, newStartIdx);\n          oldStartVnode = oldCh[++oldStartIdx];\n          newStartVnode = newCh[++newStartIdx];\n        } else if (sameVnode(oldEndVnode, newEndVnode)) {\n          patchVnode(oldEndVnode, newEndVnode, insertedVnodeQueue, newCh, newEndIdx);\n          oldEndVnode = oldCh[--oldEndIdx];\n          newEndVnode = newCh[--newEndIdx];\n        } else if (sameVnode(oldStartVnode, newEndVnode)) { // Vnode moved right\n          patchVnode(oldStartVnode, newEndVnode, insertedVnodeQueue, newCh, newEndIdx);\n          canMove && nodeOps.insertBefore(parentElm, oldStartVnode.elm, nodeOps.nextSibling(oldEndVnode.elm));\n          oldStartVnode = oldCh[++oldStartIdx];\n          newEndVnode = newCh[--newEndIdx];\n        } else if (sameVnode(oldEndVnode, newStartVnode)) { // Vnode moved left\n          patchVnode(oldEndVnode, newStartVnode, insertedVnodeQueue, newCh, newStartIdx);\n          canMove && nodeOps.insertBefore(parentElm, oldEndVnode.elm, oldStartVnode.elm);\n          oldEndVnode = oldCh[--oldEndIdx];\n          newStartVnode = newCh[++newStartIdx];\n        } else {\n          if (isUndef(oldKeyToIdx)) { oldKeyToIdx = createKeyToOldIdx(oldCh, oldStartIdx, oldEndIdx); }\n          idxInOld = isDef(newStartVnode.key)\n            ? oldKeyToIdx[newStartVnode.key]\n            : findIdxInOld(newStartVnode, oldCh, oldStartIdx, oldEndIdx);\n          if (isUndef(idxInOld)) { // New element\n            createElm(newStartVnode, insertedVnodeQueue, parentElm, oldStartVnode.elm, false, newCh, newStartIdx);\n          } else {\n            vnodeToMove = oldCh[idxInOld];\n            if (sameVnode(vnodeToMove, newStartVnode)) {\n              patchVnode(vnodeToMove, newStartVnode, insertedVnodeQueue, newCh, newStartIdx);\n              oldCh[idxInOld] = undefined;\n              canMove && nodeOps.insertBefore(parentElm, vnodeToMove.elm, oldStartVnode.elm);\n            } else {\n              // same key but different element. treat as new element\n              createElm(newStartVnode, insertedVnodeQueue, parentElm, oldStartVnode.elm, false, newCh, newStartIdx);\n            }\n          }\n          newStartVnode = newCh[++newStartIdx];\n        }\n      }\n      if (oldStartIdx > oldEndIdx) {\n        refElm = isUndef(newCh[newEndIdx + 1]) ? null : newCh[newEndIdx + 1].elm;\n        addVnodes(parentElm, refElm, newCh, newStartIdx, newEndIdx, insertedVnodeQueue);\n      } else if (newStartIdx > newEndIdx) {\n        removeVnodes(oldCh, oldStartIdx, oldEndIdx);\n      }\n    }\n\n    function checkDuplicateKeys (children) {\n      var seenKeys = {};\n      for (var i = 0; i < children.length; i++) {\n        var vnode = children[i];\n        var key = vnode.key;\n        if (isDef(key)) {\n          if (seenKeys[key]) {\n            warn(\n              (\"Duplicate keys detected: '\" + key + \"'. This may cause an update error.\"),\n              vnode.context\n            );\n          } else {\n            seenKeys[key] = true;\n          }\n        }\n      }\n    }\n\n    function findIdxInOld (node, oldCh, start, end) {\n      for (var i = start; i < end; i++) {\n        var c = oldCh[i];\n        if (isDef(c) && sameVnode(node, c)) { return i }\n      }\n    }\n\n    function patchVnode (\n      oldVnode,\n      vnode,\n      insertedVnodeQueue,\n      ownerArray,\n      index,\n      removeOnly\n    ) {\n      if (oldVnode === vnode) {\n        return\n      }\n\n      if (isDef(vnode.elm) && isDef(ownerArray)) {\n        // clone reused vnode\n        vnode = ownerArray[index] = cloneVNode(vnode);\n      }\n\n      var elm = vnode.elm = oldVnode.elm;\n\n      if (isTrue(oldVnode.isAsyncPlaceholder)) {\n        if (isDef(vnode.asyncFactory.resolved)) {\n          hydrate(oldVnode.elm, vnode, insertedVnodeQueue);\n        } else {\n          vnode.isAsyncPlaceholder = true;\n        }\n        return\n      }\n\n      // reuse element for static trees.\n      // note we only do this if the vnode is cloned -\n      // if the new node is not cloned it means the render functions have been\n      // reset by the hot-reload-api and we need to do a proper re-render.\n      if (isTrue(vnode.isStatic) &&\n        isTrue(oldVnode.isStatic) &&\n        vnode.key === oldVnode.key &&\n        (isTrue(vnode.isCloned) || isTrue(vnode.isOnce))\n      ) {\n        vnode.componentInstance = oldVnode.componentInstance;\n        return\n      }\n\n      var i;\n      var data = vnode.data;\n      if (isDef(data) && isDef(i = data.hook) && isDef(i = i.prepatch)) {\n        i(oldVnode, vnode);\n      }\n\n      var oldCh = oldVnode.children;\n      var ch = vnode.children;\n      if (isDef(data) && isPatchable(vnode)) {\n        for (i = 0; i < cbs.update.length; ++i) { cbs.update[i](oldVnode, vnode); }\n        if (isDef(i = data.hook) && isDef(i = i.update)) { i(oldVnode, vnode); }\n      }\n      if (isUndef(vnode.text)) {\n        if (isDef(oldCh) && isDef(ch)) {\n          if (oldCh !== ch) { updateChildren(elm, oldCh, ch, insertedVnodeQueue, removeOnly); }\n        } else if (isDef(ch)) {\n          {\n            checkDuplicateKeys(ch);\n          }\n          if (isDef(oldVnode.text)) { nodeOps.setTextContent(elm, ''); }\n          addVnodes(elm, null, ch, 0, ch.length - 1, insertedVnodeQueue);\n        } else if (isDef(oldCh)) {\n          removeVnodes(oldCh, 0, oldCh.length - 1);\n        } else if (isDef(oldVnode.text)) {\n          nodeOps.setTextContent(elm, '');\n        }\n      } else if (oldVnode.text !== vnode.text) {\n        nodeOps.setTextContent(elm, vnode.text);\n      }\n      if (isDef(data)) {\n        if (isDef(i = data.hook) && isDef(i = i.postpatch)) { i(oldVnode, vnode); }\n      }\n    }\n\n    function invokeInsertHook (vnode, queue, initial) {\n      // delay insert hooks for component root nodes, invoke them after the\n      // element is really inserted\n      if (isTrue(initial) && isDef(vnode.parent)) {\n        vnode.parent.data.pendingInsert = queue;\n      } else {\n        for (var i = 0; i < queue.length; ++i) {\n          queue[i].data.hook.insert(queue[i]);\n        }\n      }\n    }\n\n    var hydrationBailed = false;\n    // list of modules that can skip create hook during hydration because they\n    // are already rendered on the client or has no need for initialization\n    // Note: style is excluded because it relies on initial clone for future\n    // deep updates (#7063).\n    var isRenderedModule = makeMap('attrs,class,staticClass,staticStyle,key');\n\n    // Note: this is a browser-only function so we can assume elms are DOM nodes.\n    function hydrate (elm, vnode, insertedVnodeQueue, inVPre) {\n      var i;\n      var tag = vnode.tag;\n      var data = vnode.data;\n      var children = vnode.children;\n      inVPre = inVPre || (data && data.pre);\n      vnode.elm = elm;\n\n      if (isTrue(vnode.isComment) && isDef(vnode.asyncFactory)) {\n        vnode.isAsyncPlaceholder = true;\n        return true\n      }\n      // assert node match\n      {\n        if (!assertNodeMatch(elm, vnode, inVPre)) {\n          return false\n        }\n      }\n      if (isDef(data)) {\n        if (isDef(i = data.hook) && isDef(i = i.init)) { i(vnode, true /* hydrating */); }\n        if (isDef(i = vnode.componentInstance)) {\n          // child component. it should have hydrated its own tree.\n          initComponent(vnode, insertedVnodeQueue);\n          return true\n        }\n      }\n      if (isDef(tag)) {\n        if (isDef(children)) {\n          // empty element, allow client to pick up and populate children\n          if (!elm.hasChildNodes()) {\n            createChildren(vnode, children, insertedVnodeQueue);\n          } else {\n            // v-html and domProps: innerHTML\n            if (isDef(i = data) && isDef(i = i.domProps) && isDef(i = i.innerHTML)) {\n              if (i !== elm.innerHTML) {\n                /* istanbul ignore if */\n                if (typeof console !== 'undefined' &&\n                  !hydrationBailed\n                ) {\n                  hydrationBailed = true;\n                  console.warn('Parent: ', elm);\n                  console.warn('server innerHTML: ', i);\n                  console.warn('client innerHTML: ', elm.innerHTML);\n                }\n                return false\n              }\n            } else {\n              // iterate and compare children lists\n              var childrenMatch = true;\n              var childNode = elm.firstChild;\n              for (var i$1 = 0; i$1 < children.length; i$1++) {\n                if (!childNode || !hydrate(childNode, children[i$1], insertedVnodeQueue, inVPre)) {\n                  childrenMatch = false;\n                  break\n                }\n                childNode = childNode.nextSibling;\n              }\n              // if childNode is not null, it means the actual childNodes list is\n              // longer than the virtual children list.\n              if (!childrenMatch || childNode) {\n                /* istanbul ignore if */\n                if (typeof console !== 'undefined' &&\n                  !hydrationBailed\n                ) {\n                  hydrationBailed = true;\n                  console.warn('Parent: ', elm);\n                  console.warn('Mismatching childNodes vs. VNodes: ', elm.childNodes, children);\n                }\n                return false\n              }\n            }\n          }\n        }\n        if (isDef(data)) {\n          var fullInvoke = false;\n          for (var key in data) {\n            if (!isRenderedModule(key)) {\n              fullInvoke = true;\n              invokeCreateHooks(vnode, insertedVnodeQueue);\n              break\n            }\n          }\n          if (!fullInvoke && data['class']) {\n            // ensure collecting deps for deep class bindings for future updates\n            traverse(data['class']);\n          }\n        }\n      } else if (elm.data !== vnode.text) {\n        elm.data = vnode.text;\n      }\n      return true\n    }\n\n    function assertNodeMatch (node, vnode, inVPre) {\n      if (isDef(vnode.tag)) {\n        return vnode.tag.indexOf('vue-component') === 0 || (\n          !isUnknownElement$$1(vnode, inVPre) &&\n          vnode.tag.toLowerCase() === (node.tagName && node.tagName.toLowerCase())\n        )\n      } else {\n        return node.nodeType === (vnode.isComment ? 8 : 3)\n      }\n    }\n\n    return function patch (oldVnode, vnode, hydrating, removeOnly) {\n      if (isUndef(vnode)) {\n        if (isDef(oldVnode)) { invokeDestroyHook(oldVnode); }\n        return\n      }\n\n      var isInitialPatch = false;\n      var insertedVnodeQueue = [];\n\n      if (isUndef(oldVnode)) {\n        // empty mount (likely as component), create new root element\n        isInitialPatch = true;\n        createElm(vnode, insertedVnodeQueue);\n      } else {\n        var isRealElement = isDef(oldVnode.nodeType);\n        if (!isRealElement && sameVnode(oldVnode, vnode)) {\n          // patch existing root node\n          patchVnode(oldVnode, vnode, insertedVnodeQueue, null, null, removeOnly);\n        } else {\n          if (isRealElement) {\n            // mounting to a real element\n            // check if this is server-rendered content and if we can perform\n            // a successful hydration.\n            if (oldVnode.nodeType === 1 && oldVnode.hasAttribute(SSR_ATTR)) {\n              oldVnode.removeAttribute(SSR_ATTR);\n              hydrating = true;\n            }\n            if (isTrue(hydrating)) {\n              if (hydrate(oldVnode, vnode, insertedVnodeQueue)) {\n                invokeInsertHook(vnode, insertedVnodeQueue, true);\n                return oldVnode\n              } else {\n                warn(\n                  'The client-side rendered virtual DOM tree is not matching ' +\n                  'server-rendered content. This is likely caused by incorrect ' +\n                  'HTML markup, for example nesting block-level elements inside ' +\n                  '<p>, or missing <tbody>. Bailing hydration and performing ' +\n                  'full client-side render.'\n                );\n              }\n            }\n            // either not server-rendered, or hydration failed.\n            // create an empty node and replace it\n            oldVnode = emptyNodeAt(oldVnode);\n          }\n\n          // replacing existing element\n          var oldElm = oldVnode.elm;\n          var parentElm = nodeOps.parentNode(oldElm);\n\n          // create new node\n          createElm(\n            vnode,\n            insertedVnodeQueue,\n            // extremely rare edge case: do not insert if old element is in a\n            // leaving transition. Only happens when combining transition +\n            // keep-alive + HOCs. (#4590)\n            oldElm._leaveCb ? null : parentElm,\n            nodeOps.nextSibling(oldElm)\n          );\n\n          // update parent placeholder node element, recursively\n          if (isDef(vnode.parent)) {\n            var ancestor = vnode.parent;\n            var patchable = isPatchable(vnode);\n            while (ancestor) {\n              for (var i = 0; i < cbs.destroy.length; ++i) {\n                cbs.destroy[i](ancestor);\n              }\n              ancestor.elm = vnode.elm;\n              if (patchable) {\n                for (var i$1 = 0; i$1 < cbs.create.length; ++i$1) {\n                  cbs.create[i$1](emptyNode, ancestor);\n                }\n                // #6513\n                // invoke insert hooks that may have been merged by create hooks.\n                // e.g. for directives that uses the \"inserted\" hook.\n                var insert = ancestor.data.hook.insert;\n                if (insert.merged) {\n                  // start at index 1 to avoid re-invoking component mounted hook\n                  for (var i$2 = 1; i$2 < insert.fns.length; i$2++) {\n                    insert.fns[i$2]();\n                  }\n                }\n              } else {\n                registerRef(ancestor);\n              }\n              ancestor = ancestor.parent;\n            }\n          }\n\n          // destroy old node\n          if (isDef(parentElm)) {\n            removeVnodes([oldVnode], 0, 0);\n          } else if (isDef(oldVnode.tag)) {\n            invokeDestroyHook(oldVnode);\n          }\n        }\n      }\n\n      invokeInsertHook(vnode, insertedVnodeQueue, isInitialPatch);\n      return vnode.elm\n    }\n  }\n\n  /*  */\n\n  var directives = {\n    create: updateDirectives,\n    update: updateDirectives,\n    destroy: function unbindDirectives (vnode) {\n      updateDirectives(vnode, emptyNode);\n    }\n  };\n\n  function updateDirectives (oldVnode, vnode) {\n    if (oldVnode.data.directives || vnode.data.directives) {\n      _update(oldVnode, vnode);\n    }\n  }\n\n  function _update (oldVnode, vnode) {\n    var isCreate = oldVnode === emptyNode;\n    var isDestroy = vnode === emptyNode;\n    var oldDirs = normalizeDirectives$1(oldVnode.data.directives, oldVnode.context);\n    var newDirs = normalizeDirectives$1(vnode.data.directives, vnode.context);\n\n    var dirsWithInsert = [];\n    var dirsWithPostpatch = [];\n\n    var key, oldDir, dir;\n    for (key in newDirs) {\n      oldDir = oldDirs[key];\n      dir = newDirs[key];\n      if (!oldDir) {\n        // new directive, bind\n        callHook$1(dir, 'bind', vnode, oldVnode);\n        if (dir.def && dir.def.inserted) {\n          dirsWithInsert.push(dir);\n        }\n      } else {\n        // existing directive, update\n        dir.oldValue = oldDir.value;\n        dir.oldArg = oldDir.arg;\n        callHook$1(dir, 'update', vnode, oldVnode);\n        if (dir.def && dir.def.componentUpdated) {\n          dirsWithPostpatch.push(dir);\n        }\n      }\n    }\n\n    if (dirsWithInsert.length) {\n      var callInsert = function () {\n        for (var i = 0; i < dirsWithInsert.length; i++) {\n          callHook$1(dirsWithInsert[i], 'inserted', vnode, oldVnode);\n        }\n      };\n      if (isCreate) {\n        mergeVNodeHook(vnode, 'insert', callInsert);\n      } else {\n        callInsert();\n      }\n    }\n\n    if (dirsWithPostpatch.length) {\n      mergeVNodeHook(vnode, 'postpatch', function () {\n        for (var i = 0; i < dirsWithPostpatch.length; i++) {\n          callHook$1(dirsWithPostpatch[i], 'componentUpdated', vnode, oldVnode);\n        }\n      });\n    }\n\n    if (!isCreate) {\n      for (key in oldDirs) {\n        if (!newDirs[key]) {\n          // no longer present, unbind\n          callHook$1(oldDirs[key], 'unbind', oldVnode, oldVnode, isDestroy);\n        }\n      }\n    }\n  }\n\n  var emptyModifiers = Object.create(null);\n\n  function normalizeDirectives$1 (\n    dirs,\n    vm\n  ) {\n    var res = Object.create(null);\n    if (!dirs) {\n      // $flow-disable-line\n      return res\n    }\n    var i, dir;\n    for (i = 0; i < dirs.length; i++) {\n      dir = dirs[i];\n      if (!dir.modifiers) {\n        // $flow-disable-line\n        dir.modifiers = emptyModifiers;\n      }\n      res[getRawDirName(dir)] = dir;\n      dir.def = resolveAsset(vm.$options, 'directives', dir.name, true);\n    }\n    // $flow-disable-line\n    return res\n  }\n\n  function getRawDirName (dir) {\n    return dir.rawName || ((dir.name) + \".\" + (Object.keys(dir.modifiers || {}).join('.')))\n  }\n\n  function callHook$1 (dir, hook, vnode, oldVnode, isDestroy) {\n    var fn = dir.def && dir.def[hook];\n    if (fn) {\n      try {\n        fn(vnode.elm, dir, vnode, oldVnode, isDestroy);\n      } catch (e) {\n        handleError(e, vnode.context, (\"directive \" + (dir.name) + \" \" + hook + \" hook\"));\n      }\n    }\n  }\n\n  var baseModules = [\n    ref,\n    directives\n  ];\n\n  /*  */\n\n  function updateAttrs (oldVnode, vnode) {\n    var opts = vnode.componentOptions;\n    if (isDef(opts) && opts.Ctor.options.inheritAttrs === false) {\n      return\n    }\n    if (isUndef(oldVnode.data.attrs) && isUndef(vnode.data.attrs)) {\n      return\n    }\n    var key, cur, old;\n    var elm = vnode.elm;\n    var oldAttrs = oldVnode.data.attrs || {};\n    var attrs = vnode.data.attrs || {};\n    // clone observed objects, as the user probably wants to mutate it\n    if (isDef(attrs.__ob__)) {\n      attrs = vnode.data.attrs = extend({}, attrs);\n    }\n\n    for (key in attrs) {\n      cur = attrs[key];\n      old = oldAttrs[key];\n      if (old !== cur) {\n        setAttr(elm, key, cur);\n      }\n    }\n    // #4391: in IE9, setting type can reset value for input[type=radio]\n    // #6666: IE/Edge forces progress value down to 1 before setting a max\n    /* istanbul ignore if */\n    if ((isIE || isEdge) && attrs.value !== oldAttrs.value) {\n      setAttr(elm, 'value', attrs.value);\n    }\n    for (key in oldAttrs) {\n      if (isUndef(attrs[key])) {\n        if (isXlink(key)) {\n          elm.removeAttributeNS(xlinkNS, getXlinkProp(key));\n        } else if (!isEnumeratedAttr(key)) {\n          elm.removeAttribute(key);\n        }\n      }\n    }\n  }\n\n  function setAttr (el, key, value) {\n    if (el.tagName.indexOf('-') > -1) {\n      baseSetAttr(el, key, value);\n    } else if (isBooleanAttr(key)) {\n      // set attribute for blank value\n      // e.g. <option disabled>Select one</option>\n      if (isFalsyAttrValue(value)) {\n        el.removeAttribute(key);\n      } else {\n        // technically allowfullscreen is a boolean attribute for <iframe>,\n        // but Flash expects a value of \"true\" when used on <embed> tag\n        value = key === 'allowfullscreen' && el.tagName === 'EMBED'\n          ? 'true'\n          : key;\n        el.setAttribute(key, value);\n      }\n    } else if (isEnumeratedAttr(key)) {\n      el.setAttribute(key, convertEnumeratedValue(key, value));\n    } else if (isXlink(key)) {\n      if (isFalsyAttrValue(value)) {\n        el.removeAttributeNS(xlinkNS, getXlinkProp(key));\n      } else {\n        el.setAttributeNS(xlinkNS, key, value);\n      }\n    } else {\n      baseSetAttr(el, key, value);\n    }\n  }\n\n  function baseSetAttr (el, key, value) {\n    if (isFalsyAttrValue(value)) {\n      el.removeAttribute(key);\n    } else {\n      // #7138: IE10 & 11 fires input event when setting placeholder on\n      // <textarea>... block the first input event and remove the blocker\n      // immediately.\n      /* istanbul ignore if */\n      if (\n        isIE && !isIE9 &&\n        el.tagName === 'TEXTAREA' &&\n        key === 'placeholder' && value !== '' && !el.__ieph\n      ) {\n        var blocker = function (e) {\n          e.stopImmediatePropagation();\n          el.removeEventListener('input', blocker);\n        };\n        el.addEventListener('input', blocker);\n        // $flow-disable-line\n        el.__ieph = true; /* IE placeholder patched */\n      }\n      el.setAttribute(key, value);\n    }\n  }\n\n  var attrs = {\n    create: updateAttrs,\n    update: updateAttrs\n  };\n\n  /*  */\n\n  function updateClass (oldVnode, vnode) {\n    var el = vnode.elm;\n    var data = vnode.data;\n    var oldData = oldVnode.data;\n    if (\n      isUndef(data.staticClass) &&\n      isUndef(data.class) && (\n        isUndef(oldData) || (\n          isUndef(oldData.staticClass) &&\n          isUndef(oldData.class)\n        )\n      )\n    ) {\n      return\n    }\n\n    var cls = genClassForVnode(vnode);\n\n    // handle transition classes\n    var transitionClass = el._transitionClasses;\n    if (isDef(transitionClass)) {\n      cls = concat(cls, stringifyClass(transitionClass));\n    }\n\n    // set the class\n    if (cls !== el._prevClass) {\n      el.setAttribute('class', cls);\n      el._prevClass = cls;\n    }\n  }\n\n  var klass = {\n    create: updateClass,\n    update: updateClass\n  };\n\n  /*  */\n\n  var validDivisionCharRE = /[\\w).+\\-_$\\]]/;\n\n  function parseFilters (exp) {\n    var inSingle = false;\n    var inDouble = false;\n    var inTemplateString = false;\n    var inRegex = false;\n    var curly = 0;\n    var square = 0;\n    var paren = 0;\n    var lastFilterIndex = 0;\n    var c, prev, i, expression, filters;\n\n    for (i = 0; i < exp.length; i++) {\n      prev = c;\n      c = exp.charCodeAt(i);\n      if (inSingle) {\n        if (c === 0x27 && prev !== 0x5C) { inSingle = false; }\n      } else if (inDouble) {\n        if (c === 0x22 && prev !== 0x5C) { inDouble = false; }\n      } else if (inTemplateString) {\n        if (c === 0x60 && prev !== 0x5C) { inTemplateString = false; }\n      } else if (inRegex) {\n        if (c === 0x2f && prev !== 0x5C) { inRegex = false; }\n      } else if (\n        c === 0x7C && // pipe\n        exp.charCodeAt(i + 1) !== 0x7C &&\n        exp.charCodeAt(i - 1) !== 0x7C &&\n        !curly && !square && !paren\n      ) {\n        if (expression === undefined) {\n          // first filter, end of expression\n          lastFilterIndex = i + 1;\n          expression = exp.slice(0, i).trim();\n        } else {\n          pushFilter();\n        }\n      } else {\n        switch (c) {\n          case 0x22: inDouble = true; break         // \"\n          case 0x27: inSingle = true; break         // '\n          case 0x60: inTemplateString = true; break // `\n          case 0x28: paren++; break                 // (\n          case 0x29: paren--; break                 // )\n          case 0x5B: square++; break                // [\n          case 0x5D: square--; break                // ]\n          case 0x7B: curly++; break                 // {\n          case 0x7D: curly--; break                 // }\n        }\n        if (c === 0x2f) { // /\n          var j = i - 1;\n          var p = (void 0);\n          // find first non-whitespace prev char\n          for (; j >= 0; j--) {\n            p = exp.charAt(j);\n            if (p !== ' ') { break }\n          }\n          if (!p || !validDivisionCharRE.test(p)) {\n            inRegex = true;\n          }\n        }\n      }\n    }\n\n    if (expression === undefined) {\n      expression = exp.slice(0, i).trim();\n    } else if (lastFilterIndex !== 0) {\n      pushFilter();\n    }\n\n    function pushFilter () {\n      (filters || (filters = [])).push(exp.slice(lastFilterIndex, i).trim());\n      lastFilterIndex = i + 1;\n    }\n\n    if (filters) {\n      for (i = 0; i < filters.length; i++) {\n        expression = wrapFilter(expression, filters[i]);\n      }\n    }\n\n    return expression\n  }\n\n  function wrapFilter (exp, filter) {\n    var i = filter.indexOf('(');\n    if (i < 0) {\n      // _f: resolveFilter\n      return (\"_f(\\\"\" + filter + \"\\\")(\" + exp + \")\")\n    } else {\n      var name = filter.slice(0, i);\n      var args = filter.slice(i + 1);\n      return (\"_f(\\\"\" + name + \"\\\")(\" + exp + (args !== ')' ? ',' + args : args))\n    }\n  }\n\n  /*  */\n\n\n\n  /* eslint-disable no-unused-vars */\n  function baseWarn (msg, range) {\n    console.error((\"[Vue compiler]: \" + msg));\n  }\n  /* eslint-enable no-unused-vars */\n\n  function pluckModuleFunction (\n    modules,\n    key\n  ) {\n    return modules\n      ? modules.map(function (m) { return m[key]; }).filter(function (_) { return _; })\n      : []\n  }\n\n  function addProp (el, name, value, range, dynamic) {\n    (el.props || (el.props = [])).push(rangeSetItem({ name: name, value: value, dynamic: dynamic }, range));\n    el.plain = false;\n  }\n\n  function addAttr (el, name, value, range, dynamic) {\n    var attrs = dynamic\n      ? (el.dynamicAttrs || (el.dynamicAttrs = []))\n      : (el.attrs || (el.attrs = []));\n    attrs.push(rangeSetItem({ name: name, value: value, dynamic: dynamic }, range));\n    el.plain = false;\n  }\n\n  // add a raw attr (use this in preTransforms)\n  function addRawAttr (el, name, value, range) {\n    el.attrsMap[name] = value;\n    el.attrsList.push(rangeSetItem({ name: name, value: value }, range));\n  }\n\n  function addDirective (\n    el,\n    name,\n    rawName,\n    value,\n    arg,\n    isDynamicArg,\n    modifiers,\n    range\n  ) {\n    (el.directives || (el.directives = [])).push(rangeSetItem({\n      name: name,\n      rawName: rawName,\n      value: value,\n      arg: arg,\n      isDynamicArg: isDynamicArg,\n      modifiers: modifiers\n    }, range));\n    el.plain = false;\n  }\n\n  function prependModifierMarker (symbol, name, dynamic) {\n    return dynamic\n      ? (\"_p(\" + name + \",\\\"\" + symbol + \"\\\")\")\n      : symbol + name // mark the event as captured\n  }\n\n  function addHandler (\n    el,\n    name,\n    value,\n    modifiers,\n    important,\n    warn,\n    range,\n    dynamic\n  ) {\n    modifiers = modifiers || emptyObject;\n    // warn prevent and passive modifier\n    /* istanbul ignore if */\n    if (\n      warn &&\n      modifiers.prevent && modifiers.passive\n    ) {\n      warn(\n        'passive and prevent can\\'t be used together. ' +\n        'Passive handler can\\'t prevent default event.',\n        range\n      );\n    }\n\n    // normalize click.right and click.middle since they don't actually fire\n    // this is technically browser-specific, but at least for now browsers are\n    // the only target envs that have right/middle clicks.\n    if (modifiers.right) {\n      if (dynamic) {\n        name = \"(\" + name + \")==='click'?'contextmenu':(\" + name + \")\";\n      } else if (name === 'click') {\n        name = 'contextmenu';\n        delete modifiers.right;\n      }\n    } else if (modifiers.middle) {\n      if (dynamic) {\n        name = \"(\" + name + \")==='click'?'mouseup':(\" + name + \")\";\n      } else if (name === 'click') {\n        name = 'mouseup';\n      }\n    }\n\n    // check capture modifier\n    if (modifiers.capture) {\n      delete modifiers.capture;\n      name = prependModifierMarker('!', name, dynamic);\n    }\n    if (modifiers.once) {\n      delete modifiers.once;\n      name = prependModifierMarker('~', name, dynamic);\n    }\n    /* istanbul ignore if */\n    if (modifiers.passive) {\n      delete modifiers.passive;\n      name = prependModifierMarker('&', name, dynamic);\n    }\n\n    var events;\n    if (modifiers.native) {\n      delete modifiers.native;\n      events = el.nativeEvents || (el.nativeEvents = {});\n    } else {\n      events = el.events || (el.events = {});\n    }\n\n    var newHandler = rangeSetItem({ value: value.trim(), dynamic: dynamic }, range);\n    if (modifiers !== emptyObject) {\n      newHandler.modifiers = modifiers;\n    }\n\n    var handlers = events[name];\n    /* istanbul ignore if */\n    if (Array.isArray(handlers)) {\n      important ? handlers.unshift(newHandler) : handlers.push(newHandler);\n    } else if (handlers) {\n      events[name] = important ? [newHandler, handlers] : [handlers, newHandler];\n    } else {\n      events[name] = newHandler;\n    }\n\n    el.plain = false;\n  }\n\n  function getRawBindingAttr (\n    el,\n    name\n  ) {\n    return el.rawAttrsMap[':' + name] ||\n      el.rawAttrsMap['v-bind:' + name] ||\n      el.rawAttrsMap[name]\n  }\n\n  function getBindingAttr (\n    el,\n    name,\n    getStatic\n  ) {\n    var dynamicValue =\n      getAndRemoveAttr(el, ':' + name) ||\n      getAndRemoveAttr(el, 'v-bind:' + name);\n    if (dynamicValue != null) {\n      return parseFilters(dynamicValue)\n    } else if (getStatic !== false) {\n      var staticValue = getAndRemoveAttr(el, name);\n      if (staticValue != null) {\n        return JSON.stringify(staticValue)\n      }\n    }\n  }\n\n  // note: this only removes the attr from the Array (attrsList) so that it\n  // doesn't get processed by processAttrs.\n  // By default it does NOT remove it from the map (attrsMap) because the map is\n  // needed during codegen.\n  function getAndRemoveAttr (\n    el,\n    name,\n    removeFromMap\n  ) {\n    var val;\n    if ((val = el.attrsMap[name]) != null) {\n      var list = el.attrsList;\n      for (var i = 0, l = list.length; i < l; i++) {\n        if (list[i].name === name) {\n          list.splice(i, 1);\n          break\n        }\n      }\n    }\n    if (removeFromMap) {\n      delete el.attrsMap[name];\n    }\n    return val\n  }\n\n  function getAndRemoveAttrByRegex (\n    el,\n    name\n  ) {\n    var list = el.attrsList;\n    for (var i = 0, l = list.length; i < l; i++) {\n      var attr = list[i];\n      if (name.test(attr.name)) {\n        list.splice(i, 1);\n        return attr\n      }\n    }\n  }\n\n  function rangeSetItem (\n    item,\n    range\n  ) {\n    if (range) {\n      if (range.start != null) {\n        item.start = range.start;\n      }\n      if (range.end != null) {\n        item.end = range.end;\n      }\n    }\n    return item\n  }\n\n  /*  */\n\n  /**\n   * Cross-platform code generation for component v-model\n   */\n  function genComponentModel (\n    el,\n    value,\n    modifiers\n  ) {\n    var ref = modifiers || {};\n    var number = ref.number;\n    var trim = ref.trim;\n\n    var baseValueExpression = '$$v';\n    var valueExpression = baseValueExpression;\n    if (trim) {\n      valueExpression =\n        \"(typeof \" + baseValueExpression + \" === 'string'\" +\n        \"? \" + baseValueExpression + \".trim()\" +\n        \": \" + baseValueExpression + \")\";\n    }\n    if (number) {\n      valueExpression = \"_n(\" + valueExpression + \")\";\n    }\n    var assignment = genAssignmentCode(value, valueExpression);\n\n    el.model = {\n      value: (\"(\" + value + \")\"),\n      expression: JSON.stringify(value),\n      callback: (\"function (\" + baseValueExpression + \") {\" + assignment + \"}\")\n    };\n  }\n\n  /**\n   * Cross-platform codegen helper for generating v-model value assignment code.\n   */\n  function genAssignmentCode (\n    value,\n    assignment\n  ) {\n    var res = parseModel(value);\n    if (res.key === null) {\n      return (value + \"=\" + assignment)\n    } else {\n      return (\"$set(\" + (res.exp) + \", \" + (res.key) + \", \" + assignment + \")\")\n    }\n  }\n\n  /**\n   * Parse a v-model expression into a base path and a final key segment.\n   * Handles both dot-path and possible square brackets.\n   *\n   * Possible cases:\n   *\n   * - test\n   * - test[key]\n   * - test[test1[key]]\n   * - test[\"a\"][key]\n   * - xxx.test[a[a].test1[key]]\n   * - test.xxx.a[\"asa\"][test1[key]]\n   *\n   */\n\n  var len, str, chr, index$1, expressionPos, expressionEndPos;\n\n\n\n  function parseModel (val) {\n    // Fix https://github.com/vuejs/vue/pull/7730\n    // allow v-model=\"obj.val \" (trailing whitespace)\n    val = val.trim();\n    len = val.length;\n\n    if (val.indexOf('[') < 0 || val.lastIndexOf(']') < len - 1) {\n      index$1 = val.lastIndexOf('.');\n      if (index$1 > -1) {\n        return {\n          exp: val.slice(0, index$1),\n          key: '\"' + val.slice(index$1 + 1) + '\"'\n        }\n      } else {\n        return {\n          exp: val,\n          key: null\n        }\n      }\n    }\n\n    str = val;\n    index$1 = expressionPos = expressionEndPos = 0;\n\n    while (!eof()) {\n      chr = next();\n      /* istanbul ignore if */\n      if (isStringStart(chr)) {\n        parseString(chr);\n      } else if (chr === 0x5B) {\n        parseBracket(chr);\n      }\n    }\n\n    return {\n      exp: val.slice(0, expressionPos),\n      key: val.slice(expressionPos + 1, expressionEndPos)\n    }\n  }\n\n  function next () {\n    return str.charCodeAt(++index$1)\n  }\n\n  function eof () {\n    return index$1 >= len\n  }\n\n  function isStringStart (chr) {\n    return chr === 0x22 || chr === 0x27\n  }\n\n  function parseBracket (chr) {\n    var inBracket = 1;\n    expressionPos = index$1;\n    while (!eof()) {\n      chr = next();\n      if (isStringStart(chr)) {\n        parseString(chr);\n        continue\n      }\n      if (chr === 0x5B) { inBracket++; }\n      if (chr === 0x5D) { inBracket--; }\n      if (inBracket === 0) {\n        expressionEndPos = index$1;\n        break\n      }\n    }\n  }\n\n  function parseString (chr) {\n    var stringQuote = chr;\n    while (!eof()) {\n      chr = next();\n      if (chr === stringQuote) {\n        break\n      }\n    }\n  }\n\n  /*  */\n\n  var warn$1;\n\n  // in some cases, the event used has to be determined at runtime\n  // so we used some reserved tokens during compile.\n  var RANGE_TOKEN = '__r';\n  var CHECKBOX_RADIO_TOKEN = '__c';\n\n  function model (\n    el,\n    dir,\n    _warn\n  ) {\n    warn$1 = _warn;\n    var value = dir.value;\n    var modifiers = dir.modifiers;\n    var tag = el.tag;\n    var type = el.attrsMap.type;\n\n    {\n      // inputs with type=\"file\" are read only and setting the input's\n      // value will throw an error.\n      if (tag === 'input' && type === 'file') {\n        warn$1(\n          \"<\" + (el.tag) + \" v-model=\\\"\" + value + \"\\\" type=\\\"file\\\">:\\n\" +\n          \"File inputs are read only. Use a v-on:change listener instead.\",\n          el.rawAttrsMap['v-model']\n        );\n      }\n    }\n\n    if (el.component) {\n      genComponentModel(el, value, modifiers);\n      // component v-model doesn't need extra runtime\n      return false\n    } else if (tag === 'select') {\n      genSelect(el, value, modifiers);\n    } else if (tag === 'input' && type === 'checkbox') {\n      genCheckboxModel(el, value, modifiers);\n    } else if (tag === 'input' && type === 'radio') {\n      genRadioModel(el, value, modifiers);\n    } else if (tag === 'input' || tag === 'textarea') {\n      genDefaultModel(el, value, modifiers);\n    } else if (!config.isReservedTag(tag)) {\n      genComponentModel(el, value, modifiers);\n      // component v-model doesn't need extra runtime\n      return false\n    } else {\n      warn$1(\n        \"<\" + (el.tag) + \" v-model=\\\"\" + value + \"\\\">: \" +\n        \"v-model is not supported on this element type. \" +\n        'If you are working with contenteditable, it\\'s recommended to ' +\n        'wrap a library dedicated for that purpose inside a custom component.',\n        el.rawAttrsMap['v-model']\n      );\n    }\n\n    // ensure runtime directive metadata\n    return true\n  }\n\n  function genCheckboxModel (\n    el,\n    value,\n    modifiers\n  ) {\n    var number = modifiers && modifiers.number;\n    var valueBinding = getBindingAttr(el, 'value') || 'null';\n    var trueValueBinding = getBindingAttr(el, 'true-value') || 'true';\n    var falseValueBinding = getBindingAttr(el, 'false-value') || 'false';\n    addProp(el, 'checked',\n      \"Array.isArray(\" + value + \")\" +\n      \"?_i(\" + value + \",\" + valueBinding + \")>-1\" + (\n        trueValueBinding === 'true'\n          ? (\":(\" + value + \")\")\n          : (\":_q(\" + value + \",\" + trueValueBinding + \")\")\n      )\n    );\n    addHandler(el, 'change',\n      \"var $$a=\" + value + \",\" +\n          '$$el=$event.target,' +\n          \"$$c=$$el.checked?(\" + trueValueBinding + \"):(\" + falseValueBinding + \");\" +\n      'if(Array.isArray($$a)){' +\n        \"var $$v=\" + (number ? '_n(' + valueBinding + ')' : valueBinding) + \",\" +\n            '$$i=_i($$a,$$v);' +\n        \"if($$el.checked){$$i<0&&(\" + (genAssignmentCode(value, '$$a.concat([$$v])')) + \")}\" +\n        \"else{$$i>-1&&(\" + (genAssignmentCode(value, '$$a.slice(0,$$i).concat($$a.slice($$i+1))')) + \")}\" +\n      \"}else{\" + (genAssignmentCode(value, '$$c')) + \"}\",\n      null, true\n    );\n  }\n\n  function genRadioModel (\n    el,\n    value,\n    modifiers\n  ) {\n    var number = modifiers && modifiers.number;\n    var valueBinding = getBindingAttr(el, 'value') || 'null';\n    valueBinding = number ? (\"_n(\" + valueBinding + \")\") : valueBinding;\n    addProp(el, 'checked', (\"_q(\" + value + \",\" + valueBinding + \")\"));\n    addHandler(el, 'change', genAssignmentCode(value, valueBinding), null, true);\n  }\n\n  function genSelect (\n    el,\n    value,\n    modifiers\n  ) {\n    var number = modifiers && modifiers.number;\n    var selectedVal = \"Array.prototype.filter\" +\n      \".call($event.target.options,function(o){return o.selected})\" +\n      \".map(function(o){var val = \\\"_value\\\" in o ? o._value : o.value;\" +\n      \"return \" + (number ? '_n(val)' : 'val') + \"})\";\n\n    var assignment = '$event.target.multiple ? $$selectedVal : $$selectedVal[0]';\n    var code = \"var $$selectedVal = \" + selectedVal + \";\";\n    code = code + \" \" + (genAssignmentCode(value, assignment));\n    addHandler(el, 'change', code, null, true);\n  }\n\n  function genDefaultModel (\n    el,\n    value,\n    modifiers\n  ) {\n    var type = el.attrsMap.type;\n\n    // warn if v-bind:value conflicts with v-model\n    // except for inputs with v-bind:type\n    {\n      var value$1 = el.attrsMap['v-bind:value'] || el.attrsMap[':value'];\n      var typeBinding = el.attrsMap['v-bind:type'] || el.attrsMap[':type'];\n      if (value$1 && !typeBinding) {\n        var binding = el.attrsMap['v-bind:value'] ? 'v-bind:value' : ':value';\n        warn$1(\n          binding + \"=\\\"\" + value$1 + \"\\\" conflicts with v-model on the same element \" +\n          'because the latter already expands to a value binding internally',\n          el.rawAttrsMap[binding]\n        );\n      }\n    }\n\n    var ref = modifiers || {};\n    var lazy = ref.lazy;\n    var number = ref.number;\n    var trim = ref.trim;\n    var needCompositionGuard = !lazy && type !== 'range';\n    var event = lazy\n      ? 'change'\n      : type === 'range'\n        ? RANGE_TOKEN\n        : 'input';\n\n    var valueExpression = '$event.target.value';\n    if (trim) {\n      valueExpression = \"$event.target.value.trim()\";\n    }\n    if (number) {\n      valueExpression = \"_n(\" + valueExpression + \")\";\n    }\n\n    var code = genAssignmentCode(value, valueExpression);\n    if (needCompositionGuard) {\n      code = \"if($event.target.composing)return;\" + code;\n    }\n\n    addProp(el, 'value', (\"(\" + value + \")\"));\n    addHandler(el, event, code, null, true);\n    if (trim || number) {\n      addHandler(el, 'blur', '$forceUpdate()');\n    }\n  }\n\n  /*  */\n\n  // normalize v-model event tokens that can only be determined at runtime.\n  // it's important to place the event as the first in the array because\n  // the whole point is ensuring the v-model callback gets called before\n  // user-attached handlers.\n  function normalizeEvents (on) {\n    /* istanbul ignore if */\n    if (isDef(on[RANGE_TOKEN])) {\n      // IE input[type=range] only supports `change` event\n      var event = isIE ? 'change' : 'input';\n      on[event] = [].concat(on[RANGE_TOKEN], on[event] || []);\n      delete on[RANGE_TOKEN];\n    }\n    // This was originally intended to fix #4521 but no longer necessary\n    // after 2.5. Keeping it for backwards compat with generated code from < 2.4\n    /* istanbul ignore if */\n    if (isDef(on[CHECKBOX_RADIO_TOKEN])) {\n      on.change = [].concat(on[CHECKBOX_RADIO_TOKEN], on.change || []);\n      delete on[CHECKBOX_RADIO_TOKEN];\n    }\n  }\n\n  var target$1;\n\n  function createOnceHandler$1 (event, handler, capture) {\n    var _target = target$1; // save current target element in closure\n    return function onceHandler () {\n      var res = handler.apply(null, arguments);\n      if (res !== null) {\n        remove$2(event, onceHandler, capture, _target);\n      }\n    }\n  }\n\n  // #9446: Firefox <= 53 (in particular, ESR 52) has incorrect Event.timeStamp\n  // implementation and does not fire microtasks in between event propagation, so\n  // safe to exclude.\n  var useMicrotaskFix = isUsingMicroTask && !(isFF && Number(isFF[1]) <= 53);\n\n  function add$1 (\n    name,\n    handler,\n    capture,\n    passive\n  ) {\n    // async edge case #6566: inner click event triggers patch, event handler\n    // attached to outer element during patch, and triggered again. This\n    // happens because browsers fire microtask ticks between event propagation.\n    // the solution is simple: we save the timestamp when a handler is attached,\n    // and the handler would only fire if the event passed to it was fired\n    // AFTER it was attached.\n    if (useMicrotaskFix) {\n      var attachedTimestamp = currentFlushTimestamp;\n      var original = handler;\n      handler = original._wrapper = function (e) {\n        if (\n          // no bubbling, should always fire.\n          // this is just a safety net in case event.timeStamp is unreliable in\n          // certain weird environments...\n          e.target === e.currentTarget ||\n          // event is fired after handler attachment\n          e.timeStamp >= attachedTimestamp ||\n          // bail for environments that have buggy event.timeStamp implementations\n          // #9462 iOS 9 bug: event.timeStamp is 0 after history.pushState\n          // #9681 QtWebEngine event.timeStamp is negative value\n          e.timeStamp <= 0 ||\n          // #9448 bail if event is fired in another document in a multi-page\n          // electron/nw.js app, since event.timeStamp will be using a different\n          // starting reference\n          e.target.ownerDocument !== document\n        ) {\n          return original.apply(this, arguments)\n        }\n      };\n    }\n    target$1.addEventListener(\n      name,\n      handler,\n      supportsPassive\n        ? { capture: capture, passive: passive }\n        : capture\n    );\n  }\n\n  function remove$2 (\n    name,\n    handler,\n    capture,\n    _target\n  ) {\n    (_target || target$1).removeEventListener(\n      name,\n      handler._wrapper || handler,\n      capture\n    );\n  }\n\n  function updateDOMListeners (oldVnode, vnode) {\n    if (isUndef(oldVnode.data.on) && isUndef(vnode.data.on)) {\n      return\n    }\n    var on = vnode.data.on || {};\n    var oldOn = oldVnode.data.on || {};\n    target$1 = vnode.elm;\n    normalizeEvents(on);\n    updateListeners(on, oldOn, add$1, remove$2, createOnceHandler$1, vnode.context);\n    target$1 = undefined;\n  }\n\n  var events = {\n    create: updateDOMListeners,\n    update: updateDOMListeners\n  };\n\n  /*  */\n\n  var svgContainer;\n\n  function updateDOMProps (oldVnode, vnode) {\n    if (isUndef(oldVnode.data.domProps) && isUndef(vnode.data.domProps)) {\n      return\n    }\n    var key, cur;\n    var elm = vnode.elm;\n    var oldProps = oldVnode.data.domProps || {};\n    var props = vnode.data.domProps || {};\n    // clone observed objects, as the user probably wants to mutate it\n    if (isDef(props.__ob__)) {\n      props = vnode.data.domProps = extend({}, props);\n    }\n\n    for (key in oldProps) {\n      if (!(key in props)) {\n        elm[key] = '';\n      }\n    }\n\n    for (key in props) {\n      cur = props[key];\n      // ignore children if the node has textContent or innerHTML,\n      // as these will throw away existing DOM nodes and cause removal errors\n      // on subsequent patches (#3360)\n      if (key === 'textContent' || key === 'innerHTML') {\n        if (vnode.children) { vnode.children.length = 0; }\n        if (cur === oldProps[key]) { continue }\n        // #6601 work around Chrome version <= 55 bug where single textNode\n        // replaced by innerHTML/textContent retains its parentNode property\n        if (elm.childNodes.length === 1) {\n          elm.removeChild(elm.childNodes[0]);\n        }\n      }\n\n      if (key === 'value' && elm.tagName !== 'PROGRESS') {\n        // store value as _value as well since\n        // non-string values will be stringified\n        elm._value = cur;\n        // avoid resetting cursor position when value is the same\n        var strCur = isUndef(cur) ? '' : String(cur);\n        if (shouldUpdateValue(elm, strCur)) {\n          elm.value = strCur;\n        }\n      } else if (key === 'innerHTML' && isSVG(elm.tagName) && isUndef(elm.innerHTML)) {\n        // IE doesn't support innerHTML for SVG elements\n        svgContainer = svgContainer || document.createElement('div');\n        svgContainer.innerHTML = \"<svg>\" + cur + \"</svg>\";\n        var svg = svgContainer.firstChild;\n        while (elm.firstChild) {\n          elm.removeChild(elm.firstChild);\n        }\n        while (svg.firstChild) {\n          elm.appendChild(svg.firstChild);\n        }\n      } else if (\n        // skip the update if old and new VDOM state is the same.\n        // `value` is handled separately because the DOM value may be temporarily\n        // out of sync with VDOM state due to focus, composition and modifiers.\n        // This  #4521 by skipping the unnecesarry `checked` update.\n        cur !== oldProps[key]\n      ) {\n        // some property updates can throw\n        // e.g. `value` on <progress> w/ non-finite value\n        try {\n          elm[key] = cur;\n        } catch (e) {}\n      }\n    }\n  }\n\n  // check platforms/web/util/attrs.js acceptValue\n\n\n  function shouldUpdateValue (elm, checkVal) {\n    return (!elm.composing && (\n      elm.tagName === 'OPTION' ||\n      isNotInFocusAndDirty(elm, checkVal) ||\n      isDirtyWithModifiers(elm, checkVal)\n    ))\n  }\n\n  function isNotInFocusAndDirty (elm, checkVal) {\n    // return true when textbox (.number and .trim) loses focus and its value is\n    // not equal to the updated value\n    var notInFocus = true;\n    // #6157\n    // work around IE bug when accessing document.activeElement in an iframe\n    try { notInFocus = document.activeElement !== elm; } catch (e) {}\n    return notInFocus && elm.value !== checkVal\n  }\n\n  function isDirtyWithModifiers (elm, newVal) {\n    var value = elm.value;\n    var modifiers = elm._vModifiers; // injected by v-model runtime\n    if (isDef(modifiers)) {\n      if (modifiers.number) {\n        return toNumber(value) !== toNumber(newVal)\n      }\n      if (modifiers.trim) {\n        return value.trim() !== newVal.trim()\n      }\n    }\n    return value !== newVal\n  }\n\n  var domProps = {\n    create: updateDOMProps,\n    update: updateDOMProps\n  };\n\n  /*  */\n\n  var parseStyleText = cached(function (cssText) {\n    var res = {};\n    var listDelimiter = /;(?![^(]*\\))/g;\n    var propertyDelimiter = /:(.+)/;\n    cssText.split(listDelimiter).forEach(function (item) {\n      if (item) {\n        var tmp = item.split(propertyDelimiter);\n        tmp.length > 1 && (res[tmp[0].trim()] = tmp[1].trim());\n      }\n    });\n    return res\n  });\n\n  // merge static and dynamic style data on the same vnode\n  function normalizeStyleData (data) {\n    var style = normalizeStyleBinding(data.style);\n    // static style is pre-processed into an object during compilation\n    // and is always a fresh object, so it's safe to merge into it\n    return data.staticStyle\n      ? extend(data.staticStyle, style)\n      : style\n  }\n\n  // normalize possible array / string values into Object\n  function normalizeStyleBinding (bindingStyle) {\n    if (Array.isArray(bindingStyle)) {\n      return toObject(bindingStyle)\n    }\n    if (typeof bindingStyle === 'string') {\n      return parseStyleText(bindingStyle)\n    }\n    return bindingStyle\n  }\n\n  /**\n   * parent component style should be after child's\n   * so that parent component's style could override it\n   */\n  function getStyle (vnode, checkChild) {\n    var res = {};\n    var styleData;\n\n    if (checkChild) {\n      var childNode = vnode;\n      while (childNode.componentInstance) {\n        childNode = childNode.componentInstance._vnode;\n        if (\n          childNode && childNode.data &&\n          (styleData = normalizeStyleData(childNode.data))\n        ) {\n          extend(res, styleData);\n        }\n      }\n    }\n\n    if ((styleData = normalizeStyleData(vnode.data))) {\n      extend(res, styleData);\n    }\n\n    var parentNode = vnode;\n    while ((parentNode = parentNode.parent)) {\n      if (parentNode.data && (styleData = normalizeStyleData(parentNode.data))) {\n        extend(res, styleData);\n      }\n    }\n    return res\n  }\n\n  /*  */\n\n  var cssVarRE = /^--/;\n  var importantRE = /\\s*!important$/;\n  var setProp = function (el, name, val) {\n    /* istanbul ignore if */\n    if (cssVarRE.test(name)) {\n      el.style.setProperty(name, val);\n    } else if (importantRE.test(val)) {\n      el.style.setProperty(hyphenate(name), val.replace(importantRE, ''), 'important');\n    } else {\n      var normalizedName = normalize(name);\n      if (Array.isArray(val)) {\n        // Support values array created by autoprefixer, e.g.\n        // {display: [\"-webkit-box\", \"-ms-flexbox\", \"flex\"]}\n        // Set them one by one, and the browser will only set those it can recognize\n        for (var i = 0, len = val.length; i < len; i++) {\n          el.style[normalizedName] = val[i];\n        }\n      } else {\n        el.style[normalizedName] = val;\n      }\n    }\n  };\n\n  var vendorNames = ['Webkit', 'Moz', 'ms'];\n\n  var emptyStyle;\n  var normalize = cached(function (prop) {\n    emptyStyle = emptyStyle || document.createElement('div').style;\n    prop = camelize(prop);\n    if (prop !== 'filter' && (prop in emptyStyle)) {\n      return prop\n    }\n    var capName = prop.charAt(0).toUpperCase() + prop.slice(1);\n    for (var i = 0; i < vendorNames.length; i++) {\n      var name = vendorNames[i] + capName;\n      if (name in emptyStyle) {\n        return name\n      }\n    }\n  });\n\n  function updateStyle (oldVnode, vnode) {\n    var data = vnode.data;\n    var oldData = oldVnode.data;\n\n    if (isUndef(data.staticStyle) && isUndef(data.style) &&\n      isUndef(oldData.staticStyle) && isUndef(oldData.style)\n    ) {\n      return\n    }\n\n    var cur, name;\n    var el = vnode.elm;\n    var oldStaticStyle = oldData.staticStyle;\n    var oldStyleBinding = oldData.normalizedStyle || oldData.style || {};\n\n    // if static style exists, stylebinding already merged into it when doing normalizeStyleData\n    var oldStyle = oldStaticStyle || oldStyleBinding;\n\n    var style = normalizeStyleBinding(vnode.data.style) || {};\n\n    // store normalized style under a different key for next diff\n    // make sure to clone it if it's reactive, since the user likely wants\n    // to mutate it.\n    vnode.data.normalizedStyle = isDef(style.__ob__)\n      ? extend({}, style)\n      : style;\n\n    var newStyle = getStyle(vnode, true);\n\n    for (name in oldStyle) {\n      if (isUndef(newStyle[name])) {\n        setProp(el, name, '');\n      }\n    }\n    for (name in newStyle) {\n      cur = newStyle[name];\n      if (cur !== oldStyle[name]) {\n        // ie9 setting to null has no effect, must use empty string\n        setProp(el, name, cur == null ? '' : cur);\n      }\n    }\n  }\n\n  var style = {\n    create: updateStyle,\n    update: updateStyle\n  };\n\n  /*  */\n\n  var whitespaceRE = /\\s+/;\n\n  /**\n   * Add class with compatibility for SVG since classList is not supported on\n   * SVG elements in IE\n   */\n  function addClass (el, cls) {\n    /* istanbul ignore if */\n    if (!cls || !(cls = cls.trim())) {\n      return\n    }\n\n    /* istanbul ignore else */\n    if (el.classList) {\n      if (cls.indexOf(' ') > -1) {\n        cls.split(whitespaceRE).forEach(function (c) { return el.classList.add(c); });\n      } else {\n        el.classList.add(cls);\n      }\n    } else {\n      var cur = \" \" + (el.getAttribute('class') || '') + \" \";\n      if (cur.indexOf(' ' + cls + ' ') < 0) {\n        el.setAttribute('class', (cur + cls).trim());\n      }\n    }\n  }\n\n  /**\n   * Remove class with compatibility for SVG since classList is not supported on\n   * SVG elements in IE\n   */\n  function removeClass (el, cls) {\n    /* istanbul ignore if */\n    if (!cls || !(cls = cls.trim())) {\n      return\n    }\n\n    /* istanbul ignore else */\n    if (el.classList) {\n      if (cls.indexOf(' ') > -1) {\n        cls.split(whitespaceRE).forEach(function (c) { return el.classList.remove(c); });\n      } else {\n        el.classList.remove(cls);\n      }\n      if (!el.classList.length) {\n        el.removeAttribute('class');\n      }\n    } else {\n      var cur = \" \" + (el.getAttribute('class') || '') + \" \";\n      var tar = ' ' + cls + ' ';\n      while (cur.indexOf(tar) >= 0) {\n        cur = cur.replace(tar, ' ');\n      }\n      cur = cur.trim();\n      if (cur) {\n        el.setAttribute('class', cur);\n      } else {\n        el.removeAttribute('class');\n      }\n    }\n  }\n\n  /*  */\n\n  function resolveTransition (def$$1) {\n    if (!def$$1) {\n      return\n    }\n    /* istanbul ignore else */\n    if (typeof def$$1 === 'object') {\n      var res = {};\n      if (def$$1.css !== false) {\n        extend(res, autoCssTransition(def$$1.name || 'v'));\n      }\n      extend(res, def$$1);\n      return res\n    } else if (typeof def$$1 === 'string') {\n      return autoCssTransition(def$$1)\n    }\n  }\n\n  var autoCssTransition = cached(function (name) {\n    return {\n      enterClass: (name + \"-enter\"),\n      enterToClass: (name + \"-enter-to\"),\n      enterActiveClass: (name + \"-enter-active\"),\n      leaveClass: (name + \"-leave\"),\n      leaveToClass: (name + \"-leave-to\"),\n      leaveActiveClass: (name + \"-leave-active\")\n    }\n  });\n\n  var hasTransition = inBrowser && !isIE9;\n  var TRANSITION = 'transition';\n  var ANIMATION = 'animation';\n\n  // Transition property/event sniffing\n  var transitionProp = 'transition';\n  var transitionEndEvent = 'transitionend';\n  var animationProp = 'animation';\n  var animationEndEvent = 'animationend';\n  if (hasTransition) {\n    /* istanbul ignore if */\n    if (window.ontransitionend === undefined &&\n      window.onwebkittransitionend !== undefined\n    ) {\n      transitionProp = 'WebkitTransition';\n      transitionEndEvent = 'webkitTransitionEnd';\n    }\n    if (window.onanimationend === undefined &&\n      window.onwebkitanimationend !== undefined\n    ) {\n      animationProp = 'WebkitAnimation';\n      animationEndEvent = 'webkitAnimationEnd';\n    }\n  }\n\n  // binding to window is necessary to make hot reload work in IE in strict mode\n  var raf = inBrowser\n    ? window.requestAnimationFrame\n      ? window.requestAnimationFrame.bind(window)\n      : setTimeout\n    : /* istanbul ignore next */ function (fn) { return fn(); };\n\n  function nextFrame (fn) {\n    raf(function () {\n      raf(fn);\n    });\n  }\n\n  function addTransitionClass (el, cls) {\n    var transitionClasses = el._transitionClasses || (el._transitionClasses = []);\n    if (transitionClasses.indexOf(cls) < 0) {\n      transitionClasses.push(cls);\n      addClass(el, cls);\n    }\n  }\n\n  function removeTransitionClass (el, cls) {\n    if (el._transitionClasses) {\n      remove(el._transitionClasses, cls);\n    }\n    removeClass(el, cls);\n  }\n\n  function whenTransitionEnds (\n    el,\n    expectedType,\n    cb\n  ) {\n    var ref = getTransitionInfo(el, expectedType);\n    var type = ref.type;\n    var timeout = ref.timeout;\n    var propCount = ref.propCount;\n    if (!type) { return cb() }\n    var event = type === TRANSITION ? transitionEndEvent : animationEndEvent;\n    var ended = 0;\n    var end = function () {\n      el.removeEventListener(event, onEnd);\n      cb();\n    };\n    var onEnd = function (e) {\n      if (e.target === el) {\n        if (++ended >= propCount) {\n          end();\n        }\n      }\n    };\n    setTimeout(function () {\n      if (ended < propCount) {\n        end();\n      }\n    }, timeout + 1);\n    el.addEventListener(event, onEnd);\n  }\n\n  var transformRE = /\\b(transform|all)(,|$)/;\n\n  function getTransitionInfo (el, expectedType) {\n    var styles = window.getComputedStyle(el);\n    // JSDOM may return undefined for transition properties\n    var transitionDelays = (styles[transitionProp + 'Delay'] || '').split(', ');\n    var transitionDurations = (styles[transitionProp + 'Duration'] || '').split(', ');\n    var transitionTimeout = getTimeout(transitionDelays, transitionDurations);\n    var animationDelays = (styles[animationProp + 'Delay'] || '').split(', ');\n    var animationDurations = (styles[animationProp + 'Duration'] || '').split(', ');\n    var animationTimeout = getTimeout(animationDelays, animationDurations);\n\n    var type;\n    var timeout = 0;\n    var propCount = 0;\n    /* istanbul ignore if */\n    if (expectedType === TRANSITION) {\n      if (transitionTimeout > 0) {\n        type = TRANSITION;\n        timeout = transitionTimeout;\n        propCount = transitionDurations.length;\n      }\n    } else if (expectedType === ANIMATION) {\n      if (animationTimeout > 0) {\n        type = ANIMATION;\n        timeout = animationTimeout;\n        propCount = animationDurations.length;\n      }\n    } else {\n      timeout = Math.max(transitionTimeout, animationTimeout);\n      type = timeout > 0\n        ? transitionTimeout > animationTimeout\n          ? TRANSITION\n          : ANIMATION\n        : null;\n      propCount = type\n        ? type === TRANSITION\n          ? transitionDurations.length\n          : animationDurations.length\n        : 0;\n    }\n    var hasTransform =\n      type === TRANSITION &&\n      transformRE.test(styles[transitionProp + 'Property']);\n    return {\n      type: type,\n      timeout: timeout,\n      propCount: propCount,\n      hasTransform: hasTransform\n    }\n  }\n\n  function getTimeout (delays, durations) {\n    /* istanbul ignore next */\n    while (delays.length < durations.length) {\n      delays = delays.concat(delays);\n    }\n\n    return Math.max.apply(null, durations.map(function (d, i) {\n      return toMs(d) + toMs(delays[i])\n    }))\n  }\n\n  // Old versions of Chromium (below 61.0.3163.100) formats floating pointer numbers\n  // in a locale-dependent way, using a comma instead of a dot.\n  // If comma is not replaced with a dot, the input will be rounded down (i.e. acting\n  // as a floor function) causing unexpected behaviors\n  function toMs (s) {\n    return Number(s.slice(0, -1).replace(',', '.')) * 1000\n  }\n\n  /*  */\n\n  function enter (vnode, toggleDisplay) {\n    var el = vnode.elm;\n\n    // call leave callback now\n    if (isDef(el._leaveCb)) {\n      el._leaveCb.cancelled = true;\n      el._leaveCb();\n    }\n\n    var data = resolveTransition(vnode.data.transition);\n    if (isUndef(data)) {\n      return\n    }\n\n    /* istanbul ignore if */\n    if (isDef(el._enterCb) || el.nodeType !== 1) {\n      return\n    }\n\n    var css = data.css;\n    var type = data.type;\n    var enterClass = data.enterClass;\n    var enterToClass = data.enterToClass;\n    var enterActiveClass = data.enterActiveClass;\n    var appearClass = data.appearClass;\n    var appearToClass = data.appearToClass;\n    var appearActiveClass = data.appearActiveClass;\n    var beforeEnter = data.beforeEnter;\n    var enter = data.enter;\n    var afterEnter = data.afterEnter;\n    var enterCancelled = data.enterCancelled;\n    var beforeAppear = data.beforeAppear;\n    var appear = data.appear;\n    var afterAppear = data.afterAppear;\n    var appearCancelled = data.appearCancelled;\n    var duration = data.duration;\n\n    // activeInstance will always be the <transition> component managing this\n    // transition. One edge case to check is when the <transition> is placed\n    // as the root node of a child component. In that case we need to check\n    // <transition>'s parent for appear check.\n    var context = activeInstance;\n    var transitionNode = activeInstance.$vnode;\n    while (transitionNode && transitionNode.parent) {\n      context = transitionNode.context;\n      transitionNode = transitionNode.parent;\n    }\n\n    var isAppear = !context._isMounted || !vnode.isRootInsert;\n\n    if (isAppear && !appear && appear !== '') {\n      return\n    }\n\n    var startClass = isAppear && appearClass\n      ? appearClass\n      : enterClass;\n    var activeClass = isAppear && appearActiveClass\n      ? appearActiveClass\n      : enterActiveClass;\n    var toClass = isAppear && appearToClass\n      ? appearToClass\n      : enterToClass;\n\n    var beforeEnterHook = isAppear\n      ? (beforeAppear || beforeEnter)\n      : beforeEnter;\n    var enterHook = isAppear\n      ? (typeof appear === 'function' ? appear : enter)\n      : enter;\n    var afterEnterHook = isAppear\n      ? (afterAppear || afterEnter)\n      : afterEnter;\n    var enterCancelledHook = isAppear\n      ? (appearCancelled || enterCancelled)\n      : enterCancelled;\n\n    var explicitEnterDuration = toNumber(\n      isObject(duration)\n        ? duration.enter\n        : duration\n    );\n\n    if (explicitEnterDuration != null) {\n      checkDuration(explicitEnterDuration, 'enter', vnode);\n    }\n\n    var expectsCSS = css !== false && !isIE9;\n    var userWantsControl = getHookArgumentsLength(enterHook);\n\n    var cb = el._enterCb = once(function () {\n      if (expectsCSS) {\n        removeTransitionClass(el, toClass);\n        removeTransitionClass(el, activeClass);\n      }\n      if (cb.cancelled) {\n        if (expectsCSS) {\n          removeTransitionClass(el, startClass);\n        }\n        enterCancelledHook && enterCancelledHook(el);\n      } else {\n        afterEnterHook && afterEnterHook(el);\n      }\n      el._enterCb = null;\n    });\n\n    if (!vnode.data.show) {\n      // remove pending leave element on enter by injecting an insert hook\n      mergeVNodeHook(vnode, 'insert', function () {\n        var parent = el.parentNode;\n        var pendingNode = parent && parent._pending && parent._pending[vnode.key];\n        if (pendingNode &&\n          pendingNode.tag === vnode.tag &&\n          pendingNode.elm._leaveCb\n        ) {\n          pendingNode.elm._leaveCb();\n        }\n        enterHook && enterHook(el, cb);\n      });\n    }\n\n    // start enter transition\n    beforeEnterHook && beforeEnterHook(el);\n    if (expectsCSS) {\n      addTransitionClass(el, startClass);\n      addTransitionClass(el, activeClass);\n      nextFrame(function () {\n        removeTransitionClass(el, startClass);\n        if (!cb.cancelled) {\n          addTransitionClass(el, toClass);\n          if (!userWantsControl) {\n            if (isValidDuration(explicitEnterDuration)) {\n              setTimeout(cb, explicitEnterDuration);\n            } else {\n              whenTransitionEnds(el, type, cb);\n            }\n          }\n        }\n      });\n    }\n\n    if (vnode.data.show) {\n      toggleDisplay && toggleDisplay();\n      enterHook && enterHook(el, cb);\n    }\n\n    if (!expectsCSS && !userWantsControl) {\n      cb();\n    }\n  }\n\n  function leave (vnode, rm) {\n    var el = vnode.elm;\n\n    // call enter callback now\n    if (isDef(el._enterCb)) {\n      el._enterCb.cancelled = true;\n      el._enterCb();\n    }\n\n    var data = resolveTransition(vnode.data.transition);\n    if (isUndef(data) || el.nodeType !== 1) {\n      return rm()\n    }\n\n    /* istanbul ignore if */\n    if (isDef(el._leaveCb)) {\n      return\n    }\n\n    var css = data.css;\n    var type = data.type;\n    var leaveClass = data.leaveClass;\n    var leaveToClass = data.leaveToClass;\n    var leaveActiveClass = data.leaveActiveClass;\n    var beforeLeave = data.beforeLeave;\n    var leave = data.leave;\n    var afterLeave = data.afterLeave;\n    var leaveCancelled = data.leaveCancelled;\n    var delayLeave = data.delayLeave;\n    var duration = data.duration;\n\n    var expectsCSS = css !== false && !isIE9;\n    var userWantsControl = getHookArgumentsLength(leave);\n\n    var explicitLeaveDuration = toNumber(\n      isObject(duration)\n        ? duration.leave\n        : duration\n    );\n\n    if (isDef(explicitLeaveDuration)) {\n      checkDuration(explicitLeaveDuration, 'leave', vnode);\n    }\n\n    var cb = el._leaveCb = once(function () {\n      if (el.parentNode && el.parentNode._pending) {\n        el.parentNode._pending[vnode.key] = null;\n      }\n      if (expectsCSS) {\n        removeTransitionClass(el, leaveToClass);\n        removeTransitionClass(el, leaveActiveClass);\n      }\n      if (cb.cancelled) {\n        if (expectsCSS) {\n          removeTransitionClass(el, leaveClass);\n        }\n        leaveCancelled && leaveCancelled(el);\n      } else {\n        rm();\n        afterLeave && afterLeave(el);\n      }\n      el._leaveCb = null;\n    });\n\n    if (delayLeave) {\n      delayLeave(performLeave);\n    } else {\n      performLeave();\n    }\n\n    function performLeave () {\n      // the delayed leave may have already been cancelled\n      if (cb.cancelled) {\n        return\n      }\n      // record leaving element\n      if (!vnode.data.show && el.parentNode) {\n        (el.parentNode._pending || (el.parentNode._pending = {}))[(vnode.key)] = vnode;\n      }\n      beforeLeave && beforeLeave(el);\n      if (expectsCSS) {\n        addTransitionClass(el, leaveClass);\n        addTransitionClass(el, leaveActiveClass);\n        nextFrame(function () {\n          removeTransitionClass(el, leaveClass);\n          if (!cb.cancelled) {\n            addTransitionClass(el, leaveToClass);\n            if (!userWantsControl) {\n              if (isValidDuration(explicitLeaveDuration)) {\n                setTimeout(cb, explicitLeaveDuration);\n              } else {\n                whenTransitionEnds(el, type, cb);\n              }\n            }\n          }\n        });\n      }\n      leave && leave(el, cb);\n      if (!expectsCSS && !userWantsControl) {\n        cb();\n      }\n    }\n  }\n\n  // only used in dev mode\n  function checkDuration (val, name, vnode) {\n    if (typeof val !== 'number') {\n      warn(\n        \"<transition> explicit \" + name + \" duration is not a valid number - \" +\n        \"got \" + (JSON.stringify(val)) + \".\",\n        vnode.context\n      );\n    } else if (isNaN(val)) {\n      warn(\n        \"<transition> explicit \" + name + \" duration is NaN - \" +\n        'the duration expression might be incorrect.',\n        vnode.context\n      );\n    }\n  }\n\n  function isValidDuration (val) {\n    return typeof val === 'number' && !isNaN(val)\n  }\n\n  /**\n   * Normalize a transition hook's argument length. The hook may be:\n   * - a merged hook (invoker) with the original in .fns\n   * - a wrapped component method (check ._length)\n   * - a plain function (.length)\n   */\n  function getHookArgumentsLength (fn) {\n    if (isUndef(fn)) {\n      return false\n    }\n    var invokerFns = fn.fns;\n    if (isDef(invokerFns)) {\n      // invoker\n      return getHookArgumentsLength(\n        Array.isArray(invokerFns)\n          ? invokerFns[0]\n          : invokerFns\n      )\n    } else {\n      return (fn._length || fn.length) > 1\n    }\n  }\n\n  function _enter (_, vnode) {\n    if (vnode.data.show !== true) {\n      enter(vnode);\n    }\n  }\n\n  var transition = inBrowser ? {\n    create: _enter,\n    activate: _enter,\n    remove: function remove$$1 (vnode, rm) {\n      /* istanbul ignore else */\n      if (vnode.data.show !== true) {\n        leave(vnode, rm);\n      } else {\n        rm();\n      }\n    }\n  } : {};\n\n  var platformModules = [\n    attrs,\n    klass,\n    events,\n    domProps,\n    style,\n    transition\n  ];\n\n  /*  */\n\n  // the directive module should be applied last, after all\n  // built-in modules have been applied.\n  var modules = platformModules.concat(baseModules);\n\n  var patch = createPatchFunction({ nodeOps: nodeOps, modules: modules });\n\n  /**\n   * Not type checking this file because flow doesn't like attaching\n   * properties to Elements.\n   */\n\n  /* istanbul ignore if */\n  if (isIE9) {\n    // http://www.matts411.com/post/internet-explorer-9-oninput/\n    document.addEventListener('selectionchange', function () {\n      var el = document.activeElement;\n      if (el && el.vmodel) {\n        trigger(el, 'input');\n      }\n    });\n  }\n\n  var directive = {\n    inserted: function inserted (el, binding, vnode, oldVnode) {\n      if (vnode.tag === 'select') {\n        // #6903\n        if (oldVnode.elm && !oldVnode.elm._vOptions) {\n          mergeVNodeHook(vnode, 'postpatch', function () {\n            directive.componentUpdated(el, binding, vnode);\n          });\n        } else {\n          setSelected(el, binding, vnode.context);\n        }\n        el._vOptions = [].map.call(el.options, getValue);\n      } else if (vnode.tag === 'textarea' || isTextInputType(el.type)) {\n        el._vModifiers = binding.modifiers;\n        if (!binding.modifiers.lazy) {\n          el.addEventListener('compositionstart', onCompositionStart);\n          el.addEventListener('compositionend', onCompositionEnd);\n          // Safari < 10.2 & UIWebView doesn't fire compositionend when\n          // switching focus before confirming composition choice\n          // this also fixes the issue where some browsers e.g. iOS Chrome\n          // fires \"change\" instead of \"input\" on autocomplete.\n          el.addEventListener('change', onCompositionEnd);\n          /* istanbul ignore if */\n          if (isIE9) {\n            el.vmodel = true;\n          }\n        }\n      }\n    },\n\n    componentUpdated: function componentUpdated (el, binding, vnode) {\n      if (vnode.tag === 'select') {\n        setSelected(el, binding, vnode.context);\n        // in case the options rendered by v-for have changed,\n        // it's possible that the value is out-of-sync with the rendered options.\n        // detect such cases and filter out values that no longer has a matching\n        // option in the DOM.\n        var prevOptions = el._vOptions;\n        var curOptions = el._vOptions = [].map.call(el.options, getValue);\n        if (curOptions.some(function (o, i) { return !looseEqual(o, prevOptions[i]); })) {\n          // trigger change event if\n          // no matching option found for at least one value\n          var needReset = el.multiple\n            ? binding.value.some(function (v) { return hasNoMatchingOption(v, curOptions); })\n            : binding.value !== binding.oldValue && hasNoMatchingOption(binding.value, curOptions);\n          if (needReset) {\n            trigger(el, 'change');\n          }\n        }\n      }\n    }\n  };\n\n  function setSelected (el, binding, vm) {\n    actuallySetSelected(el, binding, vm);\n    /* istanbul ignore if */\n    if (isIE || isEdge) {\n      setTimeout(function () {\n        actuallySetSelected(el, binding, vm);\n      }, 0);\n    }\n  }\n\n  function actuallySetSelected (el, binding, vm) {\n    var value = binding.value;\n    var isMultiple = el.multiple;\n    if (isMultiple && !Array.isArray(value)) {\n      warn(\n        \"<select multiple v-model=\\\"\" + (binding.expression) + \"\\\"> \" +\n        \"expects an Array value for its binding, but got \" + (Object.prototype.toString.call(value).slice(8, -1)),\n        vm\n      );\n      return\n    }\n    var selected, option;\n    for (var i = 0, l = el.options.length; i < l; i++) {\n      option = el.options[i];\n      if (isMultiple) {\n        selected = looseIndexOf(value, getValue(option)) > -1;\n        if (option.selected !== selected) {\n          option.selected = selected;\n        }\n      } else {\n        if (looseEqual(getValue(option), value)) {\n          if (el.selectedIndex !== i) {\n            el.selectedIndex = i;\n          }\n          return\n        }\n      }\n    }\n    if (!isMultiple) {\n      el.selectedIndex = -1;\n    }\n  }\n\n  function hasNoMatchingOption (value, options) {\n    return options.every(function (o) { return !looseEqual(o, value); })\n  }\n\n  function getValue (option) {\n    return '_value' in option\n      ? option._value\n      : option.value\n  }\n\n  function onCompositionStart (e) {\n    e.target.composing = true;\n  }\n\n  function onCompositionEnd (e) {\n    // prevent triggering an input event for no reason\n    if (!e.target.composing) { return }\n    e.target.composing = false;\n    trigger(e.target, 'input');\n  }\n\n  function trigger (el, type) {\n    var e = document.createEvent('HTMLEvents');\n    e.initEvent(type, true, true);\n    el.dispatchEvent(e);\n  }\n\n  /*  */\n\n  // recursively search for possible transition defined inside the component root\n  function locateNode (vnode) {\n    return vnode.componentInstance && (!vnode.data || !vnode.data.transition)\n      ? locateNode(vnode.componentInstance._vnode)\n      : vnode\n  }\n\n  var show = {\n    bind: function bind (el, ref, vnode) {\n      var value = ref.value;\n\n      vnode = locateNode(vnode);\n      var transition$$1 = vnode.data && vnode.data.transition;\n      var originalDisplay = el.__vOriginalDisplay =\n        el.style.display === 'none' ? '' : el.style.display;\n      if (value && transition$$1) {\n        vnode.data.show = true;\n        enter(vnode, function () {\n          el.style.display = originalDisplay;\n        });\n      } else {\n        el.style.display = value ? originalDisplay : 'none';\n      }\n    },\n\n    update: function update (el, ref, vnode) {\n      var value = ref.value;\n      var oldValue = ref.oldValue;\n\n      /* istanbul ignore if */\n      if (!value === !oldValue) { return }\n      vnode = locateNode(vnode);\n      var transition$$1 = vnode.data && vnode.data.transition;\n      if (transition$$1) {\n        vnode.data.show = true;\n        if (value) {\n          enter(vnode, function () {\n            el.style.display = el.__vOriginalDisplay;\n          });\n        } else {\n          leave(vnode, function () {\n            el.style.display = 'none';\n          });\n        }\n      } else {\n        el.style.display = value ? el.__vOriginalDisplay : 'none';\n      }\n    },\n\n    unbind: function unbind (\n      el,\n      binding,\n      vnode,\n      oldVnode,\n      isDestroy\n    ) {\n      if (!isDestroy) {\n        el.style.display = el.__vOriginalDisplay;\n      }\n    }\n  };\n\n  var platformDirectives = {\n    model: directive,\n    show: show\n  };\n\n  /*  */\n\n  var transitionProps = {\n    name: String,\n    appear: Boolean,\n    css: Boolean,\n    mode: String,\n    type: String,\n    enterClass: String,\n    leaveClass: String,\n    enterToClass: String,\n    leaveToClass: String,\n    enterActiveClass: String,\n    leaveActiveClass: String,\n    appearClass: String,\n    appearActiveClass: String,\n    appearToClass: String,\n    duration: [Number, String, Object]\n  };\n\n  // in case the child is also an abstract component, e.g. <keep-alive>\n  // we want to recursively retrieve the real component to be rendered\n  function getRealChild (vnode) {\n    var compOptions = vnode && vnode.componentOptions;\n    if (compOptions && compOptions.Ctor.options.abstract) {\n      return getRealChild(getFirstComponentChild(compOptions.children))\n    } else {\n      return vnode\n    }\n  }\n\n  function extractTransitionData (comp) {\n    var data = {};\n    var options = comp.$options;\n    // props\n    for (var key in options.propsData) {\n      data[key] = comp[key];\n    }\n    // events.\n    // extract listeners and pass them directly to the transition methods\n    var listeners = options._parentListeners;\n    for (var key$1 in listeners) {\n      data[camelize(key$1)] = listeners[key$1];\n    }\n    return data\n  }\n\n  function placeholder (h, rawChild) {\n    if (/\\d-keep-alive$/.test(rawChild.tag)) {\n      return h('keep-alive', {\n        props: rawChild.componentOptions.propsData\n      })\n    }\n  }\n\n  function hasParentTransition (vnode) {\n    while ((vnode = vnode.parent)) {\n      if (vnode.data.transition) {\n        return true\n      }\n    }\n  }\n\n  function isSameChild (child, oldChild) {\n    return oldChild.key === child.key && oldChild.tag === child.tag\n  }\n\n  var isNotTextNode = function (c) { return c.tag || isAsyncPlaceholder(c); };\n\n  var isVShowDirective = function (d) { return d.name === 'show'; };\n\n  var Transition = {\n    name: 'transition',\n    props: transitionProps,\n    abstract: true,\n\n    render: function render (h) {\n      var this$1 = this;\n\n      var children = this.$slots.default;\n      if (!children) {\n        return\n      }\n\n      // filter out text nodes (possible whitespaces)\n      children = children.filter(isNotTextNode);\n      /* istanbul ignore if */\n      if (!children.length) {\n        return\n      }\n\n      // warn multiple elements\n      if (children.length > 1) {\n        warn(\n          '<transition> can only be used on a single element. Use ' +\n          '<transition-group> for lists.',\n          this.$parent\n        );\n      }\n\n      var mode = this.mode;\n\n      // warn invalid mode\n      if (mode && mode !== 'in-out' && mode !== 'out-in'\n      ) {\n        warn(\n          'invalid <transition> mode: ' + mode,\n          this.$parent\n        );\n      }\n\n      var rawChild = children[0];\n\n      // if this is a component root node and the component's\n      // parent container node also has transition, skip.\n      if (hasParentTransition(this.$vnode)) {\n        return rawChild\n      }\n\n      // apply transition data to child\n      // use getRealChild() to ignore abstract components e.g. keep-alive\n      var child = getRealChild(rawChild);\n      /* istanbul ignore if */\n      if (!child) {\n        return rawChild\n      }\n\n      if (this._leaving) {\n        return placeholder(h, rawChild)\n      }\n\n      // ensure a key that is unique to the vnode type and to this transition\n      // component instance. This key will be used to remove pending leaving nodes\n      // during entering.\n      var id = \"__transition-\" + (this._uid) + \"-\";\n      child.key = child.key == null\n        ? child.isComment\n          ? id + 'comment'\n          : id + child.tag\n        : isPrimitive(child.key)\n          ? (String(child.key).indexOf(id) === 0 ? child.key : id + child.key)\n          : child.key;\n\n      var data = (child.data || (child.data = {})).transition = extractTransitionData(this);\n      var oldRawChild = this._vnode;\n      var oldChild = getRealChild(oldRawChild);\n\n      // mark v-show\n      // so that the transition module can hand over the control to the directive\n      if (child.data.directives && child.data.directives.some(isVShowDirective)) {\n        child.data.show = true;\n      }\n\n      if (\n        oldChild &&\n        oldChild.data &&\n        !isSameChild(child, oldChild) &&\n        !isAsyncPlaceholder(oldChild) &&\n        // #6687 component root is a comment node\n        !(oldChild.componentInstance && oldChild.componentInstance._vnode.isComment)\n      ) {\n        // replace old child transition data with fresh one\n        // important for dynamic transitions!\n        var oldData = oldChild.data.transition = extend({}, data);\n        // handle transition mode\n        if (mode === 'out-in') {\n          // return placeholder node and queue update when leave finishes\n          this._leaving = true;\n          mergeVNodeHook(oldData, 'afterLeave', function () {\n            this$1._leaving = false;\n            this$1.$forceUpdate();\n          });\n          return placeholder(h, rawChild)\n        } else if (mode === 'in-out') {\n          if (isAsyncPlaceholder(child)) {\n            return oldRawChild\n          }\n          var delayedLeave;\n          var performLeave = function () { delayedLeave(); };\n          mergeVNodeHook(data, 'afterEnter', performLeave);\n          mergeVNodeHook(data, 'enterCancelled', performLeave);\n          mergeVNodeHook(oldData, 'delayLeave', function (leave) { delayedLeave = leave; });\n        }\n      }\n\n      return rawChild\n    }\n  };\n\n  /*  */\n\n  var props = extend({\n    tag: String,\n    moveClass: String\n  }, transitionProps);\n\n  delete props.mode;\n\n  var TransitionGroup = {\n    props: props,\n\n    beforeMount: function beforeMount () {\n      var this$1 = this;\n\n      var update = this._update;\n      this._update = function (vnode, hydrating) {\n        var restoreActiveInstance = setActiveInstance(this$1);\n        // force removing pass\n        this$1.__patch__(\n          this$1._vnode,\n          this$1.kept,\n          false, // hydrating\n          true // removeOnly (!important, avoids unnecessary moves)\n        );\n        this$1._vnode = this$1.kept;\n        restoreActiveInstance();\n        update.call(this$1, vnode, hydrating);\n      };\n    },\n\n    render: function render (h) {\n      var tag = this.tag || this.$vnode.data.tag || 'span';\n      var map = Object.create(null);\n      var prevChildren = this.prevChildren = this.children;\n      var rawChildren = this.$slots.default || [];\n      var children = this.children = [];\n      var transitionData = extractTransitionData(this);\n\n      for (var i = 0; i < rawChildren.length; i++) {\n        var c = rawChildren[i];\n        if (c.tag) {\n          if (c.key != null && String(c.key).indexOf('__vlist') !== 0) {\n            children.push(c);\n            map[c.key] = c\n            ;(c.data || (c.data = {})).transition = transitionData;\n          } else {\n            var opts = c.componentOptions;\n            var name = opts ? (opts.Ctor.options.name || opts.tag || '') : c.tag;\n            warn((\"<transition-group> children must be keyed: <\" + name + \">\"));\n          }\n        }\n      }\n\n      if (prevChildren) {\n        var kept = [];\n        var removed = [];\n        for (var i$1 = 0; i$1 < prevChildren.length; i$1++) {\n          var c$1 = prevChildren[i$1];\n          c$1.data.transition = transitionData;\n          c$1.data.pos = c$1.elm.getBoundingClientRect();\n          if (map[c$1.key]) {\n            kept.push(c$1);\n          } else {\n            removed.push(c$1);\n          }\n        }\n        this.kept = h(tag, null, kept);\n        this.removed = removed;\n      }\n\n      return h(tag, null, children)\n    },\n\n    updated: function updated () {\n      var children = this.prevChildren;\n      var moveClass = this.moveClass || ((this.name || 'v') + '-move');\n      if (!children.length || !this.hasMove(children[0].elm, moveClass)) {\n        return\n      }\n\n      // we divide the work into three loops to avoid mixing DOM reads and writes\n      // in each iteration - which helps prevent layout thrashing.\n      children.forEach(callPendingCbs);\n      children.forEach(recordPosition);\n      children.forEach(applyTranslation);\n\n      // force reflow to put everything in position\n      // assign to this to avoid being removed in tree-shaking\n      // $flow-disable-line\n      this._reflow = document.body.offsetHeight;\n\n      children.forEach(function (c) {\n        if (c.data.moved) {\n          var el = c.elm;\n          var s = el.style;\n          addTransitionClass(el, moveClass);\n          s.transform = s.WebkitTransform = s.transitionDuration = '';\n          el.addEventListener(transitionEndEvent, el._moveCb = function cb (e) {\n            if (e && e.target !== el) {\n              return\n            }\n            if (!e || /transform$/.test(e.propertyName)) {\n              el.removeEventListener(transitionEndEvent, cb);\n              el._moveCb = null;\n              removeTransitionClass(el, moveClass);\n            }\n          });\n        }\n      });\n    },\n\n    methods: {\n      hasMove: function hasMove (el, moveClass) {\n        /* istanbul ignore if */\n        if (!hasTransition) {\n          return false\n        }\n        /* istanbul ignore if */\n        if (this._hasMove) {\n          return this._hasMove\n        }\n        // Detect whether an element with the move class applied has\n        // CSS transitions. Since the element may be inside an entering\n        // transition at this very moment, we make a clone of it and remove\n        // all other transition classes applied to ensure only the move class\n        // is applied.\n        var clone = el.cloneNode();\n        if (el._transitionClasses) {\n          el._transitionClasses.forEach(function (cls) { removeClass(clone, cls); });\n        }\n        addClass(clone, moveClass);\n        clone.style.display = 'none';\n        this.$el.appendChild(clone);\n        var info = getTransitionInfo(clone);\n        this.$el.removeChild(clone);\n        return (this._hasMove = info.hasTransform)\n      }\n    }\n  };\n\n  function callPendingCbs (c) {\n    /* istanbul ignore if */\n    if (c.elm._moveCb) {\n      c.elm._moveCb();\n    }\n    /* istanbul ignore if */\n    if (c.elm._enterCb) {\n      c.elm._enterCb();\n    }\n  }\n\n  function recordPosition (c) {\n    c.data.newPos = c.elm.getBoundingClientRect();\n  }\n\n  function applyTranslation (c) {\n    var oldPos = c.data.pos;\n    var newPos = c.data.newPos;\n    var dx = oldPos.left - newPos.left;\n    var dy = oldPos.top - newPos.top;\n    if (dx || dy) {\n      c.data.moved = true;\n      var s = c.elm.style;\n      s.transform = s.WebkitTransform = \"translate(\" + dx + \"px,\" + dy + \"px)\";\n      s.transitionDuration = '0s';\n    }\n  }\n\n  var platformComponents = {\n    Transition: Transition,\n    TransitionGroup: TransitionGroup\n  };\n\n  /*  */\n\n  // install platform specific utils\n  Vue.config.mustUseProp = mustUseProp;\n  Vue.config.isReservedTag = isReservedTag;\n  Vue.config.isReservedAttr = isReservedAttr;\n  Vue.config.getTagNamespace = getTagNamespace;\n  Vue.config.isUnknownElement = isUnknownElement;\n\n  // install platform runtime directives & components\n  extend(Vue.options.directives, platformDirectives);\n  extend(Vue.options.components, platformComponents);\n\n  // install platform patch function\n  Vue.prototype.__patch__ = inBrowser ? patch : noop;\n\n  // public mount method\n  Vue.prototype.$mount = function (\n    el,\n    hydrating\n  ) {\n    el = el && inBrowser ? query(el) : undefined;\n    return mountComponent(this, el, hydrating)\n  };\n\n  // devtools global hook\n  /* istanbul ignore next */\n  if (inBrowser) {\n    setTimeout(function () {\n      if (config.devtools) {\n        if (devtools) {\n          devtools.emit('init', Vue);\n        } else {\n          console[console.info ? 'info' : 'log'](\n            'Download the Vue Devtools extension for a better development experience:\\n' +\n            'https://github.com/vuejs/vue-devtools'\n          );\n        }\n      }\n      if (config.productionTip !== false &&\n        typeof console !== 'undefined'\n      ) {\n        console[console.info ? 'info' : 'log'](\n          \"You are running Vue in development mode.\\n\" +\n          \"Make sure to turn on production mode when deploying for production.\\n\" +\n          \"See more tips at https://vuejs.org/guide/deployment.html\"\n        );\n      }\n    }, 0);\n  }\n\n  /*  */\n\n  var defaultTagRE = /\\{\\{((?:.|\\r?\\n)+?)\\}\\}/g;\n  var regexEscapeRE = /[-.*+?^${}()|[\\]\\/\\\\]/g;\n\n  var buildRegex = cached(function (delimiters) {\n    var open = delimiters[0].replace(regexEscapeRE, '\\\\$&');\n    var close = delimiters[1].replace(regexEscapeRE, '\\\\$&');\n    return new RegExp(open + '((?:.|\\\\n)+?)' + close, 'g')\n  });\n\n\n\n  function parseText (\n    text,\n    delimiters\n  ) {\n    var tagRE = delimiters ? buildRegex(delimiters) : defaultTagRE;\n    if (!tagRE.test(text)) {\n      return\n    }\n    var tokens = [];\n    var rawTokens = [];\n    var lastIndex = tagRE.lastIndex = 0;\n    var match, index, tokenValue;\n    while ((match = tagRE.exec(text))) {\n      index = match.index;\n      // push text token\n      if (index > lastIndex) {\n        rawTokens.push(tokenValue = text.slice(lastIndex, index));\n        tokens.push(JSON.stringify(tokenValue));\n      }\n      // tag token\n      var exp = parseFilters(match[1].trim());\n      tokens.push((\"_s(\" + exp + \")\"));\n      rawTokens.push({ '@binding': exp });\n      lastIndex = index + match[0].length;\n    }\n    if (lastIndex < text.length) {\n      rawTokens.push(tokenValue = text.slice(lastIndex));\n      tokens.push(JSON.stringify(tokenValue));\n    }\n    return {\n      expression: tokens.join('+'),\n      tokens: rawTokens\n    }\n  }\n\n  /*  */\n\n  function transformNode (el, options) {\n    var warn = options.warn || baseWarn;\n    var staticClass = getAndRemoveAttr(el, 'class');\n    if (staticClass) {\n      var res = parseText(staticClass, options.delimiters);\n      if (res) {\n        warn(\n          \"class=\\\"\" + staticClass + \"\\\": \" +\n          'Interpolation inside attributes has been removed. ' +\n          'Use v-bind or the colon shorthand instead. For example, ' +\n          'instead of <div class=\"{{ val }}\">, use <div :class=\"val\">.',\n          el.rawAttrsMap['class']\n        );\n      }\n    }\n    if (staticClass) {\n      el.staticClass = JSON.stringify(staticClass);\n    }\n    var classBinding = getBindingAttr(el, 'class', false /* getStatic */);\n    if (classBinding) {\n      el.classBinding = classBinding;\n    }\n  }\n\n  function genData (el) {\n    var data = '';\n    if (el.staticClass) {\n      data += \"staticClass:\" + (el.staticClass) + \",\";\n    }\n    if (el.classBinding) {\n      data += \"class:\" + (el.classBinding) + \",\";\n    }\n    return data\n  }\n\n  var klass$1 = {\n    staticKeys: ['staticClass'],\n    transformNode: transformNode,\n    genData: genData\n  };\n\n  /*  */\n\n  function transformNode$1 (el, options) {\n    var warn = options.warn || baseWarn;\n    var staticStyle = getAndRemoveAttr(el, 'style');\n    if (staticStyle) {\n      /* istanbul ignore if */\n      {\n        var res = parseText(staticStyle, options.delimiters);\n        if (res) {\n          warn(\n            \"style=\\\"\" + staticStyle + \"\\\": \" +\n            'Interpolation inside attributes has been removed. ' +\n            'Use v-bind or the colon shorthand instead. For example, ' +\n            'instead of <div style=\"{{ val }}\">, use <div :style=\"val\">.',\n            el.rawAttrsMap['style']\n          );\n        }\n      }\n      el.staticStyle = JSON.stringify(parseStyleText(staticStyle));\n    }\n\n    var styleBinding = getBindingAttr(el, 'style', false /* getStatic */);\n    if (styleBinding) {\n      el.styleBinding = styleBinding;\n    }\n  }\n\n  function genData$1 (el) {\n    var data = '';\n    if (el.staticStyle) {\n      data += \"staticStyle:\" + (el.staticStyle) + \",\";\n    }\n    if (el.styleBinding) {\n      data += \"style:(\" + (el.styleBinding) + \"),\";\n    }\n    return data\n  }\n\n  var style$1 = {\n    staticKeys: ['staticStyle'],\n    transformNode: transformNode$1,\n    genData: genData$1\n  };\n\n  /*  */\n\n  var decoder;\n\n  var he = {\n    decode: function decode (html) {\n      decoder = decoder || document.createElement('div');\n      decoder.innerHTML = html;\n      return decoder.textContent\n    }\n  };\n\n  /*  */\n\n  var isUnaryTag = makeMap(\n    'area,base,br,col,embed,frame,hr,img,input,isindex,keygen,' +\n    'link,meta,param,source,track,wbr'\n  );\n\n  // Elements that you can, intentionally, leave open\n  // (and which close themselves)\n  var canBeLeftOpenTag = makeMap(\n    'colgroup,dd,dt,li,options,p,td,tfoot,th,thead,tr,source'\n  );\n\n  // HTML5 tags https://html.spec.whatwg.org/multipage/indices.html#elements-3\n  // Phrasing Content https://html.spec.whatwg.org/multipage/dom.html#phrasing-content\n  var isNonPhrasingTag = makeMap(\n    'address,article,aside,base,blockquote,body,caption,col,colgroup,dd,' +\n    'details,dialog,div,dl,dt,fieldset,figcaption,figure,footer,form,' +\n    'h1,h2,h3,h4,h5,h6,head,header,hgroup,hr,html,legend,li,menuitem,meta,' +\n    'optgroup,option,param,rp,rt,source,style,summary,tbody,td,tfoot,th,thead,' +\n    'title,tr,track'\n  );\n\n  /**\n   * Not type-checking this file because it's mostly vendor code.\n   */\n\n  // Regular Expressions for parsing tags and attributes\n  var attribute = /^\\s*([^\\s\"'<>\\/=]+)(?:\\s*(=)\\s*(?:\"([^\"]*)\"+|'([^']*)'+|([^\\s\"'=<>`]+)))?/;\n  var dynamicArgAttribute = /^\\s*((?:v-[\\w-]+:|@|:|#)\\[[^=]+\\][^\\s\"'<>\\/=]*)(?:\\s*(=)\\s*(?:\"([^\"]*)\"+|'([^']*)'+|([^\\s\"'=<>`]+)))?/;\n  var ncname = \"[a-zA-Z_][\\\\-\\\\.0-9_a-zA-Z\" + (unicodeRegExp.source) + \"]*\";\n  var qnameCapture = \"((?:\" + ncname + \"\\\\:)?\" + ncname + \")\";\n  var startTagOpen = new RegExp((\"^<\" + qnameCapture));\n  var startTagClose = /^\\s*(\\/?)>/;\n  var endTag = new RegExp((\"^<\\\\/\" + qnameCapture + \"[^>]*>\"));\n  var doctype = /^<!DOCTYPE [^>]+>/i;\n  // #7298: escape - to avoid being passed as HTML comment when inlined in page\n  var comment = /^<!\\--/;\n  var conditionalComment = /^<!\\[/;\n\n  // Special Elements (can contain anything)\n  var isPlainTextElement = makeMap('script,style,textarea', true);\n  var reCache = {};\n\n  var decodingMap = {\n    '&lt;': '<',\n    '&gt;': '>',\n    '&quot;': '\"',\n    '&amp;': '&',\n    '&#10;': '\\n',\n    '&#9;': '\\t',\n    '&#39;': \"'\"\n  };\n  var encodedAttr = /&(?:lt|gt|quot|amp|#39);/g;\n  var encodedAttrWithNewLines = /&(?:lt|gt|quot|amp|#39|#10|#9);/g;\n\n  // #5992\n  var isIgnoreNewlineTag = makeMap('pre,textarea', true);\n  var shouldIgnoreFirstNewline = function (tag, html) { return tag && isIgnoreNewlineTag(tag) && html[0] === '\\n'; };\n\n  function decodeAttr (value, shouldDecodeNewlines) {\n    var re = shouldDecodeNewlines ? encodedAttrWithNewLines : encodedAttr;\n    return value.replace(re, function (match) { return decodingMap[match]; })\n  }\n\n  function parseHTML (html, options) {\n    var stack = [];\n    var expectHTML = options.expectHTML;\n    var isUnaryTag$$1 = options.isUnaryTag || no;\n    var canBeLeftOpenTag$$1 = options.canBeLeftOpenTag || no;\n    var index = 0;\n    var last, lastTag;\n    while (html) {\n      last = html;\n      // Make sure we're not in a plaintext content element like script/style\n      if (!lastTag || !isPlainTextElement(lastTag)) {\n        var textEnd = html.indexOf('<');\n        if (textEnd === 0) {\n          // Comment:\n          if (comment.test(html)) {\n            var commentEnd = html.indexOf('-->');\n\n            if (commentEnd >= 0) {\n              if (options.shouldKeepComment) {\n                options.comment(html.substring(4, commentEnd), index, index + commentEnd + 3);\n              }\n              advance(commentEnd + 3);\n              continue\n            }\n          }\n\n          // http://en.wikipedia.org/wiki/Conditional_comment#Downlevel-revealed_conditional_comment\n          if (conditionalComment.test(html)) {\n            var conditionalEnd = html.indexOf(']>');\n\n            if (conditionalEnd >= 0) {\n              advance(conditionalEnd + 2);\n              continue\n            }\n          }\n\n          // Doctype:\n          var doctypeMatch = html.match(doctype);\n          if (doctypeMatch) {\n            advance(doctypeMatch[0].length);\n            continue\n          }\n\n          // End tag:\n          var endTagMatch = html.match(endTag);\n          if (endTagMatch) {\n            var curIndex = index;\n            advance(endTagMatch[0].length);\n            parseEndTag(endTagMatch[1], curIndex, index);\n            continue\n          }\n\n          // Start tag:\n          var startTagMatch = parseStartTag();\n          if (startTagMatch) {\n            handleStartTag(startTagMatch);\n            if (shouldIgnoreFirstNewline(startTagMatch.tagName, html)) {\n              advance(1);\n            }\n            continue\n          }\n        }\n\n        var text = (void 0), rest = (void 0), next = (void 0);\n        if (textEnd >= 0) {\n          rest = html.slice(textEnd);\n          while (\n            !endTag.test(rest) &&\n            !startTagOpen.test(rest) &&\n            !comment.test(rest) &&\n            !conditionalComment.test(rest)\n          ) {\n            // < in plain text, be forgiving and treat it as text\n            next = rest.indexOf('<', 1);\n            if (next < 0) { break }\n            textEnd += next;\n            rest = html.slice(textEnd);\n          }\n          text = html.substring(0, textEnd);\n        }\n\n        if (textEnd < 0) {\n          text = html;\n        }\n\n        if (text) {\n          advance(text.length);\n        }\n\n        if (options.chars && text) {\n          options.chars(text, index - text.length, index);\n        }\n      } else {\n        var endTagLength = 0;\n        var stackedTag = lastTag.toLowerCase();\n        var reStackedTag = reCache[stackedTag] || (reCache[stackedTag] = new RegExp('([\\\\s\\\\S]*?)(</' + stackedTag + '[^>]*>)', 'i'));\n        var rest$1 = html.replace(reStackedTag, function (all, text, endTag) {\n          endTagLength = endTag.length;\n          if (!isPlainTextElement(stackedTag) && stackedTag !== 'noscript') {\n            text = text\n              .replace(/<!\\--([\\s\\S]*?)-->/g, '$1') // #7298\n              .replace(/<!\\[CDATA\\[([\\s\\S]*?)]]>/g, '$1');\n          }\n          if (shouldIgnoreFirstNewline(stackedTag, text)) {\n            text = text.slice(1);\n          }\n          if (options.chars) {\n            options.chars(text);\n          }\n          return ''\n        });\n        index += html.length - rest$1.length;\n        html = rest$1;\n        parseEndTag(stackedTag, index - endTagLength, index);\n      }\n\n      if (html === last) {\n        options.chars && options.chars(html);\n        if (!stack.length && options.warn) {\n          options.warn((\"Mal-formatted tag at end of template: \\\"\" + html + \"\\\"\"), { start: index + html.length });\n        }\n        break\n      }\n    }\n\n    // Clean up any remaining tags\n    parseEndTag();\n\n    function advance (n) {\n      index += n;\n      html = html.substring(n);\n    }\n\n    function parseStartTag () {\n      var start = html.match(startTagOpen);\n      if (start) {\n        var match = {\n          tagName: start[1],\n          attrs: [],\n          start: index\n        };\n        advance(start[0].length);\n        var end, attr;\n        while (!(end = html.match(startTagClose)) && (attr = html.match(dynamicArgAttribute) || html.match(attribute))) {\n          attr.start = index;\n          advance(attr[0].length);\n          attr.end = index;\n          match.attrs.push(attr);\n        }\n        if (end) {\n          match.unarySlash = end[1];\n          advance(end[0].length);\n          match.end = index;\n          return match\n        }\n      }\n    }\n\n    function handleStartTag (match) {\n      var tagName = match.tagName;\n      var unarySlash = match.unarySlash;\n\n      if (expectHTML) {\n        if (lastTag === 'p' && isNonPhrasingTag(tagName)) {\n          parseEndTag(lastTag);\n        }\n        if (canBeLeftOpenTag$$1(tagName) && lastTag === tagName) {\n          parseEndTag(tagName);\n        }\n      }\n\n      var unary = isUnaryTag$$1(tagName) || !!unarySlash;\n\n      var l = match.attrs.length;\n      var attrs = new Array(l);\n      for (var i = 0; i < l; i++) {\n        var args = match.attrs[i];\n        var value = args[3] || args[4] || args[5] || '';\n        var shouldDecodeNewlines = tagName === 'a' && args[1] === 'href'\n          ? options.shouldDecodeNewlinesForHref\n          : options.shouldDecodeNewlines;\n        attrs[i] = {\n          name: args[1],\n          value: decodeAttr(value, shouldDecodeNewlines)\n        };\n        if (options.outputSourceRange) {\n          attrs[i].start = args.start + args[0].match(/^\\s*/).length;\n          attrs[i].end = args.end;\n        }\n      }\n\n      if (!unary) {\n        stack.push({ tag: tagName, lowerCasedTag: tagName.toLowerCase(), attrs: attrs, start: match.start, end: match.end });\n        lastTag = tagName;\n      }\n\n      if (options.start) {\n        options.start(tagName, attrs, unary, match.start, match.end);\n      }\n    }\n\n    function parseEndTag (tagName, start, end) {\n      var pos, lowerCasedTagName;\n      if (start == null) { start = index; }\n      if (end == null) { end = index; }\n\n      // Find the closest opened tag of the same type\n      if (tagName) {\n        lowerCasedTagName = tagName.toLowerCase();\n        for (pos = stack.length - 1; pos >= 0; pos--) {\n          if (stack[pos].lowerCasedTag === lowerCasedTagName) {\n            break\n          }\n        }\n      } else {\n        // If no tag name is provided, clean shop\n        pos = 0;\n      }\n\n      if (pos >= 0) {\n        // Close all the open elements, up the stack\n        for (var i = stack.length - 1; i >= pos; i--) {\n          if (i > pos || !tagName &&\n            options.warn\n          ) {\n            options.warn(\n              (\"tag <\" + (stack[i].tag) + \"> has no matching end tag.\"),\n              { start: stack[i].start, end: stack[i].end }\n            );\n          }\n          if (options.end) {\n            options.end(stack[i].tag, start, end);\n          }\n        }\n\n        // Remove the open elements from the stack\n        stack.length = pos;\n        lastTag = pos && stack[pos - 1].tag;\n      } else if (lowerCasedTagName === 'br') {\n        if (options.start) {\n          options.start(tagName, [], true, start, end);\n        }\n      } else if (lowerCasedTagName === 'p') {\n        if (options.start) {\n          options.start(tagName, [], false, start, end);\n        }\n        if (options.end) {\n          options.end(tagName, start, end);\n        }\n      }\n    }\n  }\n\n  /*  */\n\n  var onRE = /^@|^v-on:/;\n  var dirRE = /^v-|^@|^:|^#/;\n  var forAliasRE = /([\\s\\S]*?)\\s+(?:in|of)\\s+([\\s\\S]*)/;\n  var forIteratorRE = /,([^,\\}\\]]*)(?:,([^,\\}\\]]*))?$/;\n  var stripParensRE = /^\\(|\\)$/g;\n  var dynamicArgRE = /^\\[.*\\]$/;\n\n  var argRE = /:(.*)$/;\n  var bindRE = /^:|^\\.|^v-bind:/;\n  var modifierRE = /\\.[^.\\]]+(?=[^\\]]*$)/g;\n\n  var slotRE = /^v-slot(:|$)|^#/;\n\n  var lineBreakRE = /[\\r\\n]/;\n  var whitespaceRE$1 = /\\s+/g;\n\n  var invalidAttributeRE = /[\\s\"'<>\\/=]/;\n\n  var decodeHTMLCached = cached(he.decode);\n\n  var emptySlotScopeToken = \"_empty_\";\n\n  // configurable state\n  var warn$2;\n  var delimiters;\n  var transforms;\n  var preTransforms;\n  var postTransforms;\n  var platformIsPreTag;\n  var platformMustUseProp;\n  var platformGetTagNamespace;\n  var maybeComponent;\n\n  function createASTElement (\n    tag,\n    attrs,\n    parent\n  ) {\n    return {\n      type: 1,\n      tag: tag,\n      attrsList: attrs,\n      attrsMap: makeAttrsMap(attrs),\n      rawAttrsMap: {},\n      parent: parent,\n      children: []\n    }\n  }\n\n  /**\n   * Convert HTML string to AST.\n   */\n  function parse (\n    template,\n    options\n  ) {\n    warn$2 = options.warn || baseWarn;\n\n    platformIsPreTag = options.isPreTag || no;\n    platformMustUseProp = options.mustUseProp || no;\n    platformGetTagNamespace = options.getTagNamespace || no;\n    var isReservedTag = options.isReservedTag || no;\n    maybeComponent = function (el) { return !!el.component || !isReservedTag(el.tag); };\n\n    transforms = pluckModuleFunction(options.modules, 'transformNode');\n    preTransforms = pluckModuleFunction(options.modules, 'preTransformNode');\n    postTransforms = pluckModuleFunction(options.modules, 'postTransformNode');\n\n    delimiters = options.delimiters;\n\n    var stack = [];\n    var preserveWhitespace = options.preserveWhitespace !== false;\n    var whitespaceOption = options.whitespace;\n    var root;\n    var currentParent;\n    var inVPre = false;\n    var inPre = false;\n    var warned = false;\n\n    function warnOnce (msg, range) {\n      if (!warned) {\n        warned = true;\n        warn$2(msg, range);\n      }\n    }\n\n    function closeElement (element) {\n      trimEndingWhitespace(element);\n      if (!inVPre && !element.processed) {\n        element = processElement(element, options);\n      }\n      // tree management\n      if (!stack.length && element !== root) {\n        // allow root elements with v-if, v-else-if and v-else\n        if (root.if && (element.elseif || element.else)) {\n          {\n            checkRootConstraints(element);\n          }\n          addIfCondition(root, {\n            exp: element.elseif,\n            block: element\n          });\n        } else {\n          warnOnce(\n            \"Component template should contain exactly one root element. \" +\n            \"If you are using v-if on multiple elements, \" +\n            \"use v-else-if to chain them instead.\",\n            { start: element.start }\n          );\n        }\n      }\n      if (currentParent && !element.forbidden) {\n        if (element.elseif || element.else) {\n          processIfConditions(element, currentParent);\n        } else {\n          if (element.slotScope) {\n            // scoped slot\n            // keep it in the children list so that v-else(-if) conditions can\n            // find it as the prev node.\n            var name = element.slotTarget || '\"default\"'\n            ;(currentParent.scopedSlots || (currentParent.scopedSlots = {}))[name] = element;\n          }\n          currentParent.children.push(element);\n          element.parent = currentParent;\n        }\n      }\n\n      // final children cleanup\n      // filter out scoped slots\n      element.children = element.children.filter(function (c) { return !(c).slotScope; });\n      // remove trailing whitespace node again\n      trimEndingWhitespace(element);\n\n      // check pre state\n      if (element.pre) {\n        inVPre = false;\n      }\n      if (platformIsPreTag(element.tag)) {\n        inPre = false;\n      }\n      // apply post-transforms\n      for (var i = 0; i < postTransforms.length; i++) {\n        postTransforms[i](element, options);\n      }\n    }\n\n    function trimEndingWhitespace (el) {\n      // remove trailing whitespace node\n      if (!inPre) {\n        var lastNode;\n        while (\n          (lastNode = el.children[el.children.length - 1]) &&\n          lastNode.type === 3 &&\n          lastNode.text === ' '\n        ) {\n          el.children.pop();\n        }\n      }\n    }\n\n    function checkRootConstraints (el) {\n      if (el.tag === 'slot' || el.tag === 'template') {\n        warnOnce(\n          \"Cannot use <\" + (el.tag) + \"> as component root element because it may \" +\n          'contain multiple nodes.',\n          { start: el.start }\n        );\n      }\n      if (el.attrsMap.hasOwnProperty('v-for')) {\n        warnOnce(\n          'Cannot use v-for on stateful component root element because ' +\n          'it renders multiple elements.',\n          el.rawAttrsMap['v-for']\n        );\n      }\n    }\n\n    parseHTML(template, {\n      warn: warn$2,\n      expectHTML: options.expectHTML,\n      isUnaryTag: options.isUnaryTag,\n      canBeLeftOpenTag: options.canBeLeftOpenTag,\n      shouldDecodeNewlines: options.shouldDecodeNewlines,\n      shouldDecodeNewlinesForHref: options.shouldDecodeNewlinesForHref,\n      shouldKeepComment: options.comments,\n      outputSourceRange: options.outputSourceRange,\n      start: function start (tag, attrs, unary, start$1, end) {\n        // check namespace.\n        // inherit parent ns if there is one\n        var ns = (currentParent && currentParent.ns) || platformGetTagNamespace(tag);\n\n        // handle IE svg bug\n        /* istanbul ignore if */\n        if (isIE && ns === 'svg') {\n          attrs = guardIESVGBug(attrs);\n        }\n\n        var element = createASTElement(tag, attrs, currentParent);\n        if (ns) {\n          element.ns = ns;\n        }\n\n        {\n          if (options.outputSourceRange) {\n            element.start = start$1;\n            element.end = end;\n            element.rawAttrsMap = element.attrsList.reduce(function (cumulated, attr) {\n              cumulated[attr.name] = attr;\n              return cumulated\n            }, {});\n          }\n          attrs.forEach(function (attr) {\n            if (invalidAttributeRE.test(attr.name)) {\n              warn$2(\n                \"Invalid dynamic argument expression: attribute names cannot contain \" +\n                \"spaces, quotes, <, >, / or =.\",\n                {\n                  start: attr.start + attr.name.indexOf(\"[\"),\n                  end: attr.start + attr.name.length\n                }\n              );\n            }\n          });\n        }\n\n        if (isForbiddenTag(element) && !isServerRendering()) {\n          element.forbidden = true;\n          warn$2(\n            'Templates should only be responsible for mapping the state to the ' +\n            'UI. Avoid placing tags with side-effects in your templates, such as ' +\n            \"<\" + tag + \">\" + ', as they will not be parsed.',\n            { start: element.start }\n          );\n        }\n\n        // apply pre-transforms\n        for (var i = 0; i < preTransforms.length; i++) {\n          element = preTransforms[i](element, options) || element;\n        }\n\n        if (!inVPre) {\n          processPre(element);\n          if (element.pre) {\n            inVPre = true;\n          }\n        }\n        if (platformIsPreTag(element.tag)) {\n          inPre = true;\n        }\n        if (inVPre) {\n          processRawAttrs(element);\n        } else if (!element.processed) {\n          // structural directives\n          processFor(element);\n          processIf(element);\n          processOnce(element);\n        }\n\n        if (!root) {\n          root = element;\n          {\n            checkRootConstraints(root);\n          }\n        }\n\n        if (!unary) {\n          currentParent = element;\n          stack.push(element);\n        } else {\n          closeElement(element);\n        }\n      },\n\n      end: function end (tag, start, end$1) {\n        var element = stack[stack.length - 1];\n        // pop stack\n        stack.length -= 1;\n        currentParent = stack[stack.length - 1];\n        if (options.outputSourceRange) {\n          element.end = end$1;\n        }\n        closeElement(element);\n      },\n\n      chars: function chars (text, start, end) {\n        if (!currentParent) {\n          {\n            if (text === template) {\n              warnOnce(\n                'Component template requires a root element, rather than just text.',\n                { start: start }\n              );\n            } else if ((text = text.trim())) {\n              warnOnce(\n                (\"text \\\"\" + text + \"\\\" outside root element will be ignored.\"),\n                { start: start }\n              );\n            }\n          }\n          return\n        }\n        // IE textarea placeholder bug\n        /* istanbul ignore if */\n        if (isIE &&\n          currentParent.tag === 'textarea' &&\n          currentParent.attrsMap.placeholder === text\n        ) {\n          return\n        }\n        var children = currentParent.children;\n        if (inPre || text.trim()) {\n          text = isTextTag(currentParent) ? text : decodeHTMLCached(text);\n        } else if (!children.length) {\n          // remove the whitespace-only node right after an opening tag\n          text = '';\n        } else if (whitespaceOption) {\n          if (whitespaceOption === 'condense') {\n            // in condense mode, remove the whitespace node if it contains\n            // line break, otherwise condense to a single space\n            text = lineBreakRE.test(text) ? '' : ' ';\n          } else {\n            text = ' ';\n          }\n        } else {\n          text = preserveWhitespace ? ' ' : '';\n        }\n        if (text) {\n          if (!inPre && whitespaceOption === 'condense') {\n            // condense consecutive whitespaces into single space\n            text = text.replace(whitespaceRE$1, ' ');\n          }\n          var res;\n          var child;\n          if (!inVPre && text !== ' ' && (res = parseText(text, delimiters))) {\n            child = {\n              type: 2,\n              expression: res.expression,\n              tokens: res.tokens,\n              text: text\n            };\n          } else if (text !== ' ' || !children.length || children[children.length - 1].text !== ' ') {\n            child = {\n              type: 3,\n              text: text\n            };\n          }\n          if (child) {\n            if (options.outputSourceRange) {\n              child.start = start;\n              child.end = end;\n            }\n            children.push(child);\n          }\n        }\n      },\n      comment: function comment (text, start, end) {\n        // adding anyting as a sibling to the root node is forbidden\n        // comments should still be allowed, but ignored\n        if (currentParent) {\n          var child = {\n            type: 3,\n            text: text,\n            isComment: true\n          };\n          if (options.outputSourceRange) {\n            child.start = start;\n            child.end = end;\n          }\n          currentParent.children.push(child);\n        }\n      }\n    });\n    return root\n  }\n\n  function processPre (el) {\n    if (getAndRemoveAttr(el, 'v-pre') != null) {\n      el.pre = true;\n    }\n  }\n\n  function processRawAttrs (el) {\n    var list = el.attrsList;\n    var len = list.length;\n    if (len) {\n      var attrs = el.attrs = new Array(len);\n      for (var i = 0; i < len; i++) {\n        attrs[i] = {\n          name: list[i].name,\n          value: JSON.stringify(list[i].value)\n        };\n        if (list[i].start != null) {\n          attrs[i].start = list[i].start;\n          attrs[i].end = list[i].end;\n        }\n      }\n    } else if (!el.pre) {\n      // non root node in pre blocks with no attributes\n      el.plain = true;\n    }\n  }\n\n  function processElement (\n    element,\n    options\n  ) {\n    processKey(element);\n\n    // determine whether this is a plain element after\n    // removing structural attributes\n    element.plain = (\n      !element.key &&\n      !element.scopedSlots &&\n      !element.attrsList.length\n    );\n\n    processRef(element);\n    processSlotContent(element);\n    processSlotOutlet(element);\n    processComponent(element);\n    for (var i = 0; i < transforms.length; i++) {\n      element = transforms[i](element, options) || element;\n    }\n    processAttrs(element);\n    return element\n  }\n\n  function processKey (el) {\n    var exp = getBindingAttr(el, 'key');\n    if (exp) {\n      {\n        if (el.tag === 'template') {\n          warn$2(\n            \"<template> cannot be keyed. Place the key on real elements instead.\",\n            getRawBindingAttr(el, 'key')\n          );\n        }\n        if (el.for) {\n          var iterator = el.iterator2 || el.iterator1;\n          var parent = el.parent;\n          if (iterator && iterator === exp && parent && parent.tag === 'transition-group') {\n            warn$2(\n              \"Do not use v-for index as key on <transition-group> children, \" +\n              \"this is the same as not using keys.\",\n              getRawBindingAttr(el, 'key'),\n              true /* tip */\n            );\n          }\n        }\n      }\n      el.key = exp;\n    }\n  }\n\n  function processRef (el) {\n    var ref = getBindingAttr(el, 'ref');\n    if (ref) {\n      el.ref = ref;\n      el.refInFor = checkInFor(el);\n    }\n  }\n\n  function processFor (el) {\n    var exp;\n    if ((exp = getAndRemoveAttr(el, 'v-for'))) {\n      var res = parseFor(exp);\n      if (res) {\n        extend(el, res);\n      } else {\n        warn$2(\n          (\"Invalid v-for expression: \" + exp),\n          el.rawAttrsMap['v-for']\n        );\n      }\n    }\n  }\n\n\n\n  function parseFor (exp) {\n    var inMatch = exp.match(forAliasRE);\n    if (!inMatch) { return }\n    var res = {};\n    res.for = inMatch[2].trim();\n    var alias = inMatch[1].trim().replace(stripParensRE, '');\n    var iteratorMatch = alias.match(forIteratorRE);\n    if (iteratorMatch) {\n      res.alias = alias.replace(forIteratorRE, '').trim();\n      res.iterator1 = iteratorMatch[1].trim();\n      if (iteratorMatch[2]) {\n        res.iterator2 = iteratorMatch[2].trim();\n      }\n    } else {\n      res.alias = alias;\n    }\n    return res\n  }\n\n  function processIf (el) {\n    var exp = getAndRemoveAttr(el, 'v-if');\n    if (exp) {\n      el.if = exp;\n      addIfCondition(el, {\n        exp: exp,\n        block: el\n      });\n    } else {\n      if (getAndRemoveAttr(el, 'v-else') != null) {\n        el.else = true;\n      }\n      var elseif = getAndRemoveAttr(el, 'v-else-if');\n      if (elseif) {\n        el.elseif = elseif;\n      }\n    }\n  }\n\n  function processIfConditions (el, parent) {\n    var prev = findPrevElement(parent.children);\n    if (prev && prev.if) {\n      addIfCondition(prev, {\n        exp: el.elseif,\n        block: el\n      });\n    } else {\n      warn$2(\n        \"v-\" + (el.elseif ? ('else-if=\"' + el.elseif + '\"') : 'else') + \" \" +\n        \"used on element <\" + (el.tag) + \"> without corresponding v-if.\",\n        el.rawAttrsMap[el.elseif ? 'v-else-if' : 'v-else']\n      );\n    }\n  }\n\n  function findPrevElement (children) {\n    var i = children.length;\n    while (i--) {\n      if (children[i].type === 1) {\n        return children[i]\n      } else {\n        if (children[i].text !== ' ') {\n          warn$2(\n            \"text \\\"\" + (children[i].text.trim()) + \"\\\" between v-if and v-else(-if) \" +\n            \"will be ignored.\",\n            children[i]\n          );\n        }\n        children.pop();\n      }\n    }\n  }\n\n  function addIfCondition (el, condition) {\n    if (!el.ifConditions) {\n      el.ifConditions = [];\n    }\n    el.ifConditions.push(condition);\n  }\n\n  function processOnce (el) {\n    var once$$1 = getAndRemoveAttr(el, 'v-once');\n    if (once$$1 != null) {\n      el.once = true;\n    }\n  }\n\n  // handle content being passed to a component as slot,\n  // e.g. <template slot=\"xxx\">, <div slot-scope=\"xxx\">\n  function processSlotContent (el) {\n    var slotScope;\n    if (el.tag === 'template') {\n      slotScope = getAndRemoveAttr(el, 'scope');\n      /* istanbul ignore if */\n      if (slotScope) {\n        warn$2(\n          \"the \\\"scope\\\" attribute for scoped slots have been deprecated and \" +\n          \"replaced by \\\"slot-scope\\\" since 2.5. The new \\\"slot-scope\\\" attribute \" +\n          \"can also be used on plain elements in addition to <template> to \" +\n          \"denote scoped slots.\",\n          el.rawAttrsMap['scope'],\n          true\n        );\n      }\n      el.slotScope = slotScope || getAndRemoveAttr(el, 'slot-scope');\n    } else if ((slotScope = getAndRemoveAttr(el, 'slot-scope'))) {\n      /* istanbul ignore if */\n      if (el.attrsMap['v-for']) {\n        warn$2(\n          \"Ambiguous combined usage of slot-scope and v-for on <\" + (el.tag) + \"> \" +\n          \"(v-for takes higher priority). Use a wrapper <template> for the \" +\n          \"scoped slot to make it clearer.\",\n          el.rawAttrsMap['slot-scope'],\n          true\n        );\n      }\n      el.slotScope = slotScope;\n    }\n\n    // slot=\"xxx\"\n    var slotTarget = getBindingAttr(el, 'slot');\n    if (slotTarget) {\n      el.slotTarget = slotTarget === '\"\"' ? '\"default\"' : slotTarget;\n      el.slotTargetDynamic = !!(el.attrsMap[':slot'] || el.attrsMap['v-bind:slot']);\n      // preserve slot as an attribute for native shadow DOM compat\n      // only for non-scoped slots.\n      if (el.tag !== 'template' && !el.slotScope) {\n        addAttr(el, 'slot', slotTarget, getRawBindingAttr(el, 'slot'));\n      }\n    }\n\n    // 2.6 v-slot syntax\n    {\n      if (el.tag === 'template') {\n        // v-slot on <template>\n        var slotBinding = getAndRemoveAttrByRegex(el, slotRE);\n        if (slotBinding) {\n          {\n            if (el.slotTarget || el.slotScope) {\n              warn$2(\n                \"Unexpected mixed usage of different slot syntaxes.\",\n                el\n              );\n            }\n            if (el.parent && !maybeComponent(el.parent)) {\n              warn$2(\n                \"<template v-slot> can only appear at the root level inside \" +\n                \"the receiving component\",\n                el\n              );\n            }\n          }\n          var ref = getSlotName(slotBinding);\n          var name = ref.name;\n          var dynamic = ref.dynamic;\n          el.slotTarget = name;\n          el.slotTargetDynamic = dynamic;\n          el.slotScope = slotBinding.value || emptySlotScopeToken; // force it into a scoped slot for perf\n        }\n      } else {\n        // v-slot on component, denotes default slot\n        var slotBinding$1 = getAndRemoveAttrByRegex(el, slotRE);\n        if (slotBinding$1) {\n          {\n            if (!maybeComponent(el)) {\n              warn$2(\n                \"v-slot can only be used on components or <template>.\",\n                slotBinding$1\n              );\n            }\n            if (el.slotScope || el.slotTarget) {\n              warn$2(\n                \"Unexpected mixed usage of different slot syntaxes.\",\n                el\n              );\n            }\n            if (el.scopedSlots) {\n              warn$2(\n                \"To avoid scope ambiguity, the default slot should also use \" +\n                \"<template> syntax when there are other named slots.\",\n                slotBinding$1\n              );\n            }\n          }\n          // add the component's children to its default slot\n          var slots = el.scopedSlots || (el.scopedSlots = {});\n          var ref$1 = getSlotName(slotBinding$1);\n          var name$1 = ref$1.name;\n          var dynamic$1 = ref$1.dynamic;\n          var slotContainer = slots[name$1] = createASTElement('template', [], el);\n          slotContainer.slotTarget = name$1;\n          slotContainer.slotTargetDynamic = dynamic$1;\n          slotContainer.children = el.children.filter(function (c) {\n            if (!c.slotScope) {\n              c.parent = slotContainer;\n              return true\n            }\n          });\n          slotContainer.slotScope = slotBinding$1.value || emptySlotScopeToken;\n          // remove children as they are returned from scopedSlots now\n          el.children = [];\n          // mark el non-plain so data gets generated\n          el.plain = false;\n        }\n      }\n    }\n  }\n\n  function getSlotName (binding) {\n    var name = binding.name.replace(slotRE, '');\n    if (!name) {\n      if (binding.name[0] !== '#') {\n        name = 'default';\n      } else {\n        warn$2(\n          \"v-slot shorthand syntax requires a slot name.\",\n          binding\n        );\n      }\n    }\n    return dynamicArgRE.test(name)\n      // dynamic [name]\n      ? { name: name.slice(1, -1), dynamic: true }\n      // static name\n      : { name: (\"\\\"\" + name + \"\\\"\"), dynamic: false }\n  }\n\n  // handle <slot/> outlets\n  function processSlotOutlet (el) {\n    if (el.tag === 'slot') {\n      el.slotName = getBindingAttr(el, 'name');\n      if (el.key) {\n        warn$2(\n          \"`key` does not work on <slot> because slots are abstract outlets \" +\n          \"and can possibly expand into multiple elements. \" +\n          \"Use the key on a wrapping element instead.\",\n          getRawBindingAttr(el, 'key')\n        );\n      }\n    }\n  }\n\n  function processComponent (el) {\n    var binding;\n    if ((binding = getBindingAttr(el, 'is'))) {\n      el.component = binding;\n    }\n    if (getAndRemoveAttr(el, 'inline-template') != null) {\n      el.inlineTemplate = true;\n    }\n  }\n\n  function processAttrs (el) {\n    var list = el.attrsList;\n    var i, l, name, rawName, value, modifiers, syncGen, isDynamic;\n    for (i = 0, l = list.length; i < l; i++) {\n      name = rawName = list[i].name;\n      value = list[i].value;\n      if (dirRE.test(name)) {\n        // mark element as dynamic\n        el.hasBindings = true;\n        // modifiers\n        modifiers = parseModifiers(name.replace(dirRE, ''));\n        // support .foo shorthand syntax for the .prop modifier\n        if (modifiers) {\n          name = name.replace(modifierRE, '');\n        }\n        if (bindRE.test(name)) { // v-bind\n          name = name.replace(bindRE, '');\n          value = parseFilters(value);\n          isDynamic = dynamicArgRE.test(name);\n          if (isDynamic) {\n            name = name.slice(1, -1);\n          }\n          if (\n            value.trim().length === 0\n          ) {\n            warn$2(\n              (\"The value for a v-bind expression cannot be empty. Found in \\\"v-bind:\" + name + \"\\\"\")\n            );\n          }\n          if (modifiers) {\n            if (modifiers.prop && !isDynamic) {\n              name = camelize(name);\n              if (name === 'innerHtml') { name = 'innerHTML'; }\n            }\n            if (modifiers.camel && !isDynamic) {\n              name = camelize(name);\n            }\n            if (modifiers.sync) {\n              syncGen = genAssignmentCode(value, \"$event\");\n              if (!isDynamic) {\n                addHandler(\n                  el,\n                  (\"update:\" + (camelize(name))),\n                  syncGen,\n                  null,\n                  false,\n                  warn$2,\n                  list[i]\n                );\n                if (hyphenate(name) !== camelize(name)) {\n                  addHandler(\n                    el,\n                    (\"update:\" + (hyphenate(name))),\n                    syncGen,\n                    null,\n                    false,\n                    warn$2,\n                    list[i]\n                  );\n                }\n              } else {\n                // handler w/ dynamic event name\n                addHandler(\n                  el,\n                  (\"\\\"update:\\\"+(\" + name + \")\"),\n                  syncGen,\n                  null,\n                  false,\n                  warn$2,\n                  list[i],\n                  true // dynamic\n                );\n              }\n            }\n          }\n          if ((modifiers && modifiers.prop) || (\n            !el.component && platformMustUseProp(el.tag, el.attrsMap.type, name)\n          )) {\n            addProp(el, name, value, list[i], isDynamic);\n          } else {\n            addAttr(el, name, value, list[i], isDynamic);\n          }\n        } else if (onRE.test(name)) { // v-on\n          name = name.replace(onRE, '');\n          isDynamic = dynamicArgRE.test(name);\n          if (isDynamic) {\n            name = name.slice(1, -1);\n          }\n          addHandler(el, name, value, modifiers, false, warn$2, list[i], isDynamic);\n        } else { // normal directives\n          name = name.replace(dirRE, '');\n          // parse arg\n          var argMatch = name.match(argRE);\n          var arg = argMatch && argMatch[1];\n          isDynamic = false;\n          if (arg) {\n            name = name.slice(0, -(arg.length + 1));\n            if (dynamicArgRE.test(arg)) {\n              arg = arg.slice(1, -1);\n              isDynamic = true;\n            }\n          }\n          addDirective(el, name, rawName, value, arg, isDynamic, modifiers, list[i]);\n          if (name === 'model') {\n            checkForAliasModel(el, value);\n          }\n        }\n      } else {\n        // literal attribute\n        {\n          var res = parseText(value, delimiters);\n          if (res) {\n            warn$2(\n              name + \"=\\\"\" + value + \"\\\": \" +\n              'Interpolation inside attributes has been removed. ' +\n              'Use v-bind or the colon shorthand instead. For example, ' +\n              'instead of <div id=\"{{ val }}\">, use <div :id=\"val\">.',\n              list[i]\n            );\n          }\n        }\n        addAttr(el, name, JSON.stringify(value), list[i]);\n        // #6887 firefox doesn't update muted state if set via attribute\n        // even immediately after element creation\n        if (!el.component &&\n            name === 'muted' &&\n            platformMustUseProp(el.tag, el.attrsMap.type, name)) {\n          addProp(el, name, 'true', list[i]);\n        }\n      }\n    }\n  }\n\n  function checkInFor (el) {\n    var parent = el;\n    while (parent) {\n      if (parent.for !== undefined) {\n        return true\n      }\n      parent = parent.parent;\n    }\n    return false\n  }\n\n  function parseModifiers (name) {\n    var match = name.match(modifierRE);\n    if (match) {\n      var ret = {};\n      match.forEach(function (m) { ret[m.slice(1)] = true; });\n      return ret\n    }\n  }\n\n  function makeAttrsMap (attrs) {\n    var map = {};\n    for (var i = 0, l = attrs.length; i < l; i++) {\n      if (\n        map[attrs[i].name] && !isIE && !isEdge\n      ) {\n        warn$2('duplicate attribute: ' + attrs[i].name, attrs[i]);\n      }\n      map[attrs[i].name] = attrs[i].value;\n    }\n    return map\n  }\n\n  // for script (e.g. type=\"x/template\") or style, do not decode content\n  function isTextTag (el) {\n    return el.tag === 'script' || el.tag === 'style'\n  }\n\n  function isForbiddenTag (el) {\n    return (\n      el.tag === 'style' ||\n      (el.tag === 'script' && (\n        !el.attrsMap.type ||\n        el.attrsMap.type === 'text/javascript'\n      ))\n    )\n  }\n\n  var ieNSBug = /^xmlns:NS\\d+/;\n  var ieNSPrefix = /^NS\\d+:/;\n\n  /* istanbul ignore next */\n  function guardIESVGBug (attrs) {\n    var res = [];\n    for (var i = 0; i < attrs.length; i++) {\n      var attr = attrs[i];\n      if (!ieNSBug.test(attr.name)) {\n        attr.name = attr.name.replace(ieNSPrefix, '');\n        res.push(attr);\n      }\n    }\n    return res\n  }\n\n  function checkForAliasModel (el, value) {\n    var _el = el;\n    while (_el) {\n      if (_el.for && _el.alias === value) {\n        warn$2(\n          \"<\" + (el.tag) + \" v-model=\\\"\" + value + \"\\\">: \" +\n          \"You are binding v-model directly to a v-for iteration alias. \" +\n          \"This will not be able to modify the v-for source array because \" +\n          \"writing to the alias is like modifying a function local variable. \" +\n          \"Consider using an array of objects and use v-model on an object property instead.\",\n          el.rawAttrsMap['v-model']\n        );\n      }\n      _el = _el.parent;\n    }\n  }\n\n  /*  */\n\n  function preTransformNode (el, options) {\n    if (el.tag === 'input') {\n      var map = el.attrsMap;\n      if (!map['v-model']) {\n        return\n      }\n\n      var typeBinding;\n      if (map[':type'] || map['v-bind:type']) {\n        typeBinding = getBindingAttr(el, 'type');\n      }\n      if (!map.type && !typeBinding && map['v-bind']) {\n        typeBinding = \"(\" + (map['v-bind']) + \").type\";\n      }\n\n      if (typeBinding) {\n        var ifCondition = getAndRemoveAttr(el, 'v-if', true);\n        var ifConditionExtra = ifCondition ? (\"&&(\" + ifCondition + \")\") : \"\";\n        var hasElse = getAndRemoveAttr(el, 'v-else', true) != null;\n        var elseIfCondition = getAndRemoveAttr(el, 'v-else-if', true);\n        // 1. checkbox\n        var branch0 = cloneASTElement(el);\n        // process for on the main node\n        processFor(branch0);\n        addRawAttr(branch0, 'type', 'checkbox');\n        processElement(branch0, options);\n        branch0.processed = true; // prevent it from double-processed\n        branch0.if = \"(\" + typeBinding + \")==='checkbox'\" + ifConditionExtra;\n        addIfCondition(branch0, {\n          exp: branch0.if,\n          block: branch0\n        });\n        // 2. add radio else-if condition\n        var branch1 = cloneASTElement(el);\n        getAndRemoveAttr(branch1, 'v-for', true);\n        addRawAttr(branch1, 'type', 'radio');\n        processElement(branch1, options);\n        addIfCondition(branch0, {\n          exp: \"(\" + typeBinding + \")==='radio'\" + ifConditionExtra,\n          block: branch1\n        });\n        // 3. other\n        var branch2 = cloneASTElement(el);\n        getAndRemoveAttr(branch2, 'v-for', true);\n        addRawAttr(branch2, ':type', typeBinding);\n        processElement(branch2, options);\n        addIfCondition(branch0, {\n          exp: ifCondition,\n          block: branch2\n        });\n\n        if (hasElse) {\n          branch0.else = true;\n        } else if (elseIfCondition) {\n          branch0.elseif = elseIfCondition;\n        }\n\n        return branch0\n      }\n    }\n  }\n\n  function cloneASTElement (el) {\n    return createASTElement(el.tag, el.attrsList.slice(), el.parent)\n  }\n\n  var model$1 = {\n    preTransformNode: preTransformNode\n  };\n\n  var modules$1 = [\n    klass$1,\n    style$1,\n    model$1\n  ];\n\n  /*  */\n\n  function text (el, dir) {\n    if (dir.value) {\n      addProp(el, 'textContent', (\"_s(\" + (dir.value) + \")\"), dir);\n    }\n  }\n\n  /*  */\n\n  function html (el, dir) {\n    if (dir.value) {\n      addProp(el, 'innerHTML', (\"_s(\" + (dir.value) + \")\"), dir);\n    }\n  }\n\n  var directives$1 = {\n    model: model,\n    text: text,\n    html: html\n  };\n\n  /*  */\n\n  var baseOptions = {\n    expectHTML: true,\n    modules: modules$1,\n    directives: directives$1,\n    isPreTag: isPreTag,\n    isUnaryTag: isUnaryTag,\n    mustUseProp: mustUseProp,\n    canBeLeftOpenTag: canBeLeftOpenTag,\n    isReservedTag: isReservedTag,\n    getTagNamespace: getTagNamespace,\n    staticKeys: genStaticKeys(modules$1)\n  };\n\n  /*  */\n\n  var isStaticKey;\n  var isPlatformReservedTag;\n\n  var genStaticKeysCached = cached(genStaticKeys$1);\n\n  /**\n   * Goal of the optimizer: walk the generated template AST tree\n   * and detect sub-trees that are purely static, i.e. parts of\n   * the DOM that never needs to change.\n   *\n   * Once we detect these sub-trees, we can:\n   *\n   * 1. Hoist them into constants, so that we no longer need to\n   *    create fresh nodes for them on each re-render;\n   * 2. Completely skip them in the patching process.\n   */\n  function optimize (root, options) {\n    if (!root) { return }\n    isStaticKey = genStaticKeysCached(options.staticKeys || '');\n    isPlatformReservedTag = options.isReservedTag || no;\n    // first pass: mark all non-static nodes.\n    markStatic$1(root);\n    // second pass: mark static roots.\n    markStaticRoots(root, false);\n  }\n\n  function genStaticKeys$1 (keys) {\n    return makeMap(\n      'type,tag,attrsList,attrsMap,plain,parent,children,attrs,start,end,rawAttrsMap' +\n      (keys ? ',' + keys : '')\n    )\n  }\n\n  function markStatic$1 (node) {\n    node.static = isStatic(node);\n    if (node.type === 1) {\n      // do not make component slot content static. this avoids\n      // 1. components not able to mutate slot nodes\n      // 2. static slot content fails for hot-reloading\n      if (\n        !isPlatformReservedTag(node.tag) &&\n        node.tag !== 'slot' &&\n        node.attrsMap['inline-template'] == null\n      ) {\n        return\n      }\n      for (var i = 0, l = node.children.length; i < l; i++) {\n        var child = node.children[i];\n        markStatic$1(child);\n        if (!child.static) {\n          node.static = false;\n        }\n      }\n      if (node.ifConditions) {\n        for (var i$1 = 1, l$1 = node.ifConditions.length; i$1 < l$1; i$1++) {\n          var block = node.ifConditions[i$1].block;\n          markStatic$1(block);\n          if (!block.static) {\n            node.static = false;\n          }\n        }\n      }\n    }\n  }\n\n  function markStaticRoots (node, isInFor) {\n    if (node.type === 1) {\n      if (node.static || node.once) {\n        node.staticInFor = isInFor;\n      }\n      // For a node to qualify as a static root, it should have children that\n      // are not just static text. Otherwise the cost of hoisting out will\n      // outweigh the benefits and it's better off to just always render it fresh.\n      if (node.static && node.children.length && !(\n        node.children.length === 1 &&\n        node.children[0].type === 3\n      )) {\n        node.staticRoot = true;\n        return\n      } else {\n        node.staticRoot = false;\n      }\n      if (node.children) {\n        for (var i = 0, l = node.children.length; i < l; i++) {\n          markStaticRoots(node.children[i], isInFor || !!node.for);\n        }\n      }\n      if (node.ifConditions) {\n        for (var i$1 = 1, l$1 = node.ifConditions.length; i$1 < l$1; i$1++) {\n          markStaticRoots(node.ifConditions[i$1].block, isInFor);\n        }\n      }\n    }\n  }\n\n  function isStatic (node) {\n    if (node.type === 2) { // expression\n      return false\n    }\n    if (node.type === 3) { // text\n      return true\n    }\n    return !!(node.pre || (\n      !node.hasBindings && // no dynamic bindings\n      !node.if && !node.for && // not v-if or v-for or v-else\n      !isBuiltInTag(node.tag) && // not a built-in\n      isPlatformReservedTag(node.tag) && // not a component\n      !isDirectChildOfTemplateFor(node) &&\n      Object.keys(node).every(isStaticKey)\n    ))\n  }\n\n  function isDirectChildOfTemplateFor (node) {\n    while (node.parent) {\n      node = node.parent;\n      if (node.tag !== 'template') {\n        return false\n      }\n      if (node.for) {\n        return true\n      }\n    }\n    return false\n  }\n\n  /*  */\n\n  var fnExpRE = /^([\\w$_]+|\\([^)]*?\\))\\s*=>|^function(?:\\s+[\\w$]+)?\\s*\\(/;\n  var fnInvokeRE = /\\([^)]*?\\);*$/;\n  var simplePathRE = /^[A-Za-z_$][\\w$]*(?:\\.[A-Za-z_$][\\w$]*|\\['[^']*?']|\\[\"[^\"]*?\"]|\\[\\d+]|\\[[A-Za-z_$][\\w$]*])*$/;\n\n  // KeyboardEvent.keyCode aliases\n  var keyCodes = {\n    esc: 27,\n    tab: 9,\n    enter: 13,\n    space: 32,\n    up: 38,\n    left: 37,\n    right: 39,\n    down: 40,\n    'delete': [8, 46]\n  };\n\n  // KeyboardEvent.key aliases\n  var keyNames = {\n    // #7880: IE11 and Edge use `Esc` for Escape key name.\n    esc: ['Esc', 'Escape'],\n    tab: 'Tab',\n    enter: 'Enter',\n    // #9112: IE11 uses `Spacebar` for Space key name.\n    space: [' ', 'Spacebar'],\n    // #7806: IE11 uses key names without `Arrow` prefix for arrow keys.\n    up: ['Up', 'ArrowUp'],\n    left: ['Left', 'ArrowLeft'],\n    right: ['Right', 'ArrowRight'],\n    down: ['Down', 'ArrowDown'],\n    // #9112: IE11 uses `Del` for Delete key name.\n    'delete': ['Backspace', 'Delete', 'Del']\n  };\n\n  // #4868: modifiers that prevent the execution of the listener\n  // need to explicitly return null so that we can determine whether to remove\n  // the listener for .once\n  var genGuard = function (condition) { return (\"if(\" + condition + \")return null;\"); };\n\n  var modifierCode = {\n    stop: '$event.stopPropagation();',\n    prevent: '$event.preventDefault();',\n    self: genGuard(\"$event.target !== $event.currentTarget\"),\n    ctrl: genGuard(\"!$event.ctrlKey\"),\n    shift: genGuard(\"!$event.shiftKey\"),\n    alt: genGuard(\"!$event.altKey\"),\n    meta: genGuard(\"!$event.metaKey\"),\n    left: genGuard(\"'button' in $event && $event.button !== 0\"),\n    middle: genGuard(\"'button' in $event && $event.button !== 1\"),\n    right: genGuard(\"'button' in $event && $event.button !== 2\")\n  };\n\n  function genHandlers (\n    events,\n    isNative\n  ) {\n    var prefix = isNative ? 'nativeOn:' : 'on:';\n    var staticHandlers = \"\";\n    var dynamicHandlers = \"\";\n    for (var name in events) {\n      var handlerCode = genHandler(events[name]);\n      if (events[name] && events[name].dynamic) {\n        dynamicHandlers += name + \",\" + handlerCode + \",\";\n      } else {\n        staticHandlers += \"\\\"\" + name + \"\\\":\" + handlerCode + \",\";\n      }\n    }\n    staticHandlers = \"{\" + (staticHandlers.slice(0, -1)) + \"}\";\n    if (dynamicHandlers) {\n      return prefix + \"_d(\" + staticHandlers + \",[\" + (dynamicHandlers.slice(0, -1)) + \"])\"\n    } else {\n      return prefix + staticHandlers\n    }\n  }\n\n  function genHandler (handler) {\n    if (!handler) {\n      return 'function(){}'\n    }\n\n    if (Array.isArray(handler)) {\n      return (\"[\" + (handler.map(function (handler) { return genHandler(handler); }).join(',')) + \"]\")\n    }\n\n    var isMethodPath = simplePathRE.test(handler.value);\n    var isFunctionExpression = fnExpRE.test(handler.value);\n    var isFunctionInvocation = simplePathRE.test(handler.value.replace(fnInvokeRE, ''));\n\n    if (!handler.modifiers) {\n      if (isMethodPath || isFunctionExpression) {\n        return handler.value\n      }\n      return (\"function($event){\" + (isFunctionInvocation ? (\"return \" + (handler.value)) : handler.value) + \"}\") // inline statement\n    } else {\n      var code = '';\n      var genModifierCode = '';\n      var keys = [];\n      for (var key in handler.modifiers) {\n        if (modifierCode[key]) {\n          genModifierCode += modifierCode[key];\n          // left/right\n          if (keyCodes[key]) {\n            keys.push(key);\n          }\n        } else if (key === 'exact') {\n          var modifiers = (handler.modifiers);\n          genModifierCode += genGuard(\n            ['ctrl', 'shift', 'alt', 'meta']\n              .filter(function (keyModifier) { return !modifiers[keyModifier]; })\n              .map(function (keyModifier) { return (\"$event.\" + keyModifier + \"Key\"); })\n              .join('||')\n          );\n        } else {\n          keys.push(key);\n        }\n      }\n      if (keys.length) {\n        code += genKeyFilter(keys);\n      }\n      // Make sure modifiers like prevent and stop get executed after key filtering\n      if (genModifierCode) {\n        code += genModifierCode;\n      }\n      var handlerCode = isMethodPath\n        ? (\"return \" + (handler.value) + \"($event)\")\n        : isFunctionExpression\n          ? (\"return (\" + (handler.value) + \")($event)\")\n          : isFunctionInvocation\n            ? (\"return \" + (handler.value))\n            : handler.value;\n      return (\"function($event){\" + code + handlerCode + \"}\")\n    }\n  }\n\n  function genKeyFilter (keys) {\n    return (\n      // make sure the key filters only apply to KeyboardEvents\n      // #9441: can't use 'keyCode' in $event because Chrome autofill fires fake\n      // key events that do not have keyCode property...\n      \"if(!$event.type.indexOf('key')&&\" +\n      (keys.map(genFilterCode).join('&&')) + \")return null;\"\n    )\n  }\n\n  function genFilterCode (key) {\n    var keyVal = parseInt(key, 10);\n    if (keyVal) {\n      return (\"$event.keyCode!==\" + keyVal)\n    }\n    var keyCode = keyCodes[key];\n    var keyName = keyNames[key];\n    return (\n      \"_k($event.keyCode,\" +\n      (JSON.stringify(key)) + \",\" +\n      (JSON.stringify(keyCode)) + \",\" +\n      \"$event.key,\" +\n      \"\" + (JSON.stringify(keyName)) +\n      \")\"\n    )\n  }\n\n  /*  */\n\n  function on (el, dir) {\n    if (dir.modifiers) {\n      warn(\"v-on without argument does not support modifiers.\");\n    }\n    el.wrapListeners = function (code) { return (\"_g(\" + code + \",\" + (dir.value) + \")\"); };\n  }\n\n  /*  */\n\n  function bind$1 (el, dir) {\n    el.wrapData = function (code) {\n      return (\"_b(\" + code + \",'\" + (el.tag) + \"',\" + (dir.value) + \",\" + (dir.modifiers && dir.modifiers.prop ? 'true' : 'false') + (dir.modifiers && dir.modifiers.sync ? ',true' : '') + \")\")\n    };\n  }\n\n  /*  */\n\n  var baseDirectives = {\n    on: on,\n    bind: bind$1,\n    cloak: noop\n  };\n\n  /*  */\n\n\n\n\n\n  var CodegenState = function CodegenState (options) {\n    this.options = options;\n    this.warn = options.warn || baseWarn;\n    this.transforms = pluckModuleFunction(options.modules, 'transformCode');\n    this.dataGenFns = pluckModuleFunction(options.modules, 'genData');\n    this.directives = extend(extend({}, baseDirectives), options.directives);\n    var isReservedTag = options.isReservedTag || no;\n    this.maybeComponent = function (el) { return !!el.component || !isReservedTag(el.tag); };\n    this.onceId = 0;\n    this.staticRenderFns = [];\n    this.pre = false;\n  };\n\n\n\n  function generate (\n    ast,\n    options\n  ) {\n    var state = new CodegenState(options);\n    var code = ast ? genElement(ast, state) : '_c(\"div\")';\n    return {\n      render: (\"with(this){return \" + code + \"}\"),\n      staticRenderFns: state.staticRenderFns\n    }\n  }\n\n  function genElement (el, state) {\n    if (el.parent) {\n      el.pre = el.pre || el.parent.pre;\n    }\n\n    if (el.staticRoot && !el.staticProcessed) {\n      return genStatic(el, state)\n    } else if (el.once && !el.onceProcessed) {\n      return genOnce(el, state)\n    } else if (el.for && !el.forProcessed) {\n      return genFor(el, state)\n    } else if (el.if && !el.ifProcessed) {\n      return genIf(el, state)\n    } else if (el.tag === 'template' && !el.slotTarget && !state.pre) {\n      return genChildren(el, state) || 'void 0'\n    } else if (el.tag === 'slot') {\n      return genSlot(el, state)\n    } else {\n      // component or element\n      var code;\n      if (el.component) {\n        code = genComponent(el.component, el, state);\n      } else {\n        var data;\n        if (!el.plain || (el.pre && state.maybeComponent(el))) {\n          data = genData$2(el, state);\n        }\n\n        var children = el.inlineTemplate ? null : genChildren(el, state, true);\n        code = \"_c('\" + (el.tag) + \"'\" + (data ? (\",\" + data) : '') + (children ? (\",\" + children) : '') + \")\";\n      }\n      // module transforms\n      for (var i = 0; i < state.transforms.length; i++) {\n        code = state.transforms[i](el, code);\n      }\n      return code\n    }\n  }\n\n  // hoist static sub-trees out\n  function genStatic (el, state) {\n    el.staticProcessed = true;\n    // Some elements (templates) need to behave differently inside of a v-pre\n    // node.  All pre nodes are static roots, so we can use this as a location to\n    // wrap a state change and reset it upon exiting the pre node.\n    var originalPreState = state.pre;\n    if (el.pre) {\n      state.pre = el.pre;\n    }\n    state.staticRenderFns.push((\"with(this){return \" + (genElement(el, state)) + \"}\"));\n    state.pre = originalPreState;\n    return (\"_m(\" + (state.staticRenderFns.length - 1) + (el.staticInFor ? ',true' : '') + \")\")\n  }\n\n  // v-once\n  function genOnce (el, state) {\n    el.onceProcessed = true;\n    if (el.if && !el.ifProcessed) {\n      return genIf(el, state)\n    } else if (el.staticInFor) {\n      var key = '';\n      var parent = el.parent;\n      while (parent) {\n        if (parent.for) {\n          key = parent.key;\n          break\n        }\n        parent = parent.parent;\n      }\n      if (!key) {\n        state.warn(\n          \"v-once can only be used inside v-for that is keyed. \",\n          el.rawAttrsMap['v-once']\n        );\n        return genElement(el, state)\n      }\n      return (\"_o(\" + (genElement(el, state)) + \",\" + (state.onceId++) + \",\" + key + \")\")\n    } else {\n      return genStatic(el, state)\n    }\n  }\n\n  function genIf (\n    el,\n    state,\n    altGen,\n    altEmpty\n  ) {\n    el.ifProcessed = true; // avoid recursion\n    return genIfConditions(el.ifConditions.slice(), state, altGen, altEmpty)\n  }\n\n  function genIfConditions (\n    conditions,\n    state,\n    altGen,\n    altEmpty\n  ) {\n    if (!conditions.length) {\n      return altEmpty || '_e()'\n    }\n\n    var condition = conditions.shift();\n    if (condition.exp) {\n      return (\"(\" + (condition.exp) + \")?\" + (genTernaryExp(condition.block)) + \":\" + (genIfConditions(conditions, state, altGen, altEmpty)))\n    } else {\n      return (\"\" + (genTernaryExp(condition.block)))\n    }\n\n    // v-if with v-once should generate code like (a)?_m(0):_m(1)\n    function genTernaryExp (el) {\n      return altGen\n        ? altGen(el, state)\n        : el.once\n          ? genOnce(el, state)\n          : genElement(el, state)\n    }\n  }\n\n  function genFor (\n    el,\n    state,\n    altGen,\n    altHelper\n  ) {\n    var exp = el.for;\n    var alias = el.alias;\n    var iterator1 = el.iterator1 ? (\",\" + (el.iterator1)) : '';\n    var iterator2 = el.iterator2 ? (\",\" + (el.iterator2)) : '';\n\n    if (state.maybeComponent(el) &&\n      el.tag !== 'slot' &&\n      el.tag !== 'template' &&\n      !el.key\n    ) {\n      state.warn(\n        \"<\" + (el.tag) + \" v-for=\\\"\" + alias + \" in \" + exp + \"\\\">: component lists rendered with \" +\n        \"v-for should have explicit keys. \" +\n        \"See https://vuejs.org/guide/list.html#key for more info.\",\n        el.rawAttrsMap['v-for'],\n        true /* tip */\n      );\n    }\n\n    el.forProcessed = true; // avoid recursion\n    return (altHelper || '_l') + \"((\" + exp + \"),\" +\n      \"function(\" + alias + iterator1 + iterator2 + \"){\" +\n        \"return \" + ((altGen || genElement)(el, state)) +\n      '})'\n  }\n\n  function genData$2 (el, state) {\n    var data = '{';\n\n    // directives first.\n    // directives may mutate the el's other properties before they are generated.\n    var dirs = genDirectives(el, state);\n    if (dirs) { data += dirs + ','; }\n\n    // key\n    if (el.key) {\n      data += \"key:\" + (el.key) + \",\";\n    }\n    // ref\n    if (el.ref) {\n      data += \"ref:\" + (el.ref) + \",\";\n    }\n    if (el.refInFor) {\n      data += \"refInFor:true,\";\n    }\n    // pre\n    if (el.pre) {\n      data += \"pre:true,\";\n    }\n    // record original tag name for components using \"is\" attribute\n    if (el.component) {\n      data += \"tag:\\\"\" + (el.tag) + \"\\\",\";\n    }\n    // module data generation functions\n    for (var i = 0; i < state.dataGenFns.length; i++) {\n      data += state.dataGenFns[i](el);\n    }\n    // attributes\n    if (el.attrs) {\n      data += \"attrs:\" + (genProps(el.attrs)) + \",\";\n    }\n    // DOM props\n    if (el.props) {\n      data += \"domProps:\" + (genProps(el.props)) + \",\";\n    }\n    // event handlers\n    if (el.events) {\n      data += (genHandlers(el.events, false)) + \",\";\n    }\n    if (el.nativeEvents) {\n      data += (genHandlers(el.nativeEvents, true)) + \",\";\n    }\n    // slot target\n    // only for non-scoped slots\n    if (el.slotTarget && !el.slotScope) {\n      data += \"slot:\" + (el.slotTarget) + \",\";\n    }\n    // scoped slots\n    if (el.scopedSlots) {\n      data += (genScopedSlots(el, el.scopedSlots, state)) + \",\";\n    }\n    // component v-model\n    if (el.model) {\n      data += \"model:{value:\" + (el.model.value) + \",callback:\" + (el.model.callback) + \",expression:\" + (el.model.expression) + \"},\";\n    }\n    // inline-template\n    if (el.inlineTemplate) {\n      var inlineTemplate = genInlineTemplate(el, state);\n      if (inlineTemplate) {\n        data += inlineTemplate + \",\";\n      }\n    }\n    data = data.replace(/,$/, '') + '}';\n    // v-bind dynamic argument wrap\n    // v-bind with dynamic arguments must be applied using the same v-bind object\n    // merge helper so that class/style/mustUseProp attrs are handled correctly.\n    if (el.dynamicAttrs) {\n      data = \"_b(\" + data + \",\\\"\" + (el.tag) + \"\\\",\" + (genProps(el.dynamicAttrs)) + \")\";\n    }\n    // v-bind data wrap\n    if (el.wrapData) {\n      data = el.wrapData(data);\n    }\n    // v-on data wrap\n    if (el.wrapListeners) {\n      data = el.wrapListeners(data);\n    }\n    return data\n  }\n\n  function genDirectives (el, state) {\n    var dirs = el.directives;\n    if (!dirs) { return }\n    var res = 'directives:[';\n    var hasRuntime = false;\n    var i, l, dir, needRuntime;\n    for (i = 0, l = dirs.length; i < l; i++) {\n      dir = dirs[i];\n      needRuntime = true;\n      var gen = state.directives[dir.name];\n      if (gen) {\n        // compile-time directive that manipulates AST.\n        // returns true if it also needs a runtime counterpart.\n        needRuntime = !!gen(el, dir, state.warn);\n      }\n      if (needRuntime) {\n        hasRuntime = true;\n        res += \"{name:\\\"\" + (dir.name) + \"\\\",rawName:\\\"\" + (dir.rawName) + \"\\\"\" + (dir.value ? (\",value:(\" + (dir.value) + \"),expression:\" + (JSON.stringify(dir.value))) : '') + (dir.arg ? (\",arg:\" + (dir.isDynamicArg ? dir.arg : (\"\\\"\" + (dir.arg) + \"\\\"\"))) : '') + (dir.modifiers ? (\",modifiers:\" + (JSON.stringify(dir.modifiers))) : '') + \"},\";\n      }\n    }\n    if (hasRuntime) {\n      return res.slice(0, -1) + ']'\n    }\n  }\n\n  function genInlineTemplate (el, state) {\n    var ast = el.children[0];\n    if (el.children.length !== 1 || ast.type !== 1) {\n      state.warn(\n        'Inline-template components must have exactly one child element.',\n        { start: el.start }\n      );\n    }\n    if (ast && ast.type === 1) {\n      var inlineRenderFns = generate(ast, state.options);\n      return (\"inlineTemplate:{render:function(){\" + (inlineRenderFns.render) + \"},staticRenderFns:[\" + (inlineRenderFns.staticRenderFns.map(function (code) { return (\"function(){\" + code + \"}\"); }).join(',')) + \"]}\")\n    }\n  }\n\n  function genScopedSlots (\n    el,\n    slots,\n    state\n  ) {\n    // by default scoped slots are considered \"stable\", this allows child\n    // components with only scoped slots to skip forced updates from parent.\n    // but in some cases we have to bail-out of this optimization\n    // for example if the slot contains dynamic names, has v-if or v-for on them...\n    var needsForceUpdate = el.for || Object.keys(slots).some(function (key) {\n      var slot = slots[key];\n      return (\n        slot.slotTargetDynamic ||\n        slot.if ||\n        slot.for ||\n        containsSlotChild(slot) // is passing down slot from parent which may be dynamic\n      )\n    });\n\n    // #9534: if a component with scoped slots is inside a conditional branch,\n    // it's possible for the same component to be reused but with different\n    // compiled slot content. To avoid that, we generate a unique key based on\n    // the generated code of all the slot contents.\n    var needsKey = !!el.if;\n\n    // OR when it is inside another scoped slot or v-for (the reactivity may be\n    // disconnected due to the intermediate scope variable)\n    // #9438, #9506\n    // TODO: this can be further optimized by properly analyzing in-scope bindings\n    // and skip force updating ones that do not actually use scope variables.\n    if (!needsForceUpdate) {\n      var parent = el.parent;\n      while (parent) {\n        if (\n          (parent.slotScope && parent.slotScope !== emptySlotScopeToken) ||\n          parent.for\n        ) {\n          needsForceUpdate = true;\n          break\n        }\n        if (parent.if) {\n          needsKey = true;\n        }\n        parent = parent.parent;\n      }\n    }\n\n    var generatedSlots = Object.keys(slots)\n      .map(function (key) { return genScopedSlot(slots[key], state); })\n      .join(',');\n\n    return (\"scopedSlots:_u([\" + generatedSlots + \"]\" + (needsForceUpdate ? \",null,true\" : \"\") + (!needsForceUpdate && needsKey ? (\",null,false,\" + (hash(generatedSlots))) : \"\") + \")\")\n  }\n\n  function hash(str) {\n    var hash = 5381;\n    var i = str.length;\n    while(i) {\n      hash = (hash * 33) ^ str.charCodeAt(--i);\n    }\n    return hash >>> 0\n  }\n\n  function containsSlotChild (el) {\n    if (el.type === 1) {\n      if (el.tag === 'slot') {\n        return true\n      }\n      return el.children.some(containsSlotChild)\n    }\n    return false\n  }\n\n  function genScopedSlot (\n    el,\n    state\n  ) {\n    var isLegacySyntax = el.attrsMap['slot-scope'];\n    if (el.if && !el.ifProcessed && !isLegacySyntax) {\n      return genIf(el, state, genScopedSlot, \"null\")\n    }\n    if (el.for && !el.forProcessed) {\n      return genFor(el, state, genScopedSlot)\n    }\n    var slotScope = el.slotScope === emptySlotScopeToken\n      ? \"\"\n      : String(el.slotScope);\n    var fn = \"function(\" + slotScope + \"){\" +\n      \"return \" + (el.tag === 'template'\n        ? el.if && isLegacySyntax\n          ? (\"(\" + (el.if) + \")?\" + (genChildren(el, state) || 'undefined') + \":undefined\")\n          : genChildren(el, state) || 'undefined'\n        : genElement(el, state)) + \"}\";\n    // reverse proxy v-slot without scope on this.$slots\n    var reverseProxy = slotScope ? \"\" : \",proxy:true\";\n    return (\"{key:\" + (el.slotTarget || \"\\\"default\\\"\") + \",fn:\" + fn + reverseProxy + \"}\")\n  }\n\n  function genChildren (\n    el,\n    state,\n    checkSkip,\n    altGenElement,\n    altGenNode\n  ) {\n    var children = el.children;\n    if (children.length) {\n      var el$1 = children[0];\n      // optimize single v-for\n      if (children.length === 1 &&\n        el$1.for &&\n        el$1.tag !== 'template' &&\n        el$1.tag !== 'slot'\n      ) {\n        var normalizationType = checkSkip\n          ? state.maybeComponent(el$1) ? \",1\" : \",0\"\n          : \"\";\n        return (\"\" + ((altGenElement || genElement)(el$1, state)) + normalizationType)\n      }\n      var normalizationType$1 = checkSkip\n        ? getNormalizationType(children, state.maybeComponent)\n        : 0;\n      var gen = altGenNode || genNode;\n      return (\"[\" + (children.map(function (c) { return gen(c, state); }).join(',')) + \"]\" + (normalizationType$1 ? (\",\" + normalizationType$1) : ''))\n    }\n  }\n\n  // determine the normalization needed for the children array.\n  // 0: no normalization needed\n  // 1: simple normalization needed (possible 1-level deep nested array)\n  // 2: full normalization needed\n  function getNormalizationType (\n    children,\n    maybeComponent\n  ) {\n    var res = 0;\n    for (var i = 0; i < children.length; i++) {\n      var el = children[i];\n      if (el.type !== 1) {\n        continue\n      }\n      if (needsNormalization(el) ||\n          (el.ifConditions && el.ifConditions.some(function (c) { return needsNormalization(c.block); }))) {\n        res = 2;\n        break\n      }\n      if (maybeComponent(el) ||\n          (el.ifConditions && el.ifConditions.some(function (c) { return maybeComponent(c.block); }))) {\n        res = 1;\n      }\n    }\n    return res\n  }\n\n  function needsNormalization (el) {\n    return el.for !== undefined || el.tag === 'template' || el.tag === 'slot'\n  }\n\n  function genNode (node, state) {\n    if (node.type === 1) {\n      return genElement(node, state)\n    } else if (node.type === 3 && node.isComment) {\n      return genComment(node)\n    } else {\n      return genText(node)\n    }\n  }\n\n  function genText (text) {\n    return (\"_v(\" + (text.type === 2\n      ? text.expression // no need for () because already wrapped in _s()\n      : transformSpecialNewlines(JSON.stringify(text.text))) + \")\")\n  }\n\n  function genComment (comment) {\n    return (\"_e(\" + (JSON.stringify(comment.text)) + \")\")\n  }\n\n  function genSlot (el, state) {\n    var slotName = el.slotName || '\"default\"';\n    var children = genChildren(el, state);\n    var res = \"_t(\" + slotName + (children ? (\",\" + children) : '');\n    var attrs = el.attrs || el.dynamicAttrs\n      ? genProps((el.attrs || []).concat(el.dynamicAttrs || []).map(function (attr) { return ({\n          // slot props are camelized\n          name: camelize(attr.name),\n          value: attr.value,\n          dynamic: attr.dynamic\n        }); }))\n      : null;\n    var bind$$1 = el.attrsMap['v-bind'];\n    if ((attrs || bind$$1) && !children) {\n      res += \",null\";\n    }\n    if (attrs) {\n      res += \",\" + attrs;\n    }\n    if (bind$$1) {\n      res += (attrs ? '' : ',null') + \",\" + bind$$1;\n    }\n    return res + ')'\n  }\n\n  // componentName is el.component, take it as argument to shun flow's pessimistic refinement\n  function genComponent (\n    componentName,\n    el,\n    state\n  ) {\n    var children = el.inlineTemplate ? null : genChildren(el, state, true);\n    return (\"_c(\" + componentName + \",\" + (genData$2(el, state)) + (children ? (\",\" + children) : '') + \")\")\n  }\n\n  function genProps (props) {\n    var staticProps = \"\";\n    var dynamicProps = \"\";\n    for (var i = 0; i < props.length; i++) {\n      var prop = props[i];\n      var value = transformSpecialNewlines(prop.value);\n      if (prop.dynamic) {\n        dynamicProps += (prop.name) + \",\" + value + \",\";\n      } else {\n        staticProps += \"\\\"\" + (prop.name) + \"\\\":\" + value + \",\";\n      }\n    }\n    staticProps = \"{\" + (staticProps.slice(0, -1)) + \"}\";\n    if (dynamicProps) {\n      return (\"_d(\" + staticProps + \",[\" + (dynamicProps.slice(0, -1)) + \"])\")\n    } else {\n      return staticProps\n    }\n  }\n\n  // #3895, #4268\n  function transformSpecialNewlines (text) {\n    return text\n      .replace(/\\u2028/g, '\\\\u2028')\n      .replace(/\\u2029/g, '\\\\u2029')\n  }\n\n  /*  */\n\n\n\n  // these keywords should not appear inside expressions, but operators like\n  // typeof, instanceof and in are allowed\n  var prohibitedKeywordRE = new RegExp('\\\\b' + (\n    'do,if,for,let,new,try,var,case,else,with,await,break,catch,class,const,' +\n    'super,throw,while,yield,delete,export,import,return,switch,default,' +\n    'extends,finally,continue,debugger,function,arguments'\n  ).split(',').join('\\\\b|\\\\b') + '\\\\b');\n\n  // these unary operators should not be used as property/method names\n  var unaryOperatorsRE = new RegExp('\\\\b' + (\n    'delete,typeof,void'\n  ).split(',').join('\\\\s*\\\\([^\\\\)]*\\\\)|\\\\b') + '\\\\s*\\\\([^\\\\)]*\\\\)');\n\n  // strip strings in expressions\n  var stripStringRE = /'(?:[^'\\\\]|\\\\.)*'|\"(?:[^\"\\\\]|\\\\.)*\"|`(?:[^`\\\\]|\\\\.)*\\$\\{|\\}(?:[^`\\\\]|\\\\.)*`|`(?:[^`\\\\]|\\\\.)*`/g;\n\n  // detect problematic expressions in a template\n  function detectErrors (ast, warn) {\n    if (ast) {\n      checkNode(ast, warn);\n    }\n  }\n\n  function checkNode (node, warn) {\n    if (node.type === 1) {\n      for (var name in node.attrsMap) {\n        if (dirRE.test(name)) {\n          var value = node.attrsMap[name];\n          if (value) {\n            var range = node.rawAttrsMap[name];\n            if (name === 'v-for') {\n              checkFor(node, (\"v-for=\\\"\" + value + \"\\\"\"), warn, range);\n            } else if (name === 'v-slot' || name[0] === '#') {\n              checkFunctionParameterExpression(value, (name + \"=\\\"\" + value + \"\\\"\"), warn, range);\n            } else if (onRE.test(name)) {\n              checkEvent(value, (name + \"=\\\"\" + value + \"\\\"\"), warn, range);\n            } else {\n              checkExpression(value, (name + \"=\\\"\" + value + \"\\\"\"), warn, range);\n            }\n          }\n        }\n      }\n      if (node.children) {\n        for (var i = 0; i < node.children.length; i++) {\n          checkNode(node.children[i], warn);\n        }\n      }\n    } else if (node.type === 2) {\n      checkExpression(node.expression, node.text, warn, node);\n    }\n  }\n\n  function checkEvent (exp, text, warn, range) {\n    var stripped = exp.replace(stripStringRE, '');\n    var keywordMatch = stripped.match(unaryOperatorsRE);\n    if (keywordMatch && stripped.charAt(keywordMatch.index - 1) !== '$') {\n      warn(\n        \"avoid using JavaScript unary operator as property name: \" +\n        \"\\\"\" + (keywordMatch[0]) + \"\\\" in expression \" + (text.trim()),\n        range\n      );\n    }\n    checkExpression(exp, text, warn, range);\n  }\n\n  function checkFor (node, text, warn, range) {\n    checkExpression(node.for || '', text, warn, range);\n    checkIdentifier(node.alias, 'v-for alias', text, warn, range);\n    checkIdentifier(node.iterator1, 'v-for iterator', text, warn, range);\n    checkIdentifier(node.iterator2, 'v-for iterator', text, warn, range);\n  }\n\n  function checkIdentifier (\n    ident,\n    type,\n    text,\n    warn,\n    range\n  ) {\n    if (typeof ident === 'string') {\n      try {\n        new Function((\"var \" + ident + \"=_\"));\n      } catch (e) {\n        warn((\"invalid \" + type + \" \\\"\" + ident + \"\\\" in expression: \" + (text.trim())), range);\n      }\n    }\n  }\n\n  function checkExpression (exp, text, warn, range) {\n    try {\n      new Function((\"return \" + exp));\n    } catch (e) {\n      var keywordMatch = exp.replace(stripStringRE, '').match(prohibitedKeywordRE);\n      if (keywordMatch) {\n        warn(\n          \"avoid using JavaScript keyword as property name: \" +\n          \"\\\"\" + (keywordMatch[0]) + \"\\\"\\n  Raw expression: \" + (text.trim()),\n          range\n        );\n      } else {\n        warn(\n          \"invalid expression: \" + (e.message) + \" in\\n\\n\" +\n          \"    \" + exp + \"\\n\\n\" +\n          \"  Raw expression: \" + (text.trim()) + \"\\n\",\n          range\n        );\n      }\n    }\n  }\n\n  function checkFunctionParameterExpression (exp, text, warn, range) {\n    try {\n      new Function(exp, '');\n    } catch (e) {\n      warn(\n        \"invalid function parameter expression: \" + (e.message) + \" in\\n\\n\" +\n        \"    \" + exp + \"\\n\\n\" +\n        \"  Raw expression: \" + (text.trim()) + \"\\n\",\n        range\n      );\n    }\n  }\n\n  /*  */\n\n  var range = 2;\n\n  function generateCodeFrame (\n    source,\n    start,\n    end\n  ) {\n    if ( start === void 0 ) start = 0;\n    if ( end === void 0 ) end = source.length;\n\n    var lines = source.split(/\\r?\\n/);\n    var count = 0;\n    var res = [];\n    for (var i = 0; i < lines.length; i++) {\n      count += lines[i].length + 1;\n      if (count >= start) {\n        for (var j = i - range; j <= i + range || end > count; j++) {\n          if (j < 0 || j >= lines.length) { continue }\n          res.push((\"\" + (j + 1) + (repeat$1(\" \", 3 - String(j + 1).length)) + \"|  \" + (lines[j])));\n          var lineLength = lines[j].length;\n          if (j === i) {\n            // push underline\n            var pad = start - (count - lineLength) + 1;\n            var length = end > count ? lineLength - pad : end - start;\n            res.push(\"   |  \" + repeat$1(\" \", pad) + repeat$1(\"^\", length));\n          } else if (j > i) {\n            if (end > count) {\n              var length$1 = Math.min(end - count, lineLength);\n              res.push(\"   |  \" + repeat$1(\"^\", length$1));\n            }\n            count += lineLength + 1;\n          }\n        }\n        break\n      }\n    }\n    return res.join('\\n')\n  }\n\n  function repeat$1 (str, n) {\n    var result = '';\n    if (n > 0) {\n      while (true) { // eslint-disable-line\n        if (n & 1) { result += str; }\n        n >>>= 1;\n        if (n <= 0) { break }\n        str += str;\n      }\n    }\n    return result\n  }\n\n  /*  */\n\n\n\n  function createFunction (code, errors) {\n    try {\n      return new Function(code)\n    } catch (err) {\n      errors.push({ err: err, code: code });\n      return noop\n    }\n  }\n\n  function createCompileToFunctionFn (compile) {\n    var cache = Object.create(null);\n\n    return function compileToFunctions (\n      template,\n      options,\n      vm\n    ) {\n      options = extend({}, options);\n      var warn$$1 = options.warn || warn;\n      delete options.warn;\n\n      /* istanbul ignore if */\n      {\n        // detect possible CSP restriction\n        try {\n          new Function('return 1');\n        } catch (e) {\n          if (e.toString().match(/unsafe-eval|CSP/)) {\n            warn$$1(\n              'It seems you are using the standalone build of Vue.js in an ' +\n              'environment with Content Security Policy that prohibits unsafe-eval. ' +\n              'The template compiler cannot work in this environment. Consider ' +\n              'relaxing the policy to allow unsafe-eval or pre-compiling your ' +\n              'templates into render functions.'\n            );\n          }\n        }\n      }\n\n      // check cache\n      var key = options.delimiters\n        ? String(options.delimiters) + template\n        : template;\n      if (cache[key]) {\n        return cache[key]\n      }\n\n      // compile\n      var compiled = compile(template, options);\n\n      // check compilation errors/tips\n      {\n        if (compiled.errors && compiled.errors.length) {\n          if (options.outputSourceRange) {\n            compiled.errors.forEach(function (e) {\n              warn$$1(\n                \"Error compiling template:\\n\\n\" + (e.msg) + \"\\n\\n\" +\n                generateCodeFrame(template, e.start, e.end),\n                vm\n              );\n            });\n          } else {\n            warn$$1(\n              \"Error compiling template:\\n\\n\" + template + \"\\n\\n\" +\n              compiled.errors.map(function (e) { return (\"- \" + e); }).join('\\n') + '\\n',\n              vm\n            );\n          }\n        }\n        if (compiled.tips && compiled.tips.length) {\n          if (options.outputSourceRange) {\n            compiled.tips.forEach(function (e) { return tip(e.msg, vm); });\n          } else {\n            compiled.tips.forEach(function (msg) { return tip(msg, vm); });\n          }\n        }\n      }\n\n      // turn code into functions\n      var res = {};\n      var fnGenErrors = [];\n      res.render = createFunction(compiled.render, fnGenErrors);\n      res.staticRenderFns = compiled.staticRenderFns.map(function (code) {\n        return createFunction(code, fnGenErrors)\n      });\n\n      // check function generation errors.\n      // this should only happen if there is a bug in the compiler itself.\n      // mostly for codegen development use\n      /* istanbul ignore if */\n      {\n        if ((!compiled.errors || !compiled.errors.length) && fnGenErrors.length) {\n          warn$$1(\n            \"Failed to generate render function:\\n\\n\" +\n            fnGenErrors.map(function (ref) {\n              var err = ref.err;\n              var code = ref.code;\n\n              return ((err.toString()) + \" in\\n\\n\" + code + \"\\n\");\n          }).join('\\n'),\n            vm\n          );\n        }\n      }\n\n      return (cache[key] = res)\n    }\n  }\n\n  /*  */\n\n  function createCompilerCreator (baseCompile) {\n    return function createCompiler (baseOptions) {\n      function compile (\n        template,\n        options\n      ) {\n        var finalOptions = Object.create(baseOptions);\n        var errors = [];\n        var tips = [];\n\n        var warn = function (msg, range, tip) {\n          (tip ? tips : errors).push(msg);\n        };\n\n        if (options) {\n          if (options.outputSourceRange) {\n            // $flow-disable-line\n            var leadingSpaceLength = template.match(/^\\s*/)[0].length;\n\n            warn = function (msg, range, tip) {\n              var data = { msg: msg };\n              if (range) {\n                if (range.start != null) {\n                  data.start = range.start + leadingSpaceLength;\n                }\n                if (range.end != null) {\n                  data.end = range.end + leadingSpaceLength;\n                }\n              }\n              (tip ? tips : errors).push(data);\n            };\n          }\n          // merge custom modules\n          if (options.modules) {\n            finalOptions.modules =\n              (baseOptions.modules || []).concat(options.modules);\n          }\n          // merge custom directives\n          if (options.directives) {\n            finalOptions.directives = extend(\n              Object.create(baseOptions.directives || null),\n              options.directives\n            );\n          }\n          // copy other options\n          for (var key in options) {\n            if (key !== 'modules' && key !== 'directives') {\n              finalOptions[key] = options[key];\n            }\n          }\n        }\n\n        finalOptions.warn = warn;\n\n        var compiled = baseCompile(template.trim(), finalOptions);\n        {\n          detectErrors(compiled.ast, warn);\n        }\n        compiled.errors = errors;\n        compiled.tips = tips;\n        return compiled\n      }\n\n      return {\n        compile: compile,\n        compileToFunctions: createCompileToFunctionFn(compile)\n      }\n    }\n  }\n\n  /*  */\n\n  // `createCompilerCreator` allows creating compilers that use alternative\n  // parser/optimizer/codegen, e.g the SSR optimizing compiler.\n  // Here we just export a default compiler using the default parts.\n  var createCompiler = createCompilerCreator(function baseCompile (\n    template,\n    options\n  ) {\n    var ast = parse(template.trim(), options);\n    if (options.optimize !== false) {\n      optimize(ast, options);\n    }\n    var code = generate(ast, options);\n    return {\n      ast: ast,\n      render: code.render,\n      staticRenderFns: code.staticRenderFns\n    }\n  });\n\n  /*  */\n\n  var ref$1 = createCompiler(baseOptions);\n  var compile = ref$1.compile;\n  var compileToFunctions = ref$1.compileToFunctions;\n\n  /*  */\n\n  // check whether current browser encodes a char inside attribute values\n  var div;\n  function getShouldDecode (href) {\n    div = div || document.createElement('div');\n    div.innerHTML = href ? \"<a href=\\\"\\n\\\"/>\" : \"<div a=\\\"\\n\\\"/>\";\n    return div.innerHTML.indexOf('&#10;') > 0\n  }\n\n  // #3663: IE encodes newlines inside attribute values while other browsers don't\n  var shouldDecodeNewlines = inBrowser ? getShouldDecode(false) : false;\n  // #6828: chrome encodes content in a[href]\n  var shouldDecodeNewlinesForHref = inBrowser ? getShouldDecode(true) : false;\n\n  /*  */\n\n  var idToTemplate = cached(function (id) {\n    var el = query(id);\n    return el && el.innerHTML\n  });\n\n  var mount = Vue.prototype.$mount;\n  Vue.prototype.$mount = function (\n    el,\n    hydrating\n  ) {\n    el = el && query(el);\n\n    /* istanbul ignore if */\n    if (el === document.body || el === document.documentElement) {\n      warn(\n        \"Do not mount Vue to <html> or <body> - mount to normal elements instead.\"\n      );\n      return this\n    }\n\n    var options = this.$options;\n    // resolve template/el and convert to render function\n    if (!options.render) {\n      var template = options.template;\n      if (template) {\n        if (typeof template === 'string') {\n          if (template.charAt(0) === '#') {\n            template = idToTemplate(template);\n            /* istanbul ignore if */\n            if (!template) {\n              warn(\n                (\"Template element not found or is empty: \" + (options.template)),\n                this\n              );\n            }\n          }\n        } else if (template.nodeType) {\n          template = template.innerHTML;\n        } else {\n          {\n            warn('invalid template option:' + template, this);\n          }\n          return this\n        }\n      } else if (el) {\n        template = getOuterHTML(el);\n      }\n      if (template) {\n        /* istanbul ignore if */\n        if (config.performance && mark) {\n          mark('compile');\n        }\n\n        var ref = compileToFunctions(template, {\n          outputSourceRange: \"development\" !== 'production',\n          shouldDecodeNewlines: shouldDecodeNewlines,\n          shouldDecodeNewlinesForHref: shouldDecodeNewlinesForHref,\n          delimiters: options.delimiters,\n          comments: options.comments\n        }, this);\n        var render = ref.render;\n        var staticRenderFns = ref.staticRenderFns;\n        options.render = render;\n        options.staticRenderFns = staticRenderFns;\n\n        /* istanbul ignore if */\n        if (config.performance && mark) {\n          mark('compile end');\n          measure((\"vue \" + (this._name) + \" compile\"), 'compile', 'compile end');\n        }\n      }\n    }\n    return mount.call(this, el, hydrating)\n  };\n\n  /**\n   * Get outerHTML of elements, taking care\n   * of SVG elements in IE as well.\n   */\n  function getOuterHTML (el) {\n    if (el.outerHTML) {\n      return el.outerHTML\n    } else {\n      var container = document.createElement('div');\n      container.appendChild(el.cloneNode(true));\n      return container.innerHTML\n    }\n  }\n\n  Vue.compile = compileToFunctions;\n\n  return Vue;\n\n}));\n\n/* WEBPACK VAR INJECTION */}.call(this, __webpack_require__(/*! (webpack)/buildin/global.js */ \"E:\\\\node安装\\\\node_modules\\\\webpack\\\\buildin\\\\global.js\"), __webpack_require__(/*! (webpack)/node_modules/_timers-browserify@2.0.11@timers-browserify/main.js */ \"E:\\\\node安装\\\\node_modules\\\\webpack\\\\node_modules\\\\_timers-browserify@2.0.11@timers-browserify\\\\main.js\").setImmediate))\n\n//# sourceURL=webpack:///./node_modules/_vue@2.6.11@vue/dist/vue.js?"
			);

			/***/
		}),

	/***/
	"E:\\node安装\\node_modules\\webpack\\buildin\\global.js":
		/*!***********************************!*\
		  !*** (webpack)/buildin/global.js ***!
		  \***********************************/
		/*! no static exports found */
		/***/
		(function(module, exports) {

			eval(
				"var g;\n\n// This works in non-strict mode\ng = (function() {\n\treturn this;\n})();\n\ntry {\n\t// This works if eval is allowed (see CSP)\n\tg = g || new Function(\"return this\")();\n} catch (e) {\n\t// This works if the window reference is available\n\tif (typeof window === \"object\") g = window;\n}\n\n// g can still be undefined, but nothing to do about it...\n// We return undefined, instead of nothing here, so it's\n// easier to handle this case. if(!global) { ...}\n\nmodule.exports = g;\n\n\n//# sourceURL=webpack:///(webpack)/buildin/global.js?"
			);

			/***/
		}),

	/***/
	"E:\\node安装\\node_modules\\webpack\\node_modules\\_process@0.11.10@process\\browser.js":
		/*!******************************************************************!*\
		  !*** (webpack)/node_modules/_process@0.11.10@process/browser.js ***!
		  \******************************************************************/
		/*! no static exports found */
		/***/
		(function(module, exports) {

			eval(
				"// shim for using process in browser\nvar process = module.exports = {};\n\n// cached from whatever global is present so that test runners that stub it\n// don't break things.  But we need to wrap it in a try catch in case it is\n// wrapped in strict mode code which doesn't define any globals.  It's inside a\n// function because try/catches deoptimize in certain engines.\n\nvar cachedSetTimeout;\nvar cachedClearTimeout;\n\nfunction defaultSetTimout() {\n    throw new Error('setTimeout has not been defined');\n}\nfunction defaultClearTimeout () {\n    throw new Error('clearTimeout has not been defined');\n}\n(function () {\n    try {\n        if (typeof setTimeout === 'function') {\n            cachedSetTimeout = setTimeout;\n        } else {\n            cachedSetTimeout = defaultSetTimout;\n        }\n    } catch (e) {\n        cachedSetTimeout = defaultSetTimout;\n    }\n    try {\n        if (typeof clearTimeout === 'function') {\n            cachedClearTimeout = clearTimeout;\n        } else {\n            cachedClearTimeout = defaultClearTimeout;\n        }\n    } catch (e) {\n        cachedClearTimeout = defaultClearTimeout;\n    }\n} ())\nfunction runTimeout(fun) {\n    if (cachedSetTimeout === setTimeout) {\n        //normal enviroments in sane situations\n        return setTimeout(fun, 0);\n    }\n    // if setTimeout wasn't available but was latter defined\n    if ((cachedSetTimeout === defaultSetTimout || !cachedSetTimeout) && setTimeout) {\n        cachedSetTimeout = setTimeout;\n        return setTimeout(fun, 0);\n    }\n    try {\n        // when when somebody has screwed with setTimeout but no I.E. maddness\n        return cachedSetTimeout(fun, 0);\n    } catch(e){\n        try {\n            // When we are in I.E. but the script has been evaled so I.E. doesn't trust the global object when called normally\n            return cachedSetTimeout.call(null, fun, 0);\n        } catch(e){\n            // same as above but when it's a version of I.E. that must have the global object for 'this', hopfully our context correct otherwise it will throw a global error\n            return cachedSetTimeout.call(this, fun, 0);\n        }\n    }\n\n\n}\nfunction runClearTimeout(marker) {\n    if (cachedClearTimeout === clearTimeout) {\n        //normal enviroments in sane situations\n        return clearTimeout(marker);\n    }\n    // if clearTimeout wasn't available but was latter defined\n    if ((cachedClearTimeout === defaultClearTimeout || !cachedClearTimeout) && clearTimeout) {\n        cachedClearTimeout = clearTimeout;\n        return clearTimeout(marker);\n    }\n    try {\n        // when when somebody has screwed with setTimeout but no I.E. maddness\n        return cachedClearTimeout(marker);\n    } catch (e){\n        try {\n            // When we are in I.E. but the script has been evaled so I.E. doesn't  trust the global object when called normally\n            return cachedClearTimeout.call(null, marker);\n        } catch (e){\n            // same as above but when it's a version of I.E. that must have the global object for 'this', hopfully our context correct otherwise it will throw a global error.\n            // Some versions of I.E. have different rules for clearTimeout vs setTimeout\n            return cachedClearTimeout.call(this, marker);\n        }\n    }\n\n\n\n}\nvar queue = [];\nvar draining = false;\nvar currentQueue;\nvar queueIndex = -1;\n\nfunction cleanUpNextTick() {\n    if (!draining || !currentQueue) {\n        return;\n    }\n    draining = false;\n    if (currentQueue.length) {\n        queue = currentQueue.concat(queue);\n    } else {\n        queueIndex = -1;\n    }\n    if (queue.length) {\n        drainQueue();\n    }\n}\n\nfunction drainQueue() {\n    if (draining) {\n        return;\n    }\n    var timeout = runTimeout(cleanUpNextTick);\n    draining = true;\n\n    var len = queue.length;\n    while(len) {\n        currentQueue = queue;\n        queue = [];\n        while (++queueIndex < len) {\n            if (currentQueue) {\n                currentQueue[queueIndex].run();\n            }\n        }\n        queueIndex = -1;\n        len = queue.length;\n    }\n    currentQueue = null;\n    draining = false;\n    runClearTimeout(timeout);\n}\n\nprocess.nextTick = function (fun) {\n    var args = new Array(arguments.length - 1);\n    if (arguments.length > 1) {\n        for (var i = 1; i < arguments.length; i++) {\n            args[i - 1] = arguments[i];\n        }\n    }\n    queue.push(new Item(fun, args));\n    if (queue.length === 1 && !draining) {\n        runTimeout(drainQueue);\n    }\n};\n\n// v8 likes predictible objects\nfunction Item(fun, array) {\n    this.fun = fun;\n    this.array = array;\n}\nItem.prototype.run = function () {\n    this.fun.apply(null, this.array);\n};\nprocess.title = 'browser';\nprocess.browser = true;\nprocess.env = {};\nprocess.argv = [];\nprocess.version = ''; // empty string to avoid regexp issues\nprocess.versions = {};\n\nfunction noop() {}\n\nprocess.on = noop;\nprocess.addListener = noop;\nprocess.once = noop;\nprocess.off = noop;\nprocess.removeListener = noop;\nprocess.removeAllListeners = noop;\nprocess.emit = noop;\nprocess.prependListener = noop;\nprocess.prependOnceListener = noop;\n\nprocess.listeners = function (name) { return [] }\n\nprocess.binding = function (name) {\n    throw new Error('process.binding is not supported');\n};\n\nprocess.cwd = function () { return '/' };\nprocess.chdir = function (dir) {\n    throw new Error('process.chdir is not supported');\n};\nprocess.umask = function() { return 0; };\n\n\n//# sourceURL=webpack:///(webpack)/node_modules/_process@0.11.10@process/browser.js?"
			);

			/***/
		}),

	/***/
	"E:\\node安装\\node_modules\\webpack\\node_modules\\_setimmediate@1.0.5@setimmediate\\setImmediate.js":
		/*!*******************************************************************************!*\
		  !*** (webpack)/node_modules/_setimmediate@1.0.5@setimmediate/setImmediate.js ***!
		  \*******************************************************************************/
		/*! no static exports found */
		/***/
		(function(module, exports, __webpack_require__) {

			eval(
				"/* WEBPACK VAR INJECTION */(function(global, process) {(function (global, undefined) {\n    \"use strict\";\n\n    if (global.setImmediate) {\n        return;\n    }\n\n    var nextHandle = 1; // Spec says greater than zero\n    var tasksByHandle = {};\n    var currentlyRunningATask = false;\n    var doc = global.document;\n    var registerImmediate;\n\n    function setImmediate(callback) {\n      // Callback can either be a function or a string\n      if (typeof callback !== \"function\") {\n        callback = new Function(\"\" + callback);\n      }\n      // Copy function arguments\n      var args = new Array(arguments.length - 1);\n      for (var i = 0; i < args.length; i++) {\n          args[i] = arguments[i + 1];\n      }\n      // Store and register the task\n      var task = { callback: callback, args: args };\n      tasksByHandle[nextHandle] = task;\n      registerImmediate(nextHandle);\n      return nextHandle++;\n    }\n\n    function clearImmediate(handle) {\n        delete tasksByHandle[handle];\n    }\n\n    function run(task) {\n        var callback = task.callback;\n        var args = task.args;\n        switch (args.length) {\n        case 0:\n            callback();\n            break;\n        case 1:\n            callback(args[0]);\n            break;\n        case 2:\n            callback(args[0], args[1]);\n            break;\n        case 3:\n            callback(args[0], args[1], args[2]);\n            break;\n        default:\n            callback.apply(undefined, args);\n            break;\n        }\n    }\n\n    function runIfPresent(handle) {\n        // From the spec: \"Wait until any invocations of this algorithm started before this one have completed.\"\n        // So if we're currently running a task, we'll need to delay this invocation.\n        if (currentlyRunningATask) {\n            // Delay by doing a setTimeout. setImmediate was tried instead, but in Firefox 7 it generated a\n            // \"too much recursion\" error.\n            setTimeout(runIfPresent, 0, handle);\n        } else {\n            var task = tasksByHandle[handle];\n            if (task) {\n                currentlyRunningATask = true;\n                try {\n                    run(task);\n                } finally {\n                    clearImmediate(handle);\n                    currentlyRunningATask = false;\n                }\n            }\n        }\n    }\n\n    function installNextTickImplementation() {\n        registerImmediate = function(handle) {\n            process.nextTick(function () { runIfPresent(handle); });\n        };\n    }\n\n    function canUsePostMessage() {\n        // The test against `importScripts` prevents this implementation from being installed inside a web worker,\n        // where `global.postMessage` means something completely different and can't be used for this purpose.\n        if (global.postMessage && !global.importScripts) {\n            var postMessageIsAsynchronous = true;\n            var oldOnMessage = global.onmessage;\n            global.onmessage = function() {\n                postMessageIsAsynchronous = false;\n            };\n            global.postMessage(\"\", \"*\");\n            global.onmessage = oldOnMessage;\n            return postMessageIsAsynchronous;\n        }\n    }\n\n    function installPostMessageImplementation() {\n        // Installs an event handler on `global` for the `message` event: see\n        // * https://developer.mozilla.org/en/DOM/window.postMessage\n        // * http://www.whatwg.org/specs/web-apps/current-work/multipage/comms.html#crossDocumentMessages\n\n        var messagePrefix = \"setImmediate$\" + Math.random() + \"$\";\n        var onGlobalMessage = function(event) {\n            if (event.source === global &&\n                typeof event.data === \"string\" &&\n                event.data.indexOf(messagePrefix) === 0) {\n                runIfPresent(+event.data.slice(messagePrefix.length));\n            }\n        };\n\n        if (global.addEventListener) {\n            global.addEventListener(\"message\", onGlobalMessage, false);\n        } else {\n            global.attachEvent(\"onmessage\", onGlobalMessage);\n        }\n\n        registerImmediate = function(handle) {\n            global.postMessage(messagePrefix + handle, \"*\");\n        };\n    }\n\n    function installMessageChannelImplementation() {\n        var channel = new MessageChannel();\n        channel.port1.onmessage = function(event) {\n            var handle = event.data;\n            runIfPresent(handle);\n        };\n\n        registerImmediate = function(handle) {\n            channel.port2.postMessage(handle);\n        };\n    }\n\n    function installReadyStateChangeImplementation() {\n        var html = doc.documentElement;\n        registerImmediate = function(handle) {\n            // Create a <script> element; its readystatechange event will be fired asynchronously once it is inserted\n            // into the document. Do so, thus queuing up the task. Remember to clean up once it's been called.\n            var script = doc.createElement(\"script\");\n            script.onreadystatechange = function () {\n                runIfPresent(handle);\n                script.onreadystatechange = null;\n                html.removeChild(script);\n                script = null;\n            };\n            html.appendChild(script);\n        };\n    }\n\n    function installSetTimeoutImplementation() {\n        registerImmediate = function(handle) {\n            setTimeout(runIfPresent, 0, handle);\n        };\n    }\n\n    // If supported, we should attach to the prototype of global, since that is where setTimeout et al. live.\n    var attachTo = Object.getPrototypeOf && Object.getPrototypeOf(global);\n    attachTo = attachTo && attachTo.setTimeout ? attachTo : global;\n\n    // Don't get fooled by e.g. browserify environments.\n    if ({}.toString.call(global.process) === \"[object process]\") {\n        // For Node.js before 0.9\n        installNextTickImplementation();\n\n    } else if (canUsePostMessage()) {\n        // For non-IE10 modern browsers\n        installPostMessageImplementation();\n\n    } else if (global.MessageChannel) {\n        // For web workers, where supported\n        installMessageChannelImplementation();\n\n    } else if (doc && \"onreadystatechange\" in doc.createElement(\"script\")) {\n        // For IE 6–8\n        installReadyStateChangeImplementation();\n\n    } else {\n        // For older browsers\n        installSetTimeoutImplementation();\n    }\n\n    attachTo.setImmediate = setImmediate;\n    attachTo.clearImmediate = clearImmediate;\n}(typeof self === \"undefined\" ? typeof global === \"undefined\" ? this : global : self));\n\n/* WEBPACK VAR INJECTION */}.call(this, __webpack_require__(/*! ./../../buildin/global.js */ \"E:\\\\node安装\\\\node_modules\\\\webpack\\\\buildin\\\\global.js\"), __webpack_require__(/*! ./../_process@0.11.10@process/browser.js */ \"E:\\\\node安装\\\\node_modules\\\\webpack\\\\node_modules\\\\_process@0.11.10@process\\\\browser.js\")))\n\n//# sourceURL=webpack:///(webpack)/node_modules/_setimmediate@1.0.5@setimmediate/setImmediate.js?"
			);

			/***/
		}),

	/***/
	"E:\\node安装\\node_modules\\webpack\\node_modules\\_timers-browserify@2.0.11@timers-browserify\\main.js":
		/*!**********************************************************************************!*\
		  !*** (webpack)/node_modules/_timers-browserify@2.0.11@timers-browserify/main.js ***!
		  \**********************************************************************************/
		/*! no static exports found */
		/***/
		(function(module, exports, __webpack_require__) {

			eval(
				"/* WEBPACK VAR INJECTION */(function(global) {var scope = (typeof global !== \"undefined\" && global) ||\n            (typeof self !== \"undefined\" && self) ||\n            window;\nvar apply = Function.prototype.apply;\n\n// DOM APIs, for completeness\n\nexports.setTimeout = function() {\n  return new Timeout(apply.call(setTimeout, scope, arguments), clearTimeout);\n};\nexports.setInterval = function() {\n  return new Timeout(apply.call(setInterval, scope, arguments), clearInterval);\n};\nexports.clearTimeout =\nexports.clearInterval = function(timeout) {\n  if (timeout) {\n    timeout.close();\n  }\n};\n\nfunction Timeout(id, clearFn) {\n  this._id = id;\n  this._clearFn = clearFn;\n}\nTimeout.prototype.unref = Timeout.prototype.ref = function() {};\nTimeout.prototype.close = function() {\n  this._clearFn.call(scope, this._id);\n};\n\n// Does not start the time, just sets up the members needed.\nexports.enroll = function(item, msecs) {\n  clearTimeout(item._idleTimeoutId);\n  item._idleTimeout = msecs;\n};\n\nexports.unenroll = function(item) {\n  clearTimeout(item._idleTimeoutId);\n  item._idleTimeout = -1;\n};\n\nexports._unrefActive = exports.active = function(item) {\n  clearTimeout(item._idleTimeoutId);\n\n  var msecs = item._idleTimeout;\n  if (msecs >= 0) {\n    item._idleTimeoutId = setTimeout(function onTimeout() {\n      if (item._onTimeout)\n        item._onTimeout();\n    }, msecs);\n  }\n};\n\n// setimmediate attaches itself to the global object\n__webpack_require__(/*! setimmediate */ \"E:\\\\node安装\\\\node_modules\\\\webpack\\\\node_modules\\\\_setimmediate@1.0.5@setimmediate\\\\setImmediate.js\");\n// On some exotic environments, it's not clear which object `setimmediate` was\n// able to install onto.  Search each possibility in the same order as the\n// `setimmediate` library.\nexports.setImmediate = (typeof self !== \"undefined\" && self.setImmediate) ||\n                       (typeof global !== \"undefined\" && global.setImmediate) ||\n                       (this && this.setImmediate);\nexports.clearImmediate = (typeof self !== \"undefined\" && self.clearImmediate) ||\n                         (typeof global !== \"undefined\" && global.clearImmediate) ||\n                         (this && this.clearImmediate);\n\n/* WEBPACK VAR INJECTION */}.call(this, __webpack_require__(/*! ./../../buildin/global.js */ \"E:\\\\node安装\\\\node_modules\\\\webpack\\\\buildin\\\\global.js\")))\n\n//# sourceURL=webpack:///(webpack)/node_modules/_timers-browserify@2.0.11@timers-browserify/main.js?"
			);

			/***/
		})

	/******/
});

```

关于setimmediate介绍链接：

http://www.ruanyifeng.com/blog/2014/10/event-loop.html



#### webpack打包模块的源码 执行顺序

- 1:把所有模块的代码放入到函数中，用一个数组保存起来
- 2:根据require时传入的数组索引，能知道需要哪一段代码
- 3:从数组中，根据索引取出包含我们代码的函数
- 4:执行该函数，传入一个对象 module.exports
- 5:我们的代码，按照约定，正好是用module.exports = 'xxxx' 进行赋值
- 6:调用函数结束后，module.exports从原来的空对象，就有值了
- 7:最终return module.exports; 作为require函数的返回值

#### webpack.config.js文件配置

- ###### entry 是一个对象，程序的入口

  - key:随意写
  - value: 入口文件

- ###### output 是一个对象,产出的资源

  - key: filename
  - value : 生成的build.js

- ###### module 模块（对象）

  - loaders:[]
    - 存在一些loader   `{ test:正则,loader:'style-loader!css-loader'    }

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401183220953.png" alt="image-20200401183220953" style="zoom:80%;" />

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401183138406.png" alt="image-20200401183138406" style="zoom:80%;" />

#### 配置文件webpack.config.js的修改

修改配置文件名为:webpack.dev.config.js和webpack.prod.config.js

#### 在package.json文件中修改

```javascript
"scripts": {
     "dev": "webpack --config ./webpack.dev.config.js",
     "prod": "webpack --config ./webpack.prod.config.js"

}
```



### css文件处理

#### es6模块导入

```javascript
import './main.css'
```

#### 编译之后报错

![image-20200401184528866](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401184528866.png)

对于webpack来说，css文件也是一个模块，但是像这样的文件，webpack得需要loaders去处理这些文件

#### 下载并配置

```npm i css-loader style-loader -D	```

```javascript
module:{
		loaders:[
			{	
				// 遇到后缀为.css的文件，webpack先用css-loader加载器去解析这个文件
				// 最后计算完的css，将会使用style-loader生成一个内容为最终解析完的css代码的style标签，放到head标签里。
				// webpack在打包过程中，遇到后缀为css的文件，就会使用style-loader和css-loader去加载这个文件。
				test:/\.css$/,
				loader:'style-loader!css-loader'
			}
            ]
}
```

### 图片文件的处理

#### App.js 导入图片资源

```javascript
import imgSrc from './myGirl.jpg'

export default{
	template:`
		<div>
			<img :src="imgSrc" alt="" />
		</div>
	`,
	data(){
		return {
			imgSrc:imgSrc
		}
	}
};
```

对文件的处理，webpack得需要```url-loader```和```file-loader```

#### 下载处理图片的loader模块

```npm i url-loader file-loader -D```



#### 添加loader的配置

```javascript
module:{
		loaders:[
			{
				test:/\.css$/,
				loader:'style-loader!css-loader'
			},
			{
				test:/\.(jpg|png|jpeg|gif|svg)$/,
				loader:'url-loader?limit=4000'	// limit如果小于4000就会生成base64编码的图片
			}
		]
	},
```

```javascript
webpack最终会将各个模块打包成一个文件，因此我们样式中的url路径是相对入口html页面的，而不是相对于原始css文件所在的路径的。这就会导致图片引入失败。这个问题是用file-loader解决的，file-loader可以解析项目中的url引入（不仅限于css），根据我们的配置，将图片拷贝到相应的路径，再根据我们的配置，修改打包后文件引用路径，使之指向正确的文件。
简易,对于图片的大小小于limit设置的大小，使用base64编码，可以减少一次图片的网络请求；那么对于比较大的图片,使用base64就不适合了，编码会和html混在一起，一方面可读性差，另一方面加大了html页面的大小，反而加大了下载页面的大小，得不偿失了呢,因此设置一个合理的limit是非常有必要的。
```

### html-webpack-plugin插件的使用

#### 下载模块

```npm i html-webpack-plugin --save-dev```

#### webpack.config.js文件配置

```javascript
const path = require('path');
//2.导入模块
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
	// 入口
	entry:{
		// 可以有多个入口，也可以有一个，如果一个，就默认从这一个入口开始分析
		 "main" : './src/main.js'
	},
	output:{
		// 指定产出的目录
		path: path.resolve('./dist'), //相对转绝对
		filename:'build.js'
	},
	// 声明模块
	// 包含各个loader
	module:{
		loaders:[
			{	
				// 遇到后缀为.css的文件，webpack先用css-loader加载器去解析这个文件
				// 最后计算完的css，将会使用style-loader生成一个内容为最终解析完的css代码的style标签，放到head标签里。
				// webpack在打包过程中，遇到后缀为css的文件，就会使用style-loader和css-loader去加载这个文件。
				test:/\.css$/,
				loader:'style-loader!css-loader'
			},
			{
				test:/\.(jpg|png|jpeg|gif|svg)$/,
				loader:'url-loader?limit=100000'
			},
			{
				test:/\.less$/,
				loader:'style-loader!css-loader!less-loader'
			}
		]
	},
	watch:true, //文件监视改动 自动产生build.js
    //添加插件 
	plugins:[
		new HtmlWebpackPlugin({
			//插件的执行运行与元素索引有关
			templat:'./src/index.html', //参照物
		})
	]
}
```



#### CommonsChunkPlugin的使用

> CommonsChunkPlugin主要是用来提取第三方库和公共模块，避免首屏加载的bundle文件或者按需加载的bundle文件体积过大，从而导致加载时间过长，着实是优化的一把利器.

#### chunk的分类

- webpack当中配置的入口文件(entry)是chunk，可以理解为entry chunk
- 入口文件以及它的依赖文件通过code splite(代码分割) 出来的也是chunk，可以理解为children chunk
- 通过CommonsChunkPlugin创建出来的文件也是chunk，可以理解为commons chunk



#### CommonsChunkPlugin可配置的属性

- name：可以是已经存在的chunk（一般指入口文件）对应的name，那么就会把公共模块代码合并到这个chunk上；否则，会创建名字为name的commons chunk进行合并
- filename：指定commons chunk的文件名
- chunks：指定source chunk，即指定从哪些chunk当中去找公共模块，省略该选项的时候，默认就是entry chunks
- minChunks：既可以是数字，也可以是函数，还可以是Infinity，具体用法和区别下面会说



### 验证三种情况

- 不分离出第三方库和自定义公共模块
- 分离出第三方库、自定义公共模块、webpack运行文件，但它们在同一个文件中
- 单独分离第三方库、自定义公共模块、webpack运行文件，各自在不同文件

#### 不分离出第三方库和自定义公共模块

不分离出第三方库和自定义公共模板：

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401203904887.png" alt="image-20200401203904887" style="zoom:50%;" />

src目录下各个文件内容，尽量保持简单：

```javascript
--common.js
	export const common = 'common file';
--main1.js
	import {common} from './common.js'
    import Vue from 'vue'
    console.log(Vue,`main1 ${common}`);
--main2.js
	import {common} from './common.js'
    import Vue from 'vue'
    console.log(Vue,`main1 ${common}`)
```

webpack.config.js

```javascript
const path  = require('path');
module.exports = {
	// 入口
	entry:{
		// 可以有多个入口，也可以有一个，如果有一个就默认从这一个入口开始分析
		"main1":'./src/main1.js',
		"main2":'./src/main2.js'
	},
	output:{
		path:path.resolve('./dist'),//相对转绝对
		filename:'[name].js'
	},
	watch:true,//文件监视改动 自动产出build.js
}
```

执行命令npm run build

问题：**查看main1.js和main2.js，会发现共同引用的common.js文件和vue都被打包进去了，这肯定不合理，公共模块重复打包，体积过大。**

#### 分离出第三方库、自定义公共模块、webpack运行文件

修改webpack.config.js新增一个入口文件vendor和CommonsChunkPlugin插件进行公共模块的提取：

```javascript
const path = require('path');
const webpack = require('webpack');
const packagejson = require('./package.json');
module.exports = {
    // 入口
    entry: {
        "main1": './src/main1.js',
        "main2": './src/main2.js',
        "vendor": Object.keys(packagejson.dependencies) //获取生产环境依赖的库
    },
    //出口
    output: {
        path: path.resolve('./dist'), //相对转绝对
        filename: '[name].js'
    },
    watch: true, //文件监视改动 自动产出build.js
    plugins: [
        new webpack.optimize.CommonsChunkPlugin({
            name: ['vendor'],
            filename: '[name].js'
        })
    ]
}
```

查看dist目录，新增了一个vendor.js的文件

打包信息：

通过查看vendor.js文件，发现main1.js和main2.js文件中依赖的vue和common.js都被打包进vendor.js中，同时还有webpack的运行文件。总的来说，我们初步的目的达到，提取公共模块，但是它们都在同一个文件中。

到这里，肯定有人希望自家的vendor.js纯白无瑕，只包含第三方库，不包含自定义的公共模块和webpack运行文件，又或者希望包含第三方库和公共模块，不包含webpack运行文件。

其实，这种想法是对，特别是分离出webpack运行文件，因为每次打包webpack运行文件都会变，如果你不分离出webpack运行文件，每次打包生成vendor.js对应的哈希值都会变化，导致vendor.js改变，但实际上你的第三方库其实是没有变，然而浏览器会认为你原来缓存的vendor.js就失效，要重新去服务器中获取，其实只是webpack运行文件变化而已，就要人家重新加载，好冤啊~

#### 单独分离出第三方库、自定义公共模块、webpack运行文件

这里我们分两步走：

1. 先单独抽离出webpack运行文件
2. 接着单独抽离第三方库和自定义公共模块

**（1）抽离webpack的运行文件**

修改webpack配置文件

```javascript
 plugins: [
        new webpack.optimize.CommonsChunkPlugin({
            name: ['vendor', 'runtime'],
            filename: '[name].js',
        })
```

其实上面这段代码，等价于下面这段：

```javascript
 plugins: [
        new webpack.optimize.CommonsChunkPlugin({
            name: 'vendor',
            filename: '[name].js'
        }),
        new webpack.optimize.CommonsChunkPlugin({
            name: 'runtime',
            filename: '[name].js',
            chunks: ['vendor']
        }),
    ]
```

上面两段抽离webpack运行文件代码的意思是创建一个名为runtime的commons chunk进行webpack运行文件的抽离，其中source chunks是vendor.js。

查看dist目录下，新增了一个runtime.js的文件，其实就是webpack的运行文件



再来查看一下命令行中webpack的打包信息，你会发现vendor.js的体积已经减小，说明已经把webpack运行文件提取出来了：

![image-20180924224404680](/var/folders/7b/sz6pt5jd3y3b51q1ngm_8pph0000gn/T/abnerworks.Typora/image-20180924224404680.png)

可是，vendor.js中还有自定义的公共模块common.js，人家只想vendor.js拥有项目依赖的第三方库而已（这里是jquery），这个时候把minChunks这个属性引进来。

minChunks可以设置为数字、函数和Infinity，**默认值是2，并不是官方文档说的入口文件的数量**，下面解释下minChunks含义：

- 数字：模块被多少个chunk公共引用才被抽取出来成为commons chunk
- 函数：接受 (module, count) 两个参数，返回一个布尔值，你可以在函数内进行你规定好的逻辑来决定某个模块是否提取成为commons chunk
- Infinity：**只有当入口文件（entry chunks） >= 3 才生效，用来在第三方库中分离自定义的公共模块**

**(2) 抽离第三方库和自定义公共模块**

minChunks设为Infinity，修改webpack配置文件如下

```javascript
plugins: [
        new webpack.optimize.CommonsChunkPlugin({
            name: ['vendor','runtime'],
            filename: '[name].js',
            minChunks: Infinity
        }),
        new webpack.optimize.CommonsChunkPlugin({
            name: 'common',
            filename: '[name].js',
            chunks: ['main1','main2']//从first.js和second.js中抽取commons chunk
        }),
    ]
```

查看dist目录下，新增了一个common.js的文件：

![image-20180924225354427](/var/folders/7b/sz6pt5jd3y3b51q1ngm_8pph0000gn/T/abnerworks.Typora/image-20180924225354427.png)

再来查看一下命令行中webpack的打包信息，自定义的公共模块分离出来：

![image-20180924225428549](/var/folders/7b/sz6pt5jd3y3b51q1ngm_8pph0000gn/T/abnerworks.Typora/image-20180924225428549.png)

这时候的vendor.js就纯白无瑕，只包含第三方库文件，common.js就是自定义的公共模块，runtime.js就是webpack的运行文件。

#### webpack异步加载的原理

webpack ensure 有人称它为异步加载，也有人说做代码切割。其实说白了，它就是把js模块给独立导出一个.js文件的，然后使用这个 模块的时候，webpack会构造script dom元素，由浏览器发起异步请求这个js文件。

webpack.ensure的原理：

它就是 **把一些js模块给独立出一个个js文件，然后需要用到的时候，在创建一个script对象，加入 到document.head对象中即可**，浏览器会自动帮我们发起请求，去请求这个js文件，在写个回调，去 定义得到这个js文件后，需要做什么业务逻辑操作。

main.js依赖三个js

- A.js是封装aBtn按钮点击后，才执行的业务逻辑
- B.js是封装bBtn按钮点击后，才执行的业务逻辑
- vue.js是封装了main.js需要利用的包



针对上面的需求，**优化方案**

 假设 A.js B.js   vue.js都是非常大的文件 因为 A.js B.js  都不是main.js必须有的，即未来可能发生的操作，那么我们把 他们利用异步加载，当发生的时候再去加载就行了

vue.js.js是main.js立即马上依赖的工具箱。但是它又非常的大，所以将其配置打包成一个公共模块， 利用浏览器的并发加载，加快下载速度。ok,构思完成，开始实现。

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
</head>
<body>
	<div id="app"></div>
	<button id="aBtn">Abtn</button>
	<br>
	<button id="bBtn">Bbtn</button>
	
</body>
</html>
```

定义了两个button

然后看看 main.js

```javascript
import Vue from 'vue'
console.log(Vue);
document.getElementById('aBtn').onclick = function(){
	require.ensure(['./B.js'],function(){
		var A = require('./A.js');
		alert(A.data);
		//异步里面再导入同步模块--实际是使用同步中的模块
		var Vue1 = require('vue');
	})
}
document.getElementById('bBtn').onclick = function(){
	require.ensure([],function(){

		var B = require('./B.js');
		alert(B.data);

	})
}
```

可以看到，A.js， B.js 都是点击后才ensure进来的。什么时候加载完成呢？ 就是 require.ensure() 第二个函数参数，即回调函数，它表示当下载js完成后，发生的。



### webpack-dev-server

#### 下载模块

1.```npm install webpack-dev-server --save-dev```

常用配置参数

--open 自动打开浏览器

--hot 热更新 ，不在刷新的情况下替换 css样式

--inline  自动刷新

--port 9999 指定端口

--process 显示编译进度

#### 在package.json文件中配置

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401195248700.png" alt="image-20200401195248700" style="zoom:80%;" />

#### 直接执行 ```npm run dev```

### es6的解析

#### 模块介绍

```babel-core```:

`javascript babel-core的作用是把js代码分析成ast（抽象语法树），方便各个插件分析语法进行相应的处理。有些新语法在低版本 js 中是不存在的，如箭头函数，rest 参数，函数默认值等，这种语言层面的不兼容只能通过将代码转为 ast，分析其语法后再转为低版本 js`

abel转译器本身，提供了babel的转译API，如babel.transform等，用于对代码进行转译。像webpack的babel-loader就是调用这些API来完成转译过程的。

```babel-loader```:

在将es6的代码transform进行转义，就是通过babel-loader来完成	

```babel-preset-env```

如果要自行配置转译过程中使用的各类插件，那太痛苦了，所以babel官方帮我们做了一些预设的插件集，称之为preset，这样我们只需要使用对应的preset就可以了。以JS标准为例，babel提供了如下的一些preset：

- es2015
- es2016
- es2017
- env
   es20xx的preset只转译该年份批准的标准，而env则代指最新的标准，包括了latest和es20xx各年份
   另外，还有 stage-0到stage-4的标准成形之前的各个阶段，这些都是实验版的preset，建议不要使用。

```babel-plugin-transform-runtime```

Babel 默认只转换新的 JavaScript 语法，而不转换新的 API。例如，Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise 等全局对象，以及一些定义在全局对象上的方法（比如 Object.assign）都不会转译。如果想使用这些新的对象和方法，必须使用 babel-polyfill，为当前环境提供一个垫片。

参考链接：https://segmentfault.com/q/1010000005596587?from=singlemessage&isappinstalled=1 看这个回答，说的非常详细。

#### 安装模块

```npm install babel-core babel-loader babel-preset-env babel-plugin-transform-runtime -D``` 

#### 在webpack-dev-config.js配置

```javascript
loader:[
    {
		// 处理es6,7,8
		test:/\.js$/,
		loader:'babel-loader',
		options:{
			presets:['env'],//处理关键字
			plugins:['transform-runtime'],//处理函数
		}
    }
]
```

配置完成之后执行 ```npm run dev```

发现！！！！！

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401200523200.png" alt="image-20200401200523200" style="zoom:80%;" />

解决：

排除不包含node_modules的路径，然后再配置文件中修改

```javascript
loader:[
    {
		// 处理es6,7,8
		test:/\.js$/,
		loader:'babel-loader',
        exclude:/node_modules/,	//排除不包含node_modules的路径
		options:{
			presets:['env'],//处理关键字
			plugins:['transform-runtime'],//处理函数
		}
    }
]
```

也会发现，当排除掉node_modules文件中的es6代码编译后，编译的时间也快了
以前出错的，3601毫秒的时候就开始出错了。。。。

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401200754159.png" alt="image-20200401200754159" style="zoom:80%;" />

排除掉node_modules之后

![image-20200401200629532](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200401200629532.png)



### 单文件引入

#### 下载包

注：-D代表下载的文件存在dev里面（-D开发依赖）(-S项目依赖)

```npm install vue-loader@14.1.1 vue-template-compiler@2.5.17 -D```

#### 创建App.vue文件

```javascript
//组件的模板结构
<template>
	<div>
		{{ text }}
	</div>
</template>

//组件的业务逻辑
<script>
export default {
	data(){
		return {
			text:'hello Single file'				
		}
	}
}
</script>
//组件的样式
<style>
	body{
		background-color: green;
	}
</style>
```

#### 创建入口文件main.js

```javascript
import Vue from 'vue';
import App from './App'
new Vue({
	el:'#app',
	//Render函数是Vue2.x版本新增的一个函数；
	// 使用虚拟dom来渲染节点提升性能，因为它是基于JavaScript计算。
	// 通过使用createElement(h)来创建dom节点。createElement是render的核心方法。其Vue编译的时候会把template里面的节点解析成虚拟dom；
	render:c=>c(App)
	// components:{
	//  	App
	// },
	// template:`<App />`
});

```

#### webpack.dev.config.js文件配置

```javascript
// 处理Vue文件
{
	test:/\.vue$/,
	loader:'vue-loader'
}
```

# vue-cli脚手架

## v-for中key的作用

#### 1.当数据发生变化时，vue是怎样更新节点的？

要知道渲染真实DOM的开销是很大的，比如有时候我们修改了某个数据，如果直接渲染到真实dom上会引起整个dom树的重绘和重排，有没有可能我们只更新我们修改的那一小块dom而不要更新整个dom呢？diff算法能够帮助我们。

我们先根据真实DOM生成一颗`virtual DOM`，当`virtual DOM`某个节点的数据改变后会生成一个新的`Vnode`，然后`Vnode`和`oldVnode`作对比，发现有不一样的地方就直接修改在真实的DOM上，然后使`oldVnode`的值为`Vnode`。

diff的过程就是调用名为`patch`的函数，比较新旧节点，一边比较一边给**真实的DOM**打补丁。

#### 2.virtual DOM和真实DOM的区别

virtual DOM是将真实的DOM的数据抽取出来，以对象的形式模拟树形结构。比如dom是这样的：

```javascript
<div>
    <p>123</p>
</div>
```

对应的virtual DOM（伪代码）：

```javascript
var Vnode = {
    tag: 'div',
    children: [
        { tag: 'p', text: '123' }
    ]
};
```



#### 3.diff的比较方式

在采取diff算法比较新旧节点的时候，比较只会在同层级进行, 不会跨层级比较。

```javascript
<div>
    <p>123</p>
</div>

<div>
    <span>456</span>
</div>
```



大家要知道，不仅只是vue中，react中在执行列表渲染时也会要求给每个组件添加key这个属性

如果想知道key的作用，不得我们得聊一下虚拟DOM的Diff算法



所谓虚拟DOM的诞生，使我们可以不直接操作DOM元素，只操作数据便可以重新渲染页面。而隐藏在背后的原理便是其高效的Diff算法，它的核心是基于两个简单的假设：

1. ###### 两个相同的组件产生类似的DOM结构，不同的组件产生不同的DOM结构

2. ###### 同一个层级的一组节点，他们可以通过唯一的id进行区分



下面这张图是Diff示意图：

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200402091440317.png" alt="image-20200402091440317" style="zoom:80%;" />

由此图我们可以看出：

当页面的数据发生变化时，Diff算法只会比较同一层级的节点：

###### 如果节点类型不同，直接干掉前面的节点，再创建并插入新的节点，不会再比较这个节点以后的子节点了

###### 如果节点类型相同，则会重新设置该节点的属性，从而实现节点的更新

当某一层有很多相同的界定时，也就是列表节点，Diff算法的更新过程默认情况下也是遵循以上原则

比如下面这个情况

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200402091756890.png" alt="image-20200402091756890" style="zoom:80%;" />![image-20200402092047097](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200402092047097.png)

我们希望可以在B和C之间加一个F,Diff算法默认 执行起来是这样的：

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200402092125706.png" alt="image-20200402092125706" style="zoom:80%;" />

既把C更新成F,D更新成C,E更新成D,最后再插入E,是不是很没有效率？



所有我们***需要使用key来给每个节点做一个唯一的标识，Diff算法就可以正确的识别此节点，找到正确的位置区插入新的节点***

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200402092854645.png" alt="image-20200402092854645" style="zoom:80%;" />

所以一句话，***key的作用主要是为了高效的更新虚拟DOM***。另外vue的在使用相同标签名元素的过渡切换时，也会使用到key属性，其目的也是为了让vue可以区分他们，否则vue只会替换其内部属性而不会触发过渡效果。

##### 深度剖析：如何实现一个Virtual DOM算法

所谓的 Virtual DOM 算法。包括几个步骤：

1. 用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中
2. 当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异
3. 把2所记录的差异应用到步骤1所构建的真正的DOM树上，视图就更新了

参考链接：https://github.com/livoras/blog/issues/13

总结：当给组件使用v-for遍历的时候，一定要加上：key属性，避免让vue去计算DOM

## $emit和$on进行组件之间的传值(bus)

> 注意：$emit和$on的事件必须在一个公共的实例上，才能够触发



需求：

	1.有A，B，C三个组件，同时挂载到入口组件中
	
	2.将A组件中的数据传递到C组件，再将B组件中的数据传递到C组件

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Vue2-单一事件管理组件通信</title>

  
</head>
<body>
  <div id="app">
    <dom-a></dom-a>
    <dom-b></dom-b>
    <dom-c></dom-c>   
  </div>
  <script src="vue.js"></script>
  <script>
    

  //准备一个空的实例对象
  var Event = new Vue();
  console.log(Event);
 
  //组件A
  var A = {
    template: `
      <div>
        <span>我是A组件的数据->{{a}}</span>
        <input type="button" value="把A数据传给C" @click = "send">
      </div>
    `,
    methods: {
      send () {
        alert(1);
        console.log(this);
        Event.$emit("a-msg", this.a);
      }
    },
    data () {
      return {
        a: "我是a组件中数据"
      }
    }
  };
  //组件B
  var B = {
    template: `
      <div>
        <span>我是B组件的数据->{{a}}</span>
        <input type="button" value="把B数据传给C" @click = "send">
      </div>
    `,
    methods: {
      send () {
        Event.$emit("b-msg", this.a);
      }
    },
    data () {
      return {
        a: "我是b组件中数据"
      }
    }
  };
  //组件C
  var C = {
    template: `
      <div>
        <h3>我是C组件</h3>
        <span>接收过来A的数据为: {{a}}</span>
        <br>
        <span>接收过来B的数据为: {{b}}</span>
      </div>
    `,
    mounted () {
      alert(2);
      //接收A组件的数据
      Event.$on("a-msg", (a)=> {
        this.a = a;
      });
 
      //接收B组件的数据
      Event.$on("b-msg",  (b)=> {
        this.b = b;
      });
    },
    data () {
      return {
        a: "",
        b: ""
      }
    }
  };

    new Vue({
      el: "#app",
      components: {
         'dom-a':A,
         'dom-b':B,
         'dom-c':C
      }
    });
  </script>
 
</body>
</html>

```

## vue-router的导航守卫之在导航完成后获取数据

需求：在导航完成之后加载数据。渲染DOM

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
</head>
<body>
	<div id="app"></div>
	<script type="text/javascript" src="vue.js"></script>
	<script type="text/javascript" src="vue-router.js"></script>
	<script type="text/javascript" src="axios.js"></script>
	<script type="text/javascript">

		// 导航完成后获取数据，这让我们有机会在数据获取期间展示一个 loading 状态，还可以在不同视图间展示不同的 loading 状态。
		var Index = {
			template:`
				<div>我是首页</div>
			`
		};

		var Post = {
			data(){
				return {
					loading:false,
					error:null,
					post:null
				}
			},
			template:`
				<div>
					<div class = 'loading' v-if = 'loading'>
						loading.....
					</div>
					<div v-if="error" class = 'error'>
						{{error}}
					</div>
					<div class = 'content' v-if = 'post'>
						<h2>{{post.title}}</h2>
						<p>{{post.body}}</p>
					</div>
				</div>
			`,
			created(){
				// 组件创建完成后获取数据
				// 此时data已经被监听了
				this.fetchData();

			},
			watch:{
				'$route':'fetchData'
			},
			methods:{
				fetchData(){
					this.error = null;
					this.post = null;
					this.loading = true;
					this.$axios.get('http://127.0.0.1:8888/post')
					.then(res=>{
						this.loading = false;
						console.log(res.data);
						this.post = res.data;
					})
					.catch(err=>{
						this.err = err.toString();
					})

				}
			}
		}

		var router = new VueRouter({
			routes:[
				{
					path:'/index',
					name:'index',
					component:Index
				},
				{
					path:'/post',
					name:'post',
					component:Post
				}
			]
		});

		var App = {
			template:`
				<div>
					<router-link :to = "{name:'index'}">首页</router-link>
					<router-link :to = "{name:'post'}">我的博客</router-link>

						<router-view></router-view>


				</div>
			`
		};
		Vue.prototype.$axios  = axios;
		new Vue({
			el:"#app",
			data:{

			},

			components:{
				App
			},
			template:`<App />`,
			router
		});
	</script>
</body>
</html>


```

## vue-router的导航守卫之导航完成之前获取数据

需求：在导航完成之前获取数据，之后再渲染DOM

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title></title>
</head>

<body>
    <div id="app"></div>
    <script type="text/javascript" src="vue.js"></script>
    <script type="text/javascript" src="vue-router.js"></script>
    <script type="text/javascript" src="axios.js"></script>
    <script type="text/javascript">
    // 导航完成后获取数据，这让我们有机会在数据获取期间展示一个 loading 状态，还可以在不同视图间展示不同的 loading 状态。

    var vm = null;
    var User = {
        data() {
            return {
                error: null,
                user: ''
            }
        },
        template: `
				<div>
					<div v-if="error" class = 'error'>
						{{error}}
					</div>
					<div class = 'user' v-if = 'user'>
						<h2>{{user}}</h2>
					</div>
				</div>
			`,
        beforeRouteEnter(to, from, next) {
            // 在渲染该组件的对应路由被 confirm 前调用
            // 不！能！获取组件实例 `this`
            // 因为当守卫执行前，组件实例还没被创建


            console.log(to);
            axios.get(`http://127.0.0.1:8888/user/${to.params.id}`)
                .then(res => {

                    next(vm => vm.setData(res.data))

                })
                .catch(err => {
                    console.log(err);
                    next(vm => vm.setError(err));
                })
        },
        beforeRouteUpdate(to, from, next) {
        	 // 在当前路由改变，但是该组件被复用时调用
	    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
	    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
	    // 可以访问组件实例 `this`

            this.user = null;
            this.$axios.get(`http://127.0.0.1:8888/user/${to.params.id}`)
                .then(res => {
                    this.setData(res.data);
                    next();
                })
                .catch(err => {
                 	   this.setError(err);
                    next();
                })



        },
        methods: {
            setData(user) {
                this.$nextTick(() => {
                    this.user = user;
                })
            },
            setError(err) {
                this.err = err.toString();

            }

        }

    }

    var router = new VueRouter({
        routes: [{
            path: '/user/:id',
            name: 'user',
            component: User,

        }]
    });

    var App = {
        template: `
				<div>
					
					<router-link :to = "{name:'user',params:{id:1}}">我的用户1</router-link>
					<router-link :to = "{name:'user',params:{id:2}}">我的用户2</router-link>

						<router-view></router-view>


				</div>
			`
    };
    Vue.prototype.$axios = axios;
    vm = new Vue({
        el: "#app",
        data: {

        },

        components: {
            App
        },
        template: `<App />`,
        router
    });
    </script>
</body>

</html>
```







## vue-cli2.x脚手架的使用

参考链接：https://github.com/vuejs/vue-cli/tree/v2#vue-cli--

安装：

```jade
npm install -g vue-cli
```

用法：

```
$ vue init < template-name >  < project-name >
```

例：

```
$ vue init webpack my-project
```

目前可用的模块包括：

- [webpack](https://github.com/vuejs-templates/webpack) - 一个功能齐全的Webpack + vue-loader设置，具有热重载，linting，测试和css提取功能。
- [webpack-simple](https://github.com/vuejs-templates/webpack-simple) - 一个简单的Webpack + vue-loader设置，用于快速原型设计。
- [browserify](https://github.com/vuejs-templates/browserify) -全功能Browserify + vueify设置用热重装载，linting＆单元测试。
- browserify [-simple](https://github.com/vuejs-templates/browserify-simple) - 一个简单的Browserify + vueify设置，用于快速原型设计。
- [pwa](https://github.com/vuejs-templates/pwa) - 基于webpack模板的vue-cli的PWA模板
- [simple](https://github.com/vuejs-templates/simple) - 单个HTML文件中最简单的Vue设置



相关文件和文件夹的含义：

![image-20200402085713939](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200402085713939.png)



## vue-cli3x脚手架的使用

vue-cli3x的官方文档：https://cli.vuejs.org/

Vue-cli3 中vue.config.js文件配置参考文档：https://cli.vuejs.org/zh/config/#integrity

```javascript
// vue.config.js 配置说明
//官方vue.config.js 参考文档 https://cli.vuejs.org/zh/config/#css-loaderoptions
// 这里只列一部分，具体配置参考文档
module.exports = {
  // 部署生产环境和开发环境下的URL。
  // 默认情况下，Vue CLI 会假设你的应用是被部署在一个域名的根路径上
  //例如 https://www.my-app.com/。如果应用被部署在一个子路径上，你就需要用这个选项指定这个子路径。例如，如果你的应用被部署在 https://www.my-app.com/my-app/，则设置 baseUrl 为 /my-app/。
  baseUrl: process.env.NODE_ENV === "production" ? "./" : "/",
 
  // outputDir: 在npm run build 或 yarn build 时 ，生成文件的目录名称（要和baseUrl的生产环境路径一致）
  outputDir: "dist",
  //用于放置生成的静态资源 (js、css、img、fonts) 的；（项目打包之后，静态资源会放在这个文件夹下）
  assetsDir: "assets",
  //指定生成的 index.html 的输出路径  (打包之后，改变系统默认的index.html的文件名)
  // indexPath: "myIndex.html",
  //默认情况下，生成的静态资源在它们的文件名中包含了 hash 以便更好的控制缓存。你可以通过将这个选项设为 false 来关闭文件名哈希。(false的时候就是让原来的文件名不改变)
  filenameHashing: false,
 
  //   lintOnSave：{ type:Boolean default:true } 问你是否使用eslint
  lintOnSave: true,
  //如果你想要在生产构建时禁用 eslint-loader，你可以用如下配置
  // lintOnSave: process.env.NODE_ENV !== 'production',
 
  //是否使用包含运行时编译器的 Vue 构建版本。设置为 true 后你就可以在 Vue 组件中使用 template 选项了，但是这会让你的应用额外增加 10kb 左右。(默认false)
  // runtimeCompiler: false,
 
  /**
   * 如果你不需要生产环境的 source map，可以将其设置为 false 以加速生产环境构建。
   *  打包之后发现map文件过大，项目文件体积很大，设置为false就可以不输出map文件
   *  map文件的作用在于：项目打包后，代码都是经过压缩加密的，如果运行时报错，输出的错误信息无法准确得知是哪里的代码报错。
   *  有了map就可以像未加密的代码一样，准确的输出是哪一行哪一列有错。
   * */
  productionSourceMap: false,
 
  // 它支持webPack-dev-server的所有选项
  devServer: {
    host: "localhost",
    port: 1111, // 端口号
    https: false, // https:{type:Boolean}
    open: true, //配置自动启动浏览器
    // proxy: 'http://localhost:4000' // 配置跨域处理,只有一个代理
 
    // 配置多个代理
    proxy: {
      "/api": {
        target: "<url>",
        ws: true,
        changeOrigin: true
      },
      "/foo": {
        target: "<other_url>"
      }
    }
  }
};

```



## RESTful

### RESTful 规范

　　一种软件的架构风格，设计风格，而不是标准，为客户端和服务端的交互提供一组设计原则和约束条件。

### 一  面向资源编程

　　每个URL代表一种资源，URL中尽量不要用动词，要用名词，往往名词跟数据库表格相对应。

	一般来说，数据库中的表都是同种记录的集合，所有API中的名词也应该使用复数。
	
	举例来说，有一个API提供动物园（zoo）的信息，还包括各种动物和雇员的信息，则它的路径应该设计成下面这样。

```javascript
https://api.example.com/v1/zoos
https://api.example.com/v1/animals
https://api.example.com/v1/employees
```



### 二  HTTP动词

	对于资源的具体操作类型，由HTTP动词表示
	
	常用的HTTP动词有下面五个(括号里对应的sql命令)

```javascript
GET（SELECT）：从服务器取出资源（一项或多项）。
POST（CREATE）：在服务器新建一个资源。
PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。
PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）。
DELETE（DELETE）：从服务器删除资源。
```

　　

### 三  在URL中体现版本

#### 　　	https://www.bootcss.com/v1/

　　https://v1.bootcss.com/

### 四  在URL中体现是否是API

　　https://www.bootcss.com/api/mycss

　　https://api.bootcss.com/mycss

### 五  在URL中的过滤条件

	如果记录数量很多，服务器不可能都将它们返回给用户。API应该提供参数，过滤返回结果。

```javascript
?limit=10：指定返回记录的数量
?offset=10：指定返回记录的开始位置。
?page=2&per_page=100：指定第几页，以及每页的记录数。
?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。
?animal_type_id=1：指定筛选条件
```



### 六  尽量使用HTTPS

　　https://www.bootcss.com/v1/mycss

### 七  响应时设置状态码

　　1**   信息，服务器收到请求，需要请求者继续执行操作

　　2**  成功，操作被成功接收并处理

　　3**  重定向，需要进一步的操作以完成请求

　　4**  客户端错误，请求包含语法错误或无法完成请求

　　5**  服务器错误，服务器在处理请求的过程中发生了错误

### 八  返回值

　　GET请求 返回查到所有或单条数据

　　POST请求  返回新增的数据

　　PUT请求  返回更新数据

　　PATCH请求  局部更新  返回更新整条数据

　　DELETE请求  返回值为空

### 九  返回错误信息

如果状态码是4xx，就应该向用户返回出错信息。一般来说，返回的信息中将error作为键名，出错信息作为键值即可。

```javascript
{
    error: "Invalid API key"
}
```



### 十   Hypermedia API

　　如果遇到需要跳转的情况 携带调转接口的URL

　Hypermedi API的设计,比如github的API就是这种设计，访问api.github.com会得到一个所有可用的API的网址列表。

```javascript
{
  "current_user_url": "https://api.github.com/user",
  "authorizations_url": "https://api.github.com/authorizations",
  // ...
}
```

从上面可以看到，如果想获取当前用户的信息，应该去访问 api.github.com/user，就会得到下面的记过

```javascript
{
message: "Requires authentication",
documentation_url: "https://developer.github.com/v3/users/#get-the-authenticated-user"
}
```

### 十一 其他

（1）API的身份认证应该使用OAuth 2.0框架

（2）服务器返回的数据格式，应该尽量使用JSON，避免使用XML

# 项目

- 生成项目文件，安装依赖安装包

<img src="C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200402112414130.png" alt="image-20200402112414130" style="zoom:80%;" />

- 安装mint-ui框架

  ```javascript
  npm install mint-ui -S
  ```

  ![image-20200402113731297](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200402113731297.png)

  > 参考网址：http://mint-ui.github.io/#!/zh-cn

- 在src下的main.js中使用mint-ui框架/引入mint-ui包及全局css样式

  ![image-20200402114531993](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200402114531993.png)

- 