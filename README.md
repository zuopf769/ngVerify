# ngVerify v1.1.9

a easy angular form vaild plugin.
简洁高效的__angular表单验证插件__


<br>
## github
https://github.com/Moerj/ngVerify

<br>
## DEMO
http://moerj.com/Github/ngVerify/

<br>
## Getting Started
在使用前，你需要引入angular

```javascript

require('angular');

require('ngVerify');

var app = angular.module('APP',['ngVerify']);

```

### type
	设置表单元素type类型，目前支持的type类型：

	email
	number
	phone
	url
	string
	radio
	checkbox
	select


<br>
<h2 style="color:#d9534f">verify-scope</h2>
入口指令，规定组件所控制的表单范围

```html
<form verify-scope>
	...
</form>
```

### tipStyle (defualt: 1)
设置整个表单的错误消息样式
1. 气泡浮动提示，在元素右上角浮出
2. 气泡固定高度，紧接着元素另起一行

```html
<form verify-scope="tipStyle: 2" >...</form>
```

### notip (defualt: false)
true时关闭tip提示
```html
<form verify-scope="notip: true" >...</form>
```


<br>
<h2 style="color:#d9534f">ng-verify</h2>
元素指令，定义验证规则

### defualt
只需要使用ng-verify，会根据type类型校验非空验证和类型的格式
```html
<!-- 校验非空验证和邮箱格式 -->
<input type="email" ng-verify >
```

### required (defualt: true)
false允许空值通过校验
```html
<input type="number" ng-verify="required: false" >
```

### length (min,max)
定制校验字符长度
```html
<input type="text" ng-verify="{min:3,max:6}" >
```

### pattern
自定义正则，这样会优先以你的正则进行校验
```html
<input type="text" ng-verify="pattern:/a-zA-Z/" >
```

### errmsg
自定义错误消息，会覆盖掉默认的提示。
```html
<input type="text" ng-verify="{errmsg:'其实这里没有错，我是在逗你玩'}" >
```

### option (defualt: 0)
select下拉菜单属性，指定的option表示选中会校验不通过
```html
<select ng-verify="option:0" >
	<option>请选择</option>
		<option>1</option>
		<option>2</option>
		<option>3</option>
</select>
```

### least (defualt: 1)
checkbox最少勾选数，指定至少勾选几项才会通过验证
```html
<div>
	<label >checkbox</label>
	<!-- checkbox多选，请确保所有checkbox被一个容器包起 -->
	<!-- 如果要用label修饰checkbox请统一所有都用 -->
	<!-- 确保每组checkbox的name属性相同，ng-verify指令只需要在任意一个checkbox上 -->
	<input type="checkbox" name="checkbox" > Captain America
	<input type="checkbox" name="checkbox" > Iron Man
	<input type="checkbox" name="checkbox"  ng-verify="least:2"> Hulk
</div>
```

### control
绑定一个表单提交按钮, control:'formName'
```html
<form name="myform" verify>
	...

	<a ng-verify="{control:'myform'}" ></a> <!-- 表单内的按钮 1 -->

	<input type="submit" ng-verify /> <!-- 表单内的按钮 2 -->
</form>

<button ng-verify="{control:'myform'}" >提交</button> <!--表单外的按钮-->
```

### disabled (defualt: true)
设置 disabled:false 提交按钮在表单未校验通过时不会禁用，并且会自动绑定一个click事件，点击时标记所有错误表单。
```html
	<button ng-verify="disabled:false" >按钮</button>
```

### tipStyle (defualt: form verify-scope)
同上，设置单个元素提示样式

### notip (defualt: form verify-scope)
同上，设置单个元素是否显示tip


## API
依赖注入，在v0.1.6版本以后，公共方法需要依赖注入
```javascript
//依赖注入ngVerify后，可以调用一些公共方法
app.controller('yourCtrl',function(ngVerify){
	...
})
```

### ngVerify.check()
检测一个verify表单是否验证通过，返回Boolean和errorArry(未校验通过的元素组)
```javascript
ngVerify.check('formName') //返回结果

ngVerify.check('formName',true) //返回结果，并标记出未验证通过元素
```

### ngVerify.scope()
获取一个verify表单的$scope作用域
```javascript
ngVerify.scope('formName')
```

## tips
- 传入的参数字符串都必须是对象参数"{key1: value1, key2: value2}"，可以不写大括号 { }
- checkbox、radio组绑定验证最好绑在最后一个
- errmsg参数通常不需要你设置
- 表单范围内的按钮，只要type="submit"则不需要设置control参数
- 本组件可以检测非表单元素，但是检测的是其文本值而且非value值
- 不支持form嵌套

## Support
- IE 9+
- angular 1.x
