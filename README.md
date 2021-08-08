# Click-and-Drag
效果：https://xl-z4869.github.io/Click-and-Drag/index.html
实现鼠标拖动时，页面中的条幅也跟着移动
### 主要步骤
#### 1.获取元素，监听鼠标事件
* 鼠标按下，添加样式
* 鼠标松开，清除样式
```
const items = document.querySelector('.items')

items.addEventListener('mousedown', (e) => {
    items.classList.add('active')
})

items.addEventListener('mouseup', () => {
    items.classList.remove('active')
})
```
#### 2.监听鼠标移动事件
* 当鼠标按下之后，才能触发鼠标移动事件，因此需要定义一个布尔值来进行判断
* 在鼠标按下的时候，还需要获取按下时以及滚动的x坐标
* 通过计算获得移动的距离，之后再x3使距离拉大，达到移动效果
```
let isDown = false
let startX
let scrollLeft
items.addEventListener('mousedown', (e) => {
    isDown = true
    items.classList.add('active')
    startX = e.pageX - items.offsetLeft
    scrollLeft = items.scrollLeft
})

items.addEventListener('mousemove', (e) => {
    if (!isDown) return
    e.stopPropagation()
    const x = e.pageX - items.offsetLeft
    const walk = (x - startX) * 3
    items.scrollLeft = scrollLeft - walk
})
```
