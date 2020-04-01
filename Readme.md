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

  