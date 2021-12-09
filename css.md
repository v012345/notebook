## 多行文字,溢出省略
```css
.text{
    /*将对象作为弹性伸缩盒子模型显示*/
    display: -webkit-box;
    /*设置子元素排列方式*/
    -webkit-box-orient: vertical;
    /*设置显示的行数，多出的部分会显示为...*/
    -webkit-line-clamp: 2;
}
```
```css
div{
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
```
## 背景图全覆盖,不重复
```css
div{
    background-image: url(./y0.png);
    background-repeat: no-repeat;
    background-size: cover;
}
```