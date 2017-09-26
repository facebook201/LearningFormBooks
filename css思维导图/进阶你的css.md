#### 组织你的CSS代码

* 头部使用UTF-8

  @charset 'UTF-8';



* 命名空间规范

  布局：以g为命名空间 例如 .g-wrap、g-header、.g-content

  状态：以s为命名空间 表示动态 具有交互性质的状态 例如 .s-current、s-selected

  工具：以u为命名空间 表示不耦合业务逻辑的 可复用的工具 例如：u-clearfix、u-ellipsis

  组件：以m为命名空间 表示可复用 移植的组件模块。 m-slider、m-dropMenu

  钩子：以j为命名空间 表示特定给JavaScript调用的类名 j-request j-open

  ​

* 建议使用 - 连接。字符小写

  ​

* 选择器

  当多个选择器的时候，每个选择器单独占一行。

  ​

* 数值与单位

  - 当属性值或颜色参数为 0 – 1 之间的数时，省略小数点前的 0 。color: rgba(255, 255, 255, 0.5)color: rgba(255, 255, 255, .5);

  - 当长度值为 0 时省略单位。margin: 0px automargin: 0 auto

  - 十六进制的颜色属性值使用小写和尽量简写。color: #ffcc00color: #fc0

    ​

* 样式的顺序

  按功能进行分组，并以 Positioning Model > Box Model > Typographic > Visual 的顺序书写，提高代码的可读性。

  ```CSS
  /* 如果有content属性 就放在第一位 */
  content: '', 
  /* Positioning Model 布局方式、位置，相关属性 */
  position: relative; // 布局相关 位置 top left z-index float display
  top: 10px;
  z-index: 10,
  float: left;
  display: block;
  /* Box Model 盒子模型 width padding overflow border */
  height: 100px;
  padding: 10px;
  overflow: hidden;
  /* 文字排版 font line-height */
  line-height: 20px;
  text-align: center;
  word-wrap: break;
  /* 视觉外观 相关属性 */
  color: #fff;
  background-color: #1f09sa;
  ```

  ​

* ​





















* ​