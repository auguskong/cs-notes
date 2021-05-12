

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

 

## Drag & Drop



### 知识点

* LocalStorage

  ```javascript
  // get the element and index
  arrayNames.forEach((arrayName, index) => {
  });
  ```

  

* Update DOM

  ```javascript
  backlogList.textContent // update the unordered list content
  ```

  

* [HTML Drag & Drop API](https://www.w3schools.com/html/html5_draganddrop.asp)

  * draggable
  * drag event, drag function  ondragstart
  * 在HTML中也需要添加eventListener



ondrop

ondragover

ondragenter: 进入了某一个特定区域就可以进行处理了 



高亮显示颜色是通过 CSS `.over` class来控制的

显示和取消是分成了两个步骤的 先add class 然后 remove class 

更新HTML element之后还需要更新loca Storage 当中的数据



HTML onclick attribute

contenteditable



为什么input field 没有在Save Item 之后hide ? 





inputItem 没有在被Save 之后及时隐藏起来? 为什么呢? 



```javascript
onclick="showInputBox()" 加错位置了 加在了add-btn-group中 和hideInputBox() 冲突了 不知道应该show 还是hide最后就超时了 
```







focusout event



focusin event



drag 和 edit content 发生了冲突 

```

```



![image-20210413215149595](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210413215149595.png)

### Q & A

```
JS 中 '' vs. `` 区别? 
`` 表示的是template ? 
```





### 快捷键

* Vim
  * `nyy`: 复制接下来的n行
  * `:5,10s/foo/bar/g`: Change each `foo` to `bar` for all lines from line 5 to line 12 (inclusive). more search and replace commands: https://vim.fandom.com/wiki/Search_and_replace
  * `:g/foo/d`: delete all lines that contain a particular pattern https://vim.fandom.com/wiki/Delete_all_lines_containing_a_pattern
  * `d1/>`: delete from the cursor to the 1th occurence of `>` 快速删除某一部分
  * `.`: repeat last norma command







### Debug

定义的div有两个class的话 会用哪一个 会重叠? 

createItemEl() 中的column param是干啥的? 

```
Uncaught SyntaxError: Unexpected token u in JSON at position 0
```

是因为是空数组? 



`JSON.parse(undefined)` 会报错

progress 写成了 proress 少了个g 结果就没有办法找到对应的token了





为什么我的object 变成空的了? 

![image-20210411150149987](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210411150149987.png)



Array数组中的data type不一致 导致更新失败了 数组中存的应该是string type 但是我直接更新成了 List.children[i] 就变成了object 然后`createItemEl()` 中使用`listEl.textContent = item;` 赋值时出错了



可以改进的地方 

* background color 没有进行实时的更新 会有三种颜色
* 如果item 没有添加到column当中可能background color就不会消失了![image-20210411201406744](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210411201406744.png)





## Splash Page 



### 知识点

* Figma 基本使用

  * Figma 是给Designer用的 可以创建mockup 和 prototype  image/icon/ 
  * 分层概念

* 图片资源管理

  * Splash Page Figma https://www.figma.com/file/4KIM14zOqqIKRuF8kBtHGs/Showcase-Website?node-id=1%3A2

  * 位置是Designer帮忙调整好了的 但是不能完全照抄 需要根据特定情况修改

    * ![image-20210408202145273](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210408202145273.png)

      比如这里就存在了只显示半页的图片 高度需要减半

  * 处理图片大小不匹配的问题 修改内部的`img` element

  * 更改背景板颜色 切换过去 并且切换回来

外部资源

* [Figma 官方文档](https://www.figma.com/best-practices/tips-on-developer-handoff/an-overview-of-figma-for-developers/) 
* 背景图画 https://www.heropatterns.com/
* 渐变背景图: https://uigradients.com/#EasyMed



### 心得

* 各种Element的嵌套本质上就是在进行分层
* 前端的确存在着大量的copy&paste低效的重复劳动 包括样式 定义各种div 找资源的link 
* 需要展示想法也是必不可少的



Q&A

* 为什么要对于App Store button 单独写一个div来包起来呢? 
* `const { body } = document;` 这是个什么写法? 



## Video Player



### 知识点

* HTML
  * `<video>`: insert video file
  * `<select>`: 下拉窗口 speed button
* CSS
  * @media 放在文件靠后的位置可以覆盖前面的attribute
  * `calc()`: CSS function lets you perform calculations when specifiying CSS property values
  * 

*

### 心得

![image-20210422223827877](/Users/xiangyu/Library/Application Support/typora-user-images/image-20210422223827877.png)





这里是格式错误是由于没有将div play 和 volume添加到 left control div当中

通过修改CSS来对视频下方的控制栏进行修改

```css
opacity: 
transition: all 0.5s ease-out 
cursor: pointer ?   
```



如何进行动态调整progress bar ? hover之后会有width的变化 

拖拽的位置会影响整个video的进度条 需要进行计算

CSS 当中querySelector的点是干嘛用的 选择的是class本身? 



可以直接check HTML`<video>` element 的各种性质 https://www.w3schools.com/tags/ref_av_dom.asp



使用play() method来播放video, pause() method来暂停video 

`paused`: returns whether the audio/video is paused or not G 



hover动画



使用



cursor: pointer 是



使用ternary operator 来代替if / else statement



通过给video.currentTime 变量赋值来改变视频的播放时间点



### 资源链接

* Font Awesome: 各种icon https://www.udemy.com/course/javascript-web-projects-to-build-your-portfolio-resume/learn/lecture/20893712#notes
* 

!(/Users/xiangyu/Library/Application Support/typora-user-images/image-20210422223735740.png)

### 快捷键

* Vim快捷键
  * `y t space`:复制当前行到下一个空格之前
  * paste location 是和copy的方式有关的 https://stackoverflow.com/a/9383985
  * `t`: till next character
  * 

直接check browser feature 

而不是check user agent value  



更加future proof 不会轻易改动

https://developer.mozilla.org/en-US/docs/Web/HTTP/Browser_detection_using_the_user_agent

https://security.stackexchange.com/questions/126407/why-does-chrome-send-four-browsers-in-the-user-agent-header

### Q&A



## Animated Template (2021.5.11)



### 资源链接

Taiwind 官网: https://www.creative-tim.com/learning-lab/tailwind-starter-kit/presentation



模板页面: https://www.creative-tim.com/learning-lab/tailwind-starter-kit/documentation/download



使用HTML Fomatter 来进行HTML格式调整



免费图片: 

https://unsplash.com/



Animation JS 网站: https://michalsnik.github.io/aos/



可以使用`async`关键字来异步加载third party library 先将页面render出来可以让用户感觉网页速度比较快





直接读文档 添加class 类型来添加动画效果

```
data-aos="fade-up
```



提高网站加载性能的技巧: 

https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/loading-third-party-javascript





## Music Player (2021.5.12)





## JS 进阶知识点

Fix memory problems: https://developer.chrome.com/docs/devtools/memory-problems/

Record heap snapshots: https://developer.chrome.com/docs/devtools/memory-problems/heap-snapshots/ 





