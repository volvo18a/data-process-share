# 关于一些数据处理方法的分享(前端)

> 限制输入30个字符或15个中文

```js
/*
* this.streamName 为输入的字符
* this.streamNameSize 为长度记录 一个中文长度增减2
*/
changeNameKeyUp() {
    let len = 0;
    // console.log(this.streamName);
    for (let i = 0; i < this.streamName.length; i++) {
        if (this.streamName.charCodeAt(i) > 255) {
            len += 2;
            if (len > 30) {
                this.streamName = this.streamName.substring(0, i);
                len -= 2;
            }
            this.streamNameSize = len;
        } else {
            len++;
            if (len > 30) {
                this.streamName = this.streamName.substring(0, i);
                len--;
            }
            this.streamNameSize = len;
        }
    }
}
```

__changeNameKeyUp()__ 为 __input__ 绑定的 __keyup__ 事件

> 两个数组对象对比出各自特有的项

```js
//step 1
var arr1 = [
	{id: 1, name: '1111'},
	{id: 2, name: '2222'},
	{id: 3, name: '3333'}
];

//step 2
var arr2 = [
	{id: 1, name: '1111'},
	{id: 3, name: '3333'},
	{id: 4, name: '4444'},
	{id: 5, name: '5555'},
];

//step 3
var temp = arr1.filter(val1 => {
	return arr2.every(val2 => {
		return val2.id !== val1.id;
	})
})
```

输出 __temp__ 为 ```[ {id: 2, name: '2222'} ]```
若要取出 __arr2__ 中特有的项 将 __step 3__ 位置反一下即可 (ps: 方法取自贤鱼老师)

> 简易的点击元素复制指定内容到剪切板的小方法

```html
<div id="box" style="width: 100px; height: 100px; background-color: #ccc"></div>
```

```js
let box = document.getElementById('box');

box.onclick = function(e) {
	let videoDom = e.target;
	console.log(videoDom.nodeName);
	const aux = document.createElement('input');
	const content = "something";
	aux.setAttribute('value', content);
	document.body.appendChild(aux);
	aux.select();
	aux.setSelectionRange(0, aux.value.length);
	document.execCommand('copy');
	document.body.removeChild(aux);
}
```

简单分析：创建一个 __input Dom__ 元素 (__aux__) 将指定内容设置为该元素的 __value__ 属性
元素加入页面 调用该元素的 __select setSelectionRange__ 方法 选中元素 再调用 __document.execCommand('copy')__ 进行复制操作，删除该元素

持续更新ing( •̀ ω •́ )y
