## 重绘和回流
- 可以改变布局,隐藏,尺寸等,则为**回流**.如改变元素的top,width等
- 只改变元素的外观,则为**重绘**.如改变color,background等
  
  > 回流必定会重绘
* **获取布局信息的时候,会强制刷新回流队列**.[参考文章](https://gist.github.com/paulirish/5d52fb081b3570c81e3a). 获取布局信息的操作:
  - offsetTop、offsetLeft、offsetWidth、offsetHeight
  - scrollTop、scrollLeft、scrollWidth、scrollHeight
  - clientTop、clientLeft、clientWidth、clientHeight
  - getComputedStyle()
  - getBoundingClientRect
    > 简单来说, 在浏览器还没执行重绘或者回流队列的时候.如果此时人为进行了获取布局信息的操作.则会触发重绘或者回流的机制;
    > ```javascript
    >  let ele = document.querySelector('#id1')
    >  ele.style.color = 'blue'
    >  ele.style.borderLeft = '10px';
    >  ele.style.borderRight = '20px';
    >  console.log(ele.offsetHeight); // 这里就会产生重绘了.通过Performance可以看到进行了2次重绘
    >  ele.style.padding = '50px';
    > ```

## 减少重绘和回流的一些方法
* 可以通过直接改变CSS样式,而不直接改变元素属性.如新增一个className

* 可以通过display:none,先隐藏需要改变的元素,最后再展示,这样,这里就只会产生2次重绘
  > ```javascript
  > let ele = document.querySelector('#id1')
  > ele.style.display = 'none'
  > // 这里进行你想要改变元素的一些操作
  > ele.style.display = 'block'
  > ```
  
* 避免直接访问布局信息的一些操作,避免因此强制进行回流的操作
* 对于复杂动画,使用绝对定位,让其脱离文档留
* 如果可以,可以通过transform来替代top left的一些操作   
