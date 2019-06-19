## 目录

1. **[CSS 盒模型,在不同浏览器的差异](#css-盒模型在不同浏览器的差异)**
1. **[CSS 所有选择器及其优先级、使用场景,哪些可以继承,如何运用 at 规则](#css-所有选择器及其优先级使用场景哪些可以继承如何运用-at-规则)**
1. **[CSS 伪类和伪元素有哪些,它们的区别和实际应用](#css-伪类和伪元素有哪些它们的区别和实际应用)**
1. **[HTML 文档流的排版规则,CSS 几种定位的规则、定位参照物、对文档流的影响,如何选择最好的定位方式,雪碧图实现原理](#html-文档流的排版规则CSS几种定位的规则定位参照物对文档流的影响如何选择最好的定位方式雪碧图实现原理)**
1. **[水平垂直居中的方案、可以实现 6 种以上并对比它们的优缺点](#水平垂直居中的方案可以实现-6-种以上并对比它们的优缺点)**
1. **[BFC 实现原理,可以解决的问题,如何创建 BFC](#bfc-实现原理可以解决的问题如何创建bfc)**
1. **[可使用 CSS 函数复用代码,实现特殊效果](#可使用-css-函数复用代码实现特殊效果)**
1. **[PostCSS、Sass、Less 的异同,以及使用配置,至少掌握一种](#postcsssassless的异同以及使用配置至少掌握一种)**
1. **[CSS 模块化方案、如何配置按需加载、如何防止 CSS 阻塞渲染](#css-模块化方案如何配置按需加载如何防止-css-阻塞渲染)**
1. **[熟练使用 CSS 实现常见动画,如渐变、移动、旋转、缩放等等](#熟练使用-css-实现常见动画如渐变移动旋转缩放等等)**
1. **[CSS 浏览器兼容性写法,了解不同 API 在不同浏览器下的兼容性情况](#css-浏览器兼容性写法了解不同-api-在不同浏览器下的兼容性情况)**
1. **[掌握一套完整的响应式布局方案](#掌握一套完整的响应式布局方案)**

### CSS 盒模型,在不同浏览器的差异

**W3C 中的盒子模型的宽：包括 margin + border + padding + width;**

`W = margin * 2 + border * 2 + padding * 2 + width;`
`H = margin * 2 + border * 2 + padding * 2 + hight;`

**IE 中的盒子模型的宽：包括 margin + border + padding + width;**

`W = margin * 2 + width;`
`H = margin * 2 + height;`

**两者的区别**

- IE 盒子模型的 content 部分包含了 border 和 padding。

**那么应该选择哪种盒子模型呢？**

- 当然是“标准 w3c 盒子模型”了。
- 在网页顶部加上`doctype`声明,所有的浏览器都会采用标准的 w3c 盒子模型去解释你的盒子,网页就能在各个浏览器中显示一致了。

[:arrow_up:返回目录](#目录)

### CSS 所有选择器及其优先级、使用场景,哪些可以继承,如何运用 at 规则

#### 优先级是如何计算的？

优先级就是分配给指定的 CSS 声明的一个权重,它由匹配的选择器中的每一种选择器类型的数值决定。
而当优先级与多个 CSS 声明中任意一个声明的优先级相等的时候,CSS 中最后的那个声明会被应用到元素上。
当同一个元素有多个声明的时候,优先级才会有意义。因为每一个直接作用于元素的 CSS 规则总是会接管/覆盖(take over)该元素从祖先元素继承而来的规则。

> 选择器的类型
>
> 1. **类型选择器**(type selectors) (例如,h1)和**伪元素**(pseudo-elements) (例如,::before)
> 1. **类选择器**(class selectors) (例如,`.example`),**属性选择器**(attributes selectors) (例如,`[type="radio"]`),**伪类**(pseudo-classes) (例如,:hover)
> 1. **ID 选择器**(例如,`#example`)
> 1. **子选择器**（Child selector）
> 1. **后代（包含）选择器**（Descendant selector）使用**空格**,用于选择指定标签元素下的**后辈元素**
> 1. **相邻兄弟选择器**（Adjacent sibling selector）使用加号`+`。**E+F,匹配 E 元素之后的同级元素 F(直接相邻)**
> 1. **通用兄弟选择器** 使用波浪号`~`,比如**E~F,匹配 E 元素之后的所有同级元素 F(无论相邻与否)**
> 1. **通配符选择符**(universal selector) (\*),**关系选择符**(combinators) (`+`,`>`,`~`,'``')和**否定伪类**(negation pseudo-class) (`:not()`)对优先级没有影响。(但是,在**:not()内部声明**的选择器是会影响优先级的)。
> 1. 给元素添加的**内联样式**(例如,`style="font-weight:bold"`)总是会覆盖外部样式表的任何样式,因此可看作是具有最高优先级。

> 例外的`！important`规则
>
> 当在一个样式声明中使用一个`!important`规则时,此声明将覆盖任何其他声明。
> 使用`!important`是一个坏习惯,应该尽量避免,因为这破坏了样式表中固有的级联规则,使得调试找 bug 变得更加困难了。

#### 选择器的优先级

- css 样式的简单权重级别由高到低排列:
  - 在属性后面使用 !important 会覆盖页面内任何位置定义的元素样式。
  - 作为 style 属性写在元素标签上的内联样式
  - id 选择器
  - 类选择器、伪类选择器、属性选择器
  - 标签选择器、伪元素选择器
  - 通配符选择器
  - 浏览器自定义

#### 复杂场景下计算优先级

- 复杂场景下将选择器分为四个级别通过各级别的出现次数决定。
- 四个级别分别为：行内选择符、ID 选择符、类别选择符、元素选择符。
- 优先级的算法：
  - 每个规则对应一个初始"四位数"：0、0、0、0
  - 若是 行内选择符,则加 1、0、0、0
  - 若是 ID 选择符,则加 0、1、0、0
  - 若是 类选择符/属性选择符/伪类选择符,则分别加 0、0、1、0
  - 若是 元素选择符/伪元素选择符,则分别加 0、0、0、1
- 算法：将每条规则中,选择符对应的数相加后得到的“四位数”,从左到右进行比较,大的优先级更高。 优先级相同时,采用就近原则,即最后出现的样式。

#### 一些经验法则

- **一定**要优化考虑使用样式规则的优先级来解决问题而不是`!important`
- **只有**在需要覆盖全站或外部 CSS(例如引用 ExtJs 或者 YUI)的特定页面中使用`!important`
- **永远不要**在全站范围的 css 上使用`!important`
- **永远不要**在你的插件上使用`!important`

#### 类和 ID 选择器的使用场景

- 使用场景
  - class 重在样式的复用,重普遍性
  - id 重在划分样式区域,可以作为样式表中的命名空间来管理样式
  - id 也可以指定某一个特殊元素的样式,重特殊性

#### 哪些可以继承？

给父元素设置一些属性,子元素也可以使用,这个我们就称之为继承性

**注意点:**

1. 并不是所有的属性都可以继承
1. 不可继承的:display、margin、border、padding、background、height、min-height、max-height、width、min-width、max-width、overflow、position、left、right、top、bottom、z-index、float、clear、table-layout、vertical-align、page-break-after、page-bread-before 和 unicode-bidi
1. 所有元素可继承:visibility 和 cursor
1. 内联元素可继承:letter-spacing、word-spacing、white-space、line-height、color、font、font-family、font-size、font-style、font-variant、font-weight、text-decoration、text-transform、direction
1. 在 CSS 的继承中不仅仅是儿子可以继承,只要是后代都可以继承
1. 继承中的特殊性
   a 标签的文字颜色和下划线是不能继承的
   h 标签的文字大小是不能继承的
1. 终端块状元素可继承:text-indent 和 text-align
1. 列表元素可继承:list-style、list-style-type、list-style-position、list-style-image
1. 表格元素可继承：border-collapse

**应用场景**

一般用于设置网页上的一些共性信息,例如网页的文字颜色,字体,文字大小等内容 body{}

[:arrow_up:返回目录](#目录)

### CSS 伪类和伪元素有哪些,它们的区别和实际应用

#### 伪类(Pseudo-class)

一个 CSS 伪类(Pseudo-class)是一个以冒号(`:`)作为前缀,被添加到一个选择器末尾的关键字,当你希望样式在特定状态下才被呈现到指定的元素时,可以往元素的选择器后面加上对应的伪类(Pseudo-class)。

- 伪类
  - :active
    - CSS 伪类匹配被用户激活的元素
  - :any
    - any()伪类可以让您快速构建类似的选择器集合,通过建立包含所有包含项的组来匹配
  - :checked
    - 表示任何处于选中状态的 radio,checkbox, 或("select")元素中的 option HTML 元素("option")。
  - :default
    - 表示一组相关元素中的默认表单元素
  - :dir()
    - 匹配特定文字书写方向的元素
  - :disabled
    - 表示任何被禁用的元素。如果一个元素不能被激活,或获取焦点,则该元素处于被禁用状态。元素还有一个启用状态(enabled state),在启用状态下,元素可以被激活或获取焦点。
  - :empty
    - 代表没有子元素的元素,子元素只可以是元素节点或文本(包括空格)。注释或处理指令都不会产生影响。
  - :enabled
    - 表示任何启用的(enabled)元素,如果一个元素能够被激活,或获取焦点,则该元素是启用的。元素还有一个禁用状态,在被禁用时,元素不能被激活或获取焦点。
  - :first
    - @page :first 描述的是:打印文档时第一页的样式
    - 不能改变所有的 css 属性,只能改变 margins,orphans,widows,文档什么时候换页。别的所有 css 样式都会被忽略。
  - :first-child
    - 表示在一组兄弟元素中的第一个元素。
  - :first-of-type
    - 表示一组兄弟元素中其类型的第一个元素。
  - :fullscreen
    - 应用于当前处于全屏显示模式的元素。它不仅仅选择顶级元素,还包括所有已显示的栈内元素。
  - :focus
    - 表示获得焦点的元素。当用户点击或触摸元素或通过键盘"tab"键选择它时会被触发。
  - :hover
    - 适用于用户使用指示设备虚指一个元素的情况下。
    - 这个样式会被任何与链接相关的伪类重写,像:link,:visited,和"active 等。
    - 为了确保生效,:hover 规则需放在:link 和:visited 规则之后,但是在:active 规则之前。
    - :link->:visited->:hover->:active。
  - :indeterminate
    - 表示状态不确定的表单元素。
    - checkbox 元素,其 indeterminate 属性被 JavaScript 设置为 true。
    - radio 元素,表单中拥有相同的 name 值的所有单选按钮都未被选中时。
    - 处于不确定状态的 progress 元素。
  - :in-range
    - 给用户一个可视化的提示,表示输入域的当前值处于允许范围内。
    - 代表一个 input 元素,其当前值处于属性 min 和 max 限定的范围之内.
  - :invalid
    - 表示任意内容未通过验证的 input 或其他 form 元素。
  - :lang()
    - 基于元素语言来匹配页面元素。
    - :lang( `<language-code>` )
  - :last-child
    - 代表父元素的最后一个子元素
  - :last-of-type
    - 表示在(它父元素的)子元素列表中,最后一个给定类型的元素。
    - element:last-of-type { style properties }
  - :left
    - 需要和@规则 @page 配套使用,对打印文档的左侧页面设置 CSS 样式。
  - :link
    - 用来选中元素当中的链接。
    - 它将会选中所有尚未访问的链接,包括那些已经给定了其他伪类选择器的链接
    - 为了可以正确地渲染链接元素的样式,:link 伪类选择器应当放在其他伪类选择器的前面
  - :not(X)
    - 是一个简单的以选择器 X 为参数的功能性标记函数。
    - 它匹配不符合参数选择器 X 描述的元素。
    - X 不能包含另外一个否定选择器
    - 可以将一个或多个以逗号分隔的选择器作为其参数。选择器中不得包含另一个否定选择符或伪元素(尚未广泛推广)。
  - :nth-child(an+b)
    - 首先找到所有当前元素的兄弟元素,然后按照位置先后顺序从 1 开始排序,选择结果为第(an+b)个元素的集合。
      - 2n+1 表示 HTML 中的奇数
      - odd 表示 HTML 中的奇数
      - 2n 表示 HTML 中的偶数
      - even 表示 HTML 中的偶数
  - :nth-last-child()
    - 基本上和 :nth-child 一样,只是它从结尾处反序计数,而不是从开头处。
  - :nth-last-of-type()
    - 基本上和 :nth-of-type 一样,只是它从结尾处反序计数,而不是从开头处。
  - :nth-of-type()
    - 匹配文档树中在其之前具有 an+b-1 个相同兄弟节点的元素,其中 n 为正值或零值。
    - 这个选择器匹配那些在相同兄弟节点中的位置与模式 an+b 匹配的相同元素。
  - :only-child
    - 代表了属于某个父元素的唯一一个子元素。
    - 等效的选择器还可以写成:first-child :last-child
  - :only-of-type
    - 代表了任意一个元素,这个元素没有其他相同类型的兄弟元素
  - :optional
    - 表示任意没有 required 属性的 `<input>`,`<select>` 或 `<textarea>` 元素使用它。
  - :out-of-range
    - 表示输入域的当前值处于允许范围外
  - :read-only
    - 表示元素不可被用户编辑的状态
  - :read-write
    - 表示一个元素可以被用户编辑
  - :required
    - 表示任意 required 属性的 `<input>`,`<select>` 或 `<textarea>` 元素使用它。
    - 它允许表单在提交之前容易的展示必填字段并且渲染其外观
  - :right
    - 需要和@规则 @page 配套使用,对打印文档的右侧页面设置 CSS 样式。
  - :root
    - 匹配文档树的根元素。
    - 对于 HTML 来说,:root 表示`<html>`元素,除了优先级更高之外,与 html 选择器相同
  - :scope
    - 它将会匹配作为选择符匹配元素的参考点
  - :target
    - 代表一个唯一的页面元素(目标元素),其 id 与当前 url 片段匹配
  - :valid
    - 表示内容验证正确的`<input>`或其他`<form>`元素。
    - 这能简单地将校验字段展示为一种能够让用户辨别出其输入数据的正确性的样式。
  - :visited
    - 表示用户已访问过的链接。

#### 伪元素(Pseudo-element)

伪元素(Pseudo-element)跟伪类很像,但它们又有不同的地方。它们都是关键字,但这次伪元素前缀是两个冒号 ('`::`') , 同样是添加到选择器后面去选择某个元素的某个部分。

- ::after
  - 用来创建一个伪元素,作为已选中元素的最后一个子元素。
  - 通常会配合 content 属性来为该元素添加装式内容。
  - 这个虚拟元素默认是行内元素。
- ::before
  - 通常会配合 content 属性来为该元素添加装式内容。
  - 这个虚拟元素默认是行内元素。
- ::first-letter
  - 会选中块级元素第一行的第一个字母。
  - 文字所处的行之前没有其他内容
- ::first-line
  - 在某块级元素的第一行应用样式。
  - 第一行的长度取决于很多因素,包括元素的宽度,文档的宽度和文本的文字大小
- ::selection
  - 应用于文档中被用户高亮的部分(比如使用鼠标或其他选择设备选中的部分)
- ::backdrop
  - 在任何处于全屏模式的元素下的即刻渲染的盒子(并且在所有其他在堆中的层级更低的元素之上)

#### 两者的区别

1. CSS 伪类用于向某些选择器添加特殊的效果
   CSS 伪元素用于将特殊的效果添加到某些选择器
1. 伪类的效果可以通过添加一个实际的类来达到
   伪元素的效果则需要通过添加一个实际的元素才能达到
1. CSS3 明确规定伪类用一个冒号('`:`')来表示
   伪元素用两个冒号('`::`')来表示

[:arrow_up:返回目录](#目录)

### HTML 文档流的排版规则,CSS 几种定位的规则、定位参照物、对文档流的影响,如何选择最好的定位方式,雪碧图实现原理

#### 文档流(normal flow)

想像一下，什么是"流"？我们平常说的"水流"，"流体"，我们就可以把像河流那样长长的东西作为流。

那这里所指的文档流指的是什么呢？由于这是显示在浏览器上面，显示在电脑屏幕前的。如果我们将屏幕的两侧想象成河道，将屏幕的上面作为流的源头，将屏幕的底部作为流的结尾的话，那我们就抽象出来的文档流。

那文档流是什么呢？那就是元素！可以将屏幕显示中的内容都可以一一对应文档中的一个元素，在这里就引出两个概念：**内联元素**和**块级元素**

#### 块级元素和内联元素

> 块级元素:四四方方的块，在文档中自己占一行。如`<div>` `<p>`  
> 内联元素:(行内元素)多个内联元素,可以在一行显示。如`<span>` `<img>`

> 将**展现宏观**的元素设置成块(**相当宏大**)
> 将**修饰细节**的东西设置成行内元素(相对细微)

在《CSS 权威》中:内联元素始终以"行布局",意思是，始终以行的形式表现。

**在内联元素中回车符会被显示成为一个空格**

#### 块级元素和行内元素的转换

块级元素(block)和行内元素(inline)只要加上 display:block;或者是 display:inline 就可以转换了！

#### 脱离文档流

CSS 中有三种方式脱离文档流

```CSS
position:absolute
position:fixed
float
```

#### CSS 中的定位

- 静态定位
  - 静态定位是每个元素获取的默认值————他只是意味着"将元素放入它在文档布局流中的正常位置"。
  - position:static
- 相对定位
  - 它与静态定位非常相似，占据在正常的文档流中，可以修改他的最终位置(通过`top`,`left`,`right`,`bottom`)，也可以与页面上的其他元素重叠。
  - position:relative
- 绝对定位
  - 绝对定位的元素不再存在正常的文档布局流中。相反，它独立于一切坐在它自己的层。
  - 这意味着我们可以创建不干扰页面上其他元素的位置的隔离 UI 功能。
- 定位上下文
  - 哪个元素是绝对定位元素的"包含元素"？这取决于绝对定位元素的父元素 position 属性。
  - 我们可以改变**定位上下文**————绝对定位的元素的相对位置元素。通过设置其中一个父元素的定位属性————也就是包含绝对定位元素的那个元素(如果要设置绝对定位元素的相对元素，那么这个元素一定要包含绝对定位元素)。给包含元素设置`position:relative`。

#### CSS 雪碧图

> 雪碧图也叫 CSS 精灵，是一 CSS 图像合成技术

**CSS 雪碧图应用原理:**

其实就是 截取 大图一部分显示，而这部分就是一个小图

**优缺点**

- 优点:调用简单,维护方便，
- 缺点:请求文件过多，引发性能问题
  每个小图标都单独调用一图片，即意味着每个小图标的显示都产生一个 HTTP 请求，一般情况下每次创建一个 HTTP 请求，请求到的内容往往是次要的，性能代销主要在请求、以及响应阶段。

[:arrow_up:返回目录](#目录)

### 水平垂直居中的方案、可以实现 6 种以上并对比它们的优缺点

#### 行内元素水平、垂直居中

- 方案一:表格布局(不设置居中元素宽高)

```CSS
使用
display:table;
display:table-cell;
vertical-align:middle;
```

```HTML
 <!--html代码如下：-->
  <div class="panel-body line-align-center-one-content">
    <div class="line-align-center-one">
       <span class="mark-item">
          这里是测试的内容 Lorem ipsum dolor sit amet, consectetur adipisicing elite. Blate larum nibs unde vel. Ab accusantium distinctio ex ipsa necessitatibus. Dolorum facere impedit laudantium magni minima molestiae, nam quidem soluta veniam.
       </span>
    </div>
  </div>
```

```CSS
 /*css代码段*/
 .line-align-center-one-content{
   display: table;
   width: 100%;
 }
 .line-align-center-one{
   height: 400px;
   display: table-cell;
   vertical-align: middle;
   border: 1px solid #e4393c;
   text-align: center;
 }
 .mark-item{
   background: #ccc;
   color: #fff;
 }
```

- 方案二:使用绝对定位+位移(不设置元素宽高)

```HTML
<!--html代码段如下-->
 <div class="line-align-center-two">
    <span class="mark-two">
       这里是一个行内元素 Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aperiam exercitationem pariatur recusandae voluptate. Amet, animi architecto commodi cumque distinctio, dolorum eaque laborum modi molestiae mollitia nesciunt perferendis rem tenetur voluptate!
    </span>
 </div>
```

```CSS
  /*css代码段如下*/
  .line-align-center-two{
    position: relative;
    height: 400px;
    border: 1px solid #e4393c;
  }
  .mark-two{
    background: #ccc;
    color: #fff;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%) ;
  }
```
- 方案三:使用相对位移+位移+text-align:center(不设置居中元素宽高)

```HTML
 <-- html代码段如下-->
 <div class="line-align-center-three">
    <span class="mark-three">
       这里是一个行内元素
    </span>
 </div>
```

```CSS
  /*css代码段如下*/
  .line-align-center-three{
    height: 400px;
    border: 1px solid #e4393c;
    text-align: center;
  }
  .mark-three{
    position: relative;
    top: 50%;
    transform: translateY(-50%) ;
    background: #ccc;
    color: #fff;
  }
```
- 方案四:使用flex布局(不设置居中元素宽高)

```HTML
  <!--html代码-->
  <div class="line-align-center-four">
    <span class="mark-four">
      这里是一个行内元素 lorem
    </span>
  </div>
```

```CSS
  .line-align-center-four{
    display:flex;/*Flex布局*/
    justify-content: center;/*指定水平居中*/
    align-items:center;/*指定垂直居中*/
    height: 400px;
    border: 1px solid #e4393c;
  }
  .mark-four{
    background: #ccc;
    color: #fff;
  }
```

- 方案五:使用伪类(不设置居中元素宽高)

```HTML
  <!--html代码如下-->
  <div class="line-align-center-five">
    <span class="mark-five">
        这里是一个行内元素 Lorem
    </span>
  </div>
```

```CSS
  /*css代码如下*/
  .line-align-center-five {
    height: 400px;
    border: 1px solid #e4393c;
    text-align: center;/*水平居中*/
    font-size: 0;/*这一个很重要*/
  }
  .line-align-center-five:before {
    content: '';
    display: inline-block;
    vertical-align: middle;
    height: 100%;
  }
  .mark-five {
    font-size: 14px;
    display: inline-block;
    vertical-align: middle;
    background: #ccc;
    color: #fff;
    line-height: 26px;
  }
```
#### 块级元素,水平、垂直居中

块级元素的居中同样可以使用上述的行为元素的居中方案

**通用方案**

- 在已知容器和居中元素的宽高情况下，可以使用margin来调节元素居中
```HTML
<!--html如下-->
<div class="common-item">
  <div class="common-one">
    这里是内容区域，宽高100
  </div>
</div>
```

```CSS
 /*css代码如下：*/
 .common-item{
   height: 400px;
   border: 1px solid #e4393c;
 }
 .common-one{
   width: 100px;
   height: 100px;
   border:1px solid blue;
   margin: 150px auto 0;
 
 }
```

- 在已知居中元素的宽高尺寸的情况下，可以使用绝对定位或相对定位+margin负值实现

```HTML
 <div class="common-item-two">
   <div class="common-two">
     这里是内容区域，宽高100
   </div>
 </div>
```

```CSS
  .common-item-two{
    height: 400px;
    border: 1px solid #e4393c;
    position: relative;
  }
  .common-two{
    width: 100px;
    height: 100px;
    border:1px solid blue;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -50px;
    margin-left: -50px;
  }
```




[:arrow_up:返回目录](#目录)

### BFC 实现原理,可以解决的问题,如何创建 BFC

[:arrow_up:返回目录](#目录)

### 可使用 CSS 函数复用代码,实现特殊效果

[:arrow_up:返回目录](#目录)

### PostCSS、Sass、Less 的异同,以及使用配置,至少掌握一种

[:arrow_up:返回目录](#目录)

### CSS 模块化方案、如何配置按需加载、如何防止 CSS 阻塞渲染

[:arrow_up:返回目录](#目录)

### 熟练使用 CSS 实现常见动画,如渐变、移动、旋转、缩放等等

[:arrow_up:返回目录](#目录)

### CSS 浏览器兼容性写法,了解不同 API 在不同浏览器下的兼容性情况

[:arrow_up:返回目录](#目录)

### 掌握一套完整的响应式布局方案

[:arrow_up:返回目录](#目录)
