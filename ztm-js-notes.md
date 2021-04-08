

## Quote Generator

Demo: https://jacintodesign.github.io/quote-generator/



### 知识点

* AJAX API call

* Twitter

* Loading Animation
* Mobile Responsive: fit the size of the mobile screen



### 外部资源

* Google Fonts: https://fonts.google.com/
* Hero Patterns: 做背景图 https://www.heropatterns.com/



### 快捷键

#### HTML快捷键

* `.`: 给新添加的element 添加className
* `#`: 给新添加的element 添加idKK



#### VS Code快捷键 

* control + 数字: 在已经打开的文件中切换
* control + ` : 切换到terminal 



#### Vim 快捷键

* `f` + `space` / `char`: find the next `space` / `char`
* `F ` + `space` / `char`: find the next `space` /  `char` (backward 向前找)



Twitter Intergration: https://developer.twitter.com/en/docs/twitter-for-websites/tweet-button/guides/web-intent 



展示Quote的过程

JS和HTML element 的结合是通过DOM来操作的



如何在HTML中动态绑定变量?  直接通过id来绑定的



和button 绑定 添加一个EventListener 然后绑定 `click` 和一个JS function







Animation 只是一个简单的loader class 就行



使用`hidden` method



loading() 必须要在getQuotes里面也call一次 否则仍然会显示



### Code



```css
button:hover {
  
}
   
/* doc: https://developer.mozilla.org/en-US/docs/Web/CSS/:active */
button: active {
  
}

@media screen and (max-width: 1000px) {
  
}
```



Fetch Data 









## Form Validation







`<form>` element defines a form that is used to collect user input

`<input>` type可以用来定义样式 `button` `checkbox` `color` etc

https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input



`email` type自动的就能进行validate 





[Form Elements](https://www.w3schools.com/html/html_form_elements.asp)



`<label>`: 是用来做为提示符的





`<input type="submit">` defines a button for submitting the form data to a form-handler



如何绑定submit button和Enter键?

如何读取input当中的field 并validate?



doc_verify的表格用到了`<input>` type 吗?



VSCode Tips



* multi-cursor
  *  `Alt + Click` 
  *  如果是选择相同的单词 可以先选中 再按`Ctrl/Command + D`来自动定位当前选中词的下一次出现位置



Validate



[Send form data](https://developer.mozilla.org/en-US/docs/Learn/Forms/Sending_and_retrieving_form_data)



[Submit Event](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/submit_event)

The `submit` event fires when the user clicks a submit button ([`<button>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button) or [\<input type="submit"\>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit)) or presses Enter while editing a field (e.g. [\<intput type="text"\>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text)) in a form. The event is not sent to the form when calling the [`form.submit()`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/submit) method directly.







按下enter键本身是一个event 这个event 可以trigger 一个action 需要有一个监听的function



React 提供了让我们定制组件的能力





## Infinite Scroll



### 知识点

* 生成 / 下载 loading animation 保存为`svg` 文件

* Loader 的展示/隐藏 以及位置居中

* 通过API Call 从第三方站点加载图片 

* 使用js来添加HTML 

  ```javascript
  document.createElement('img')
  setAttribute('href', <your link>)
  ```

  * document.createElement()

* 实现infinite scroll: 最基本的原理是先看一下当前位置在总体位置的哪里，如果已经接近底部的时候(最大值减去一个自定义的值) 重新call API拿数据并且加载新的数据

  * `window.scrollY`: Distance from top of page user has scrolled 已经翻过的页面的距离
  * `window.innerHeight`: Total height of browser window  
  * `document.body.offsetHeight`: Height of everything in the body, including what is not within view. 



需要解决多次加载的问题 





### 外部资源

* loader动画 loading animation: https://loading.io/
* 第三方图片素材库: https://unsplash.com/

### 快捷键

* 



### Debug

```javascript
if (imageLoaded == totalImages) {
  ready = true;
}
```

```
Uncaught SyntaxError: Identifier 'imageLoaded' has already been declared
```

JS中的 `==` 和 `===`  含义不同?  这不是原因



原因是因为我的变量名和function名字重复了 都是用了imageLoaded 所以没有办法分开 





### 心得

html 更像是 一个框架 内部的各种元素都可以通过js来生成



```javascript
for (const key in attributes) {
  element.setAttribute()
}
```



最简单的重构: 使用for loop 来代替重复代码



template ? 

使用变量添加到url 当中

 



