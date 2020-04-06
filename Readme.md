# 《CSS揭秘》笔记

## Chapter 2 背景和边框

1. [半透明边框](./Chapter%202/Chapter%202.1/transparent-borders.html)
  默认情况下, 背景会延伸到边框所在区域的下层(边框盒子). 可以设置`background-clip: padding-box;`将背景限制为内边距盒子。

2. [多重边框](Chapter%202/chapter%202.2/multiple-borders.html)
  使用`box-shadow`可以创建任意数量的多重边框, 且`box-shadow`产生的投影会贴合元素的圆角。
  使用`outline`实现的边框不会贴合元素的圆角。

3. [灵活的背景定位](Chapter%202/chapter%202.3/background-position.html)
  3.1. 可以使用`background-position`定位。
  3.2. 一般情况下，背景偏移和内边距一致，此时可以设置`background-origin: padding-box;`。

4. [边框内圆角](Chapter%202/chapter%202.4/inner-rounding.html)
  由于`border`和`box-shadow`会贴合圆角，`outline`不会贴合圆角。
  所以可以使用`outline`模拟边框，`box-shadow`来填充`outline`和`padding-box`之间的空隙。

5. 条纹背景
  5.1 [水平条纹背景](Chapter%202/chapter%202.5/horizontal-stripes.html)
  5.2 [垂直条纹背景](Chapter%202/chapter%202.5/vertical-stripes.html)
  5.3* [45度斜向条纹背景](Chapter%202/chapter%202.5/diagonal-stripes.html)
    需要指定条纹背景贴片的大小。
  5.4* [60度斜向条纹背景](Chapter%202/chapter%202.5/diagonal-stripes-60deg.html)
    需要指定条纹背景贴片的大小。

6. 复杂背景图案
  6.1* [蓝色网布](Chapter%202/chapter%202.6/blueprint.html)
    使用四个`linear-gradient`模拟。
  6.2* [波点](Chapter%202/chapter%202.6/polka.html)
    使用两个`radial-gradient`模拟。

7. [伪随机背景](Chapter%202/chapter%202.7/cicada-stripes.html)
  使用无法整除的`background-size`和`linear-gradient`尺寸来模拟。

8. [连续的图像边框](Chapter%202/chapter%202.8/continuous-image-borders.html) [信封边框](Chapter%202/chapter%202.8/vintage-envelop.html) [蚂蚁行军边框](Chapter%202/chapter%202.8/marching-ant.html)
  8.1 `background-clip`: `padding-box` / `content-box` / `border-box`
  8.2 `background-origin`: `padding-box` / `content-box` / `border-box`
  8.3 `background-size`: `contain` / `cover` / `auto`

## Chapter 3 形状

9. [自适应的椭圆](./Chapter%203/chapter%203.9/ellipse.html) [自适应半椭圆](Chapter%203/chapter%203.9/half-ellipse.html) [自适应四分一椭圆](Chapter%203/chapter%203.9/quarter-ellipse.html)
  `border-radius`使用百分比`50%`或者`100%`

10. 平行四边形
  10.1 [嵌套元素方案](Chapter%203/chapter%203.10/parallelograms.html)
    由于直接使用`transform`的话，字体也会跟着变形，所以可以额外嵌套一个元素，再进行一次反向的变形，来抵消容器的变形。
  10.2 [伪元素方案](Chapter%203/chapter%203.10/parallelograms-pseudo.html)
    容器不变行，由伪元素提供变形的效果，不需要添加额外的HTML元素，推荐方案。

11. [菱形图片](Chapter%203/chapter%203.11/diamond-images.html)

  ``` html
  <div class="diamond">
    <img src="http://csssecrets.io/images/adamcatlace.jpg" />
  </div>
  ```

  ``` css {highlight=[7-8,13]}
  .diamond {
    width: 250px;
    height: 250px;
    margin: 100px;
    border: 1px dashed gray;

    overflow: hidden;
    transform: rotate(45deg);
  }

  .diamond > img {
    max-width: 100%;
    transform: rotate(-45deg) scale(1.42);
  }
  ```

  需要额外嵌套一个HTML元素，使用`transform: rotate(45deg);`旋转。
  图片使用一次反向的变形`transform: rotate(-45deg);`，来抵消容器的变形。
  且由于矩形旋转后，图片的宽度应该由边长变成对角线长，所以需要使用`transform：scale(1.42)`放大。

12. [切角效果](Chapter%203/chapter%203.12/bevel-corners-gradients.html) [弧形切角效果](Chapter%203/chapter%203.12/scoop-corners.html) [SVG切角方案](Chapter%203/chapter%203.12/bevel-corners-svg.html)
  斜边切角使用`linear-gradient`模拟，弧边切角使用`radial-gradient`模拟。
  需要配合`background-position`、`background-size`、`background-repeat`使用。

13. [梯形标签页](Chapter%203/chapter%203.13/trapezoid-tabs.html)

  ``` html
  <nav class="both">
    <a href="#">Home</a>
    <a href="#" class="selected">Projects</a>
    <a href="#">About</a>
  </nav>
  <main>
    Content area
  </main>
  ```

  ``` css {highlight=[2-3,12-21,26]}
  nav > a {
    /* 相对于普通位置定位，没设置top/right/bottom/left时与正常位置相同 */
    position: relative;

    /* 左右边距为负值，缩小tab导航标签的间距 */
    margin: 0 -0.3em;

    display: inline-block;
  }

  nav > a::before {
    /* 在选中元素的内容之前插入内容，content属性只能跟伪元素一起使用 */
    content: '';

    /* 元素相对于position值不为static的第一个祖先元素来定位 */
    position: absolute;
    /* 相对于position属性指定的元素的偏移量 */
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;

    /* 使用负值降低优先级 */
    z-index: -1;

    transform: perspective(0.5em) rotateX(5deg) scale(1.2, 1.3);
  }
  ```

14. [动态饼图](Chapter%203/chapter%203.14/pie-animated.html) [静止饼图](Chapter%203/chapter%203.14/pie-static.html)

  ``` html
  <div class="pie">20%</div>
  ```

  ``` css {highlight=[6-9]]}
  @keyframes spin { to { transform: rotate(0.5turn); }}

  @keyframes bg { 50% { background-color: #655; }}

  .pie {
    /* 默认颜色 左边半圆颜色 颜色1 */
    background-color: yellowgreen;
    /* 默认颜色 右边半圆颜色 颜色2 */
    background-image: linear-gradient(to right, transparent 50%, #655 0);

    margin: 40px;
    height: 100px;
    width: 100px;
    border-radius: 50%;
  }

  .pie::before {
    content: '';

    /* 此元素将显示为块级元素，此元素前后会带有换行符 */
    display: block;

    margin-left: 50%;
    width: 50%;
    height: 100%;

    /* 初始颜色 颜色1 */
    background-color: inherit;

    border-top-right-radius: 100% 50%;
    border-bottom-right-radius: 100% 50%;

    /* 选择的圆点为圆心 */
    transform-origin: 0 50%;

    animation: spin 0.5s linear, bg 1s step-end;
    /* 动画初始状态为暂停 */
    animation-play-state: paused;
    /* 动画延迟继承自pie元素，由脚本设置！ */
    animation-delay: inherit;
  }
  ```

  ``` js
  document.querySelectorAll('.pie').forEach(pie => {
    const percent = parseFloat(pie.textContent) / 100;
    pie.style.animationDelay = '-' + percent + 's';
  });
  ```

## Chapter 4 视觉效果

14. [单侧投影](Chapter%204/chapter%204.15/shadow-one-side.html) [邻边投影](Chapter%204/chapter%204.15/shadow-two-sides.html) [双侧投影](Chapter%204/chapter%204.15/shadow-opposite-sides.html)

  ```css
  /* x偏移量 | y偏移量 | 阴影模糊半径 | 阴影扩散半径 | 阴影颜色 */
  box-shadow: 0px 5px 4px -2px rgba(0, 0, 0, 0.5);;
  ```

16. [不规则投影](Chapter%204/chapter%204.16/drop-shadow.html)

  ```css {highlight=[4-5]}
    /* 使用box-shadow会出错，无法符合要求 */
    /* box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5); */

    /* 使用filter的drop-shadow CSS函数可以满足要求 */
    filter: drop-shadow(5px 5px 10px rgba(0, 0, 0, 0.5));
  ```

  [CSS filter 滤镜 (MDN)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/filter)

17. [染色效果(基于滤镜)](Chapter%204/chapter%204.17/color-tint-filter.html) [染色效果(基于混合模式)](Chapter%204/chapter%204.17/color-tint.html)

  ```css {highlight=[5-6]}
  /* 基于混合模式 */
  background-image: url(http://csssecrets.io/images/tiger.jpg);
  background-color: hsl(335, 100%, 50%);

  /* 定义该元素的背景图片和背景色如何混合 */
  background-blend-mode: luminosity;
  ```

  `background-blend-mode` 定义该元素的背景图片和背景色如何混合。 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-blend-mode)

18. [毛玻璃效果](Chapter%204/chapter%204.18/frosted-glass.html)

  ```css {highlight=[4]}
  /* 避免背景的模糊效果超过容器 */
  overflow: hidden;
  
  filter: blur(10px);
  ```

19. [45°折角效果](Chapter%204/chapter%204.19/folded-corner.html) [30°折角效果](Chapter%204/chapter%204.19/folded-corner-realistic.html)

## Chapter 5 字体排版

20. [连字效果](Chapter%205/chapter%205.20/hyphenation.html)

  ```css
  /* Chrome only supported on Android & Mac platform!!!! */
  hyphens: auto
  ```

21. [插入换行](Chapter%205/chapter%205.21/break-lines.html)

  ```html
  <dt>Email:</dt>
  <dd>lea@verou.me</dd>
  <dd>leaverou@mit.edu</dd>
  ```

  ```css{highlight=[6-9]}
  dt, dd {
    display: inline;
    margin: 0;
  }

  dd + dt::before {
    content: '\A';
    white-space: pre;
  }

  dd + dd::before {
    content: ', ';
  }
  ```

22. [斑马条纹](Chapter%205/chapter%205.22/zebra-lines.html)

  ```html
  <pre>line 1
    line 2
    line 3</pre>
  ```

  ```css{highlight=[6,9]}
  pre {
    padding: 0.5em;
    line-height: 1.5em;

    /* 背景的大小是2倍的line-height */
    background-size: 100% 3em;

    /* 使用渐变模拟条纹 */
    background-image: linear-gradient(gray 50%, gold 0);

    /* 背景区域为内容盒子, 可以让条纹不受边框和内边距的影响 */
    background-origin: content-box;
  }
  ```

23. [调整tab的宽度](Chapter%205/chapter%205.23/tab-size.html)

  ```css
  /* IE,Edge不支持tab-size，Chrome不支持这个属性的动画，VS Code我的常用设置会把Tab转化为空格~~~ */
  tab-size: 2;
  ```

26. [自定义下划线](Chapter%205/chapter%205.26/underlines.html)

  ```html
  <p>“The only way to <a>get rid of a temptation </a> is to <a>yield</a> to it.”</p>
  ```

  使用 `text-decoration: underline;` 无法自定义下划线的样式。
  如果设置`border-bottom` 如果出现文本换行时，无法正确显示下划线。
  最佳方法为使用`background-image: linear-gradient()`。

  ```css
  a {
    background-position: bottom;

    /* 生成实线样式的下划线 */
    background-image: linear-gradient(gray, gray);
    background-repeat: no-repeat;
    background-size: 100% 2px;

    /* 生成虚线样式的下划线 */
    background: linear-gradient(90deg, gray 66%, transparent 0) repeat-x;
    background-repeat: repeat-x;
    background-size: 0.2em 1px;
  }
  ```

## Chapter 6 用户体验

29. [鼠标光标](Chapter%206/chapter%206.29/disabled.html)

  ```css
  cursor: not-allowed;
  ```

  常用的`cursor`样式: `crosshair`, `help`, `move`, `pointer`, `wait`, `none`, `ew-resize`, `ns-resize`, `nesw-resize`, `nwse-resize`, `col-resize`, `row-resize`, `all-scroll`, `zoom-in`, `zoom-out`。

30. 扩大可点击范围 [放大按钮方案](Chapter%206/chapter%206.30/hit-area-border.html) [伪元素方案(最佳方案)](Chapter%206/chapter%206.30/hit-area.html)

  `border` 可以增加点击区域范围,但是效果不够好,会让按钮变大。
  `box-shadow` 不能增加点击范围，不会让按钮变大。
  伪元素能增加点击范围，而且不会让按钮变大，是最佳方案。

  ```html
  <button>+</button>
  ```

  ```css{highlight=[12,15-24]}
  button {
    cursor: pointer;
    color: white;
    padding: 0.3em 0.5em;
    background: #58a;
    border-radius: 50%;
    margin-left: 10px;

    /* border可以增加点击区域范围,但是效果不够好,会让按钮变大 */
    border: 1px solid rgb(200, 200, 200);

    position: relative;
  }

  /* 伪元素可以响应鼠标事件 */
  button::before {
    content: '';

    position: absolute;
    top: -10px;
    bottom: -10px;
    left: -10px;
    right: -10px;
  }
  ```

31. 自定义复选框 [复选框](Chapter%206/chapter%206.31/checkboxes.html) [开关式按钮](Chapter%206/chapter%206.31/toggle-buttons.html)

  原生CSS不支持定义复选框的样式！hack 方法。

32. [通过阴影弱化背景](Chapter%206/chapter%206.32/dimming-box-shadow.html)
  
  ```css
  box-shadow: 0 0 0 50vmax rgba(0, 0, 0, 0.8);
  ```

  1vmax相当于1vw和1vh两者中的较大值，100vw等于整个视口的宽度，100vh等于整个视口的高度。
  box-shadow不会增加元素可点击的范围，所以可以遮蔽背景的事件！！！

33. [通过模糊弱化背景](Chapter%206/chapter%206.33/deemphasizing-blur.html)

  ```css
  filter: blur(5px);
  ```

34. [滚动提示](Chapter%206/chapter%206.34/scrolling-hint.html)

  使用了`background-attachment`属性的区别：

  `fixed` 此关键字表示背景相对于**视口**固定。即使一个元素拥有滚动机制，背景也不会随着元素的内容滚动。

  `local` 此关键字表示背景相对于**元素的内容**固定。如果一个元素拥有滚动机制，背景将会随着元素的内容滚动， 并且背景的绘制区域和定位区域是相对于可滚动的区域而不是包含他们的边框。

  `scroll` 此关键字表示背景相对于**元素本身**固定， 而不是随着它的内容滚动（对元素边框是有效的）。

35. 交互式图片对比控件 [CSS Resize方案](Chapter%206/chapter%206.35/image-slider.html) [范围输入控件方案](Chapter%206/chapter%206.35/image-slider-controller.html)

## Chapter 7 结构和布局

36. [自适应内部元素](Chapter%207/chapter%207.36/intrinsic-sizing.html)

  ```css
  /* IE和Edge截止2020-04都不支持 min-content!! */
  width: min-content
  ```

37. [精确控制表格列宽](Chapter%207/chapter%207.37/table-column-width.html)

  ```css
  /* 为了使table-layout生效,需要设置width. */
  width: 100%;

  /** 表格和列的宽度通过表格的宽度来设置，某一列的宽度仅由该列首行的单元格决定。
    * 在当前列中，该单元格所在行之后的行并不会影响整个列宽。
    * 使用 “fixed” 布局方式时，整个表格可以在其首行被下载后就被解析和渲染。
    * 这样对于 “automatic” 自动布局方式来说可以加速渲染。
    * 任何一个包含溢出内容的单元格可以使用 overflow  属性控制是否允许内容溢出。
    */
  table-layout: fixed;
  ```

  控制文本行溢出行为`text-overflow`: `ellipsis`;

38. [兄弟元素选择器](Chapter%207/chapter%207.38/styling-sibling-count.html)

  方法1：

  ```css
  /* 相邻兄弟元素选择器 ~ , 可以选中在它之后的所有兄弟元素. (**不包含自身**) */
  div > span:nth-child(4),
  div > span:nth-child(4) ~ span {
    background-color: #ae0055;
  }
  ```

  方法2：

  ```css
  /* :nth-child(), n+b这种形式的表达式可以选中从第b个元素开始的所有子元素。(**包含自身**)*/
  div > span:nth-child(n + 4) {
    background-color: #ae0055;
  }
  ```

39. [满幅的背景，定宽的内容](Chapter%207/chapter%207.39/fluid-fixed.html)

  ```css
  header,
  section,
  footer {
    padding: 1em calc(50% - 350px);
  }
  ```

40. 垂直居中

  a. [基于绝对定位](Chapter%207/chapter%207.40/vertical-centering-abs.html)

  ```css
  div {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
  ```

  b. [基于视口单位vh](Chapter%207/chapter%207.40/vertical-centering-vh.html)

  ```css
  div {
    margin: 50vh auto 0;
    transform: translateY(-50%);
  }
  ```

  c. [基于Flexbox](Chapter%207/chapter%207.40/vertical-centering-flex.html)
  
  ```css
  /* 注意：设置在父级的元素上！！ */
  body {
    /* 设置水平垂直居中 */
    display: flex;
    align-items: center;
    justify-content: center;

    /* 设置父级元素的大小 */
    min-height: 100vh;
  }
  ```

41. 紧贴底部的页脚

  a. [固定高度的解决方案](Chapter%207/chapter%207.41/sticky-footer-fixed.html)
  
  ```css
  body {
    margin: 0;
  }

  header {
    height: 10em;
    box-sizing: border-box;
  }

  footer {
    height: 12em;
    box-sizing: border-box;
  }

  main {
    /* 不能使用calc(100% - 10em - 12em) */
    /* 此方案不够灵活的原因是每次更改footer或者header的高度都需要同时更改main的高度。 */
    height: calc(100vh - 10em - 12em);
    box-sizing: border-box;
  }
  ```

  b. [更灵活的解决方案](Chapter%207/chapter%207.41/sticky-footer.html)

  ```css
  body {
    margin: 0;

    display: flex;
    /* CSS flex-flow 属性是 flex-direction 和 flex-wrap 的简写。 */
    /* flex-flow默认属性是row */
    flex-flow: column;

    min-height: 100vh;
  }

  main {
    /* CSS属性 flex 规定了弹性元素如何伸长或缩短以适应flex容器中的可用空间。
     * 这是一个简写属性，用来设置 flex-grow, flex-shrink 与 flex-basis。
     * 大多数情况下，开发者需要将 flex 设置为 auto，initial，none，或一个无单位正数
     */
    flex: 1;
  }
  ```
