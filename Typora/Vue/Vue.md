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



### **1.3.4. 指令语法**

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



### **1.4.2. 单向数据绑定**

1. 语法：`v-bind:href ="xxx"` 或简写为 `:href`
2. 特点：数据只能从 data 流向页面



### **1.4.3. 双向数据绑定**

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



### **1.8.2. 绑定监听**

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

