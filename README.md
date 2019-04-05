自定义的fullpage效果, 其核心是`top`属性的改变

#### 起步
  1. 复制此模板去自己的项目中
  2. 每一个滚动屏div添加上`class:section`
  3. 在totalPageNum填入当前滚动屏的数量

#### 使用了一些技巧
  - css高度属性  hv, wv, 高度，宽度的视口大小， 100hv = 1 viewport height 等等
  - 为了双向数据绑定，将变化的css属性 以style属性的方式写在了标签内部。

#### 预览效果
![预览效果](/1.gif)
