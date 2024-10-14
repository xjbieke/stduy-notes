# CSS3 笔记

## 一、CSS 基础

### （一）简介

CSS（cascding style sheet，层叠式样式表）是用来给HTML标签添加样式的语言

CSS3是CSS的最新版本，增加了大量的样式，动画，3D特效和移动端特性等

CSS使样式和结构分离，样式和结构不用“杂糅着写”，而是彼此分开：HTML负责结构，CSS负责样式

HTML和CSS通过“选择器”为纽带来结合。

CSS的本质：CSS就是样式的“清单”，要书写合适的选择器，然后把指定元素的样式“一条一条罗列”出来。

**背诵CSS属性是非常重要的**，属性背诵熟练程度决定了做网页的速度

### （二）CSS3的书写位置

#### 1、内嵌式

- 内嵌在html文件中
- 在`<head></head>`标签对中，书写`<style></style>`标签对，里面书写CSS语句

#### 2、外链式

- 将CSS单独存为.css文件，然后使用`<link>`标签引入它
- `<link rel="stylesheet" href="css/css.css">`
- 外链式的优点：多个页面可以公用一个css样式表文件

#### 3、导入式

- 用@import指令引入，`<style>@import url(css/css.css)</style>`
- 导入式引入的样式表，不会等待css文件加载完毕，html结构会直接渲染。

#### 4、行内式（不推荐）

- 样式可以直接通过style属性写在标签身上 `<标签 style="属性:属性值;属性:属性值;">`
- 行内式牺牲了样式表的批量设置样式的能力

### （三）CSS3 的基本语法

```css
选择器{
    属性:属性值;
    属性:属性值;
    ......
}
```



css规则由两部分组成的：**选择器**与**大括号(样式规则)**

1. 选择器用于“给谁作用样式”。找到html文档中的标签对象，改变这个html标签的样式。
2. 样式规则用于之指定”作用什么样式“。
   - 样式规则由属性和属性值构成的kv键值对，可以有多个以;号分隔
   - 属性：找到的html文件中标签对象有什么属性就可以设置修改什么属性。
3. CSS3的注释是：/**/
   - VScode 快捷键：ctrl + / 单行，shift + alt + A 多行

### （四）html 元素的 4种CSS样式来源

- 浏览器默认样式
- 继承样式，后代元素继承祖先元素的样式，主要是文本有关的样式
- 观看网页用户通过浏览器自定义的样式
- 前端人员编写的指定样式

## 二、选择器

确定样式的作用范围

#### 命名规范

因为选择器除了标签选择器外，其他选择器都是自定义标识符（id、class 等）名称，所以必须有一定的命名规范。

- 只能以字母（字母都是小写）开头，后面可以有数字或中划线或下划线（不推荐）
- 中划线可以用来表示层级关系
- 层级嵌套4级时，考虑采用缩写
- 命名基本套路
  - 用模块的功能来命名 `modlename` 使用翻译软件将功能翻译成英文，尽量不要用缩写或拼音
  - 父子关系之间用中划线连接子元素的模块名称 `modlename-top`
  - 继续嵌套 `modlename-top-info` 及 `modlename-top-info-user`
  - 一般嵌套到4个级别时，可用缩写形式表示祖先再次嵌套 `mtiu-img`

常用命名：模块、元件

|  语义  |     命名     | 简写  |  语义  |   命名    | 简写 |
| :----: | :----------: | :---: | :----: | :-------: | :--: |
|  导航  |     nav      |  nav  | 子导航 |  subnav   | snav |
| 面包屑 |    crumb     |  crm  |  菜单  |   menu    | menu |
| 选项卡 |     tab      |  tab  |  排行  |    top    | top  |
| 标题区 |  head/title  | hd/tt |  登录  |   login   | log  |
| 内容区 | body/content | bd/ct |  标志  |   logo    | logo |
|  列表  |     list     | list  |  广告  | advertise |  ad  |
|  表格  |    table     |  tb   |  搜索  |  search   | sch  |
|  表单  |     form     |  fm   |  幻灯  |   slide   | sld  |
|  热点  |     hot      |  hot  |  提示  |   tips    | tips |
|  帮助  |     help     | help  |  新闻  |   news    | news |
|  下载  |   download   |  dld  |  注册  |  regist   | reg  |
|  投票  |     vote     | vote  |  版权  | copyright | cprt |
|  结果  |    result    |  rst  |  标题  |   title   |  tt  |
|  按钮  |    button    |  btn  |  输入  |   input   | ipt  |

常用命名：功能

|   语义   |        命名         | 简写 |   语义   |    命名     | 简写 |
| :------: | :-----------------: | :--: | :------: | :---------: | :--: |
| 清除浮动 |      clearfix       |  cb  |  左浮动  |  floatleft  |  fl  |
|   内联   |     inlineblock     |  ib  | 完全消失 | displaynone |  dn  |
| 文本居中 |   textaligncenter   | tac  | 字体大小 |  fontsize   |  fz  |
| 垂直居中 | verticalalignmiddle | vam  | 字体粗细 | fontweight  |  fs  |
| 溢出隐藏 |   overflowhidden    |  oh  |          |             |      |

常用命名：皮肤

|   语义   |      命名       | 简写 |   语义   |    命名     | 简写 |
| :------: | :-------------: | :--: | :------: | :---------: | :--: |
| 字体颜色 |    fontcolor    |  fc  | 边框颜色 | bordercolor | bdc  |
| 背景颜色 | backgroundcolor | bgc  |          |             |      |

常用命名：状态

| 语义   | 命名     | 简写 | 语义 | 命名           | 简写  |
| ------ | -------- | ---- | ---- | -------------- | ----- |
| 选中   | selected | sel  | 当前 | current/active | crt   |
| 显示   | show     | show | 隐藏 | hide           | hide  |
| 打开   | open     | open | 关闭 | close          | close |
| 出错   | error    | err  | 成功 | success        |       |
| 不可用 | disabled | dis  | 可用 | enabled        |       |

网易规范手册

- 命名方式（BEM）：类-体（例：`g-head`）、类-体-修饰符（例：`u-btn-active`）
- 相同语义的不同类命名方法：直接加数字或字母区分（如：`.m-list`、`.m-list2` 等，都是列表模块，但是是完全不一样的模块）。其他举例：`.f-fw0、.f-fw1、m-logo1、m-logo2`等等。

#### 选择器类型

##### 标签选择器

- 标签选择器也称元素选择器---div：通过元素名来选择作用范围，它直接使用元素的标签名当作选择器

  ```vue
  <template>
  	<div>
          <button>按钮</button>
      </div>
  </template>
  <style>
      button{
          background:black;
      }
  </style>
  ```

- 标签选择器将选择页面上所有该种标签，无论这个标签所处位置的深浅

- 标签选择器“覆盖面”非常大，所以通常用于标签的初始化

  ```css
  ul {
    /* 去掉无序列表的小圆点 */
    list-style: none;
  }
  a {
    /* 去掉超级链接的下划线 */
    text-decoration: none;
  }
  ```

##### 认识id属性

- 标签可以有 id 属性，是这个标签的唯一标识
- id 的名称只能由字母、数字、下划线、短横构成，且不能以数字开头，字母区分大小写
- 同一个页面不能有相同id的标签

##### id选择器

- ID选择器---#id：通过定义标签的id名称来精准选择指定id的标签，有唯一性

  ```vue
  <template>
  	<div>
          <button id="mybut">按钮</button>
      </div>
  </template>
  <style>
      #mybut {
          background:black;
      }
  </style>
  ```

##### class类名

- class 属性表示“类名”
- 类目的命名规范和id的命名规范相同

##### class类选择器

- 类选择器---.class：通过定义标签类名称来选择作用范围，非常灵活

- 一个标签可以同时属于多个类名，类目用空格隔开

- 多个标签素可以共用类名称

  

  ```vue
  <template>
  	<div>
          <button class="mybut">按钮</button>
      </div>
  </template>
  <style>
      .mybut {
          background:black;
      }
  </style>
  ```

##### 原子类

- 在做网页项目前，可以将所有的常用字号、文字颜色、行高、外边距、内边距等都设置为单独的类

  ```css
  .fs12{ font-size:12px;}
  .fs13{ font-size:13px;}
  .color-red {color:red;}
  .color-blue {color:blue;}
  ```

- html标签就i可以“则需选择”它的类名了，这样可以非常快速的添加一些常见样式

  ```html
  <p class="fs13 color-blue">显示信息</pp>
  ```

##### 属性选择器

- 属性选择器---[prop=value]：通过标签属性和对应的值来选择标签。

  ```css
  [href] { /* 选中所有拥有href属性的元素 */
      /* 样式规则 */
  }
  
  [href="https://baidu.com"] { /* 选中所有拥有href属性等于"https://baidu.com"的元素 */
      /* 样式规则 */
  }
  ```

##### 全局选择器

- 全局选择器---*

  ```css
  * { /* 选择页面中的所有元素添加边框 */
     border:2px solid #000
  }
  
  body * { /* 选中 body 下的所有元素添加边框 */
     border:2px solid #000
  }
  ```

#### 复合选择器

- 选择器可以任何搭配、结合，从而形成复合选择器，我们必须要能一目了然的看出选择器代表的含义

##### 并集选择器

- 并集选择器也叫分组选择器，逗号表示分组

  ```vue
  <template>
  <div>
      <p>
          ......
      </p>
      <a>.....</a>
  </div>
  </template>
  <style>
      p,a {/* 同时选择p标签和a标签 */
          font-size: 18px;
      }
  </style>
  ```

##### 交集选择器

- 多条件选择---多个选择，同一个标签，即满足多个条件的标签

  ```html
    <body>
      <p class="solid">我是第一段</p>
      <p class="dashed">我是第二段</p>
      <p class="solid dashed">我是第三段</p>
    </body>
  <style>
      .solid {
          background:pink;
      }
      .dashed {
          border: 2px solid #000;
      }
      /* 交集选择器 选中同时拥有solid类和dashed类的元素，选择器之间没有空格 */
      .solid.dashed {
          font-size: 22px;
      }
  </style>
  ```

##### 后代选择器

- CSS选择器中，使用空格表示“后代”

- “后代”并不一定是”儿子“

- 后代选择器可以有很多空格，隔开好几代

- 后代选择法可能是我们使用得最频繁得一中选择方式，因为它得逻辑非常简洁。

  ```html
  <p>
      <span>A</span>
      <span>B</span>
  </p>
  <foorer>
      <span>C</span>
      <span>D</sapan>
  </foorer>
  <style>
  /* 选择footer标签内的span标签 */
  footer span { border: 2px solid #000 }
  </style>
  ```

#### 伪类

- 伪类是添加到选择器的描述性词语，**指定要选择的元素的特殊状态**，超级链接拥有4个特殊状态

  | 伪类      | 意义                                             |
  | --------- | ------------------------------------------------ |
  | a:link    | 没有被访问的超级链接                             |
  | a:visited | 已经被访问过的超级链接                           |
  | a:hover   | 正被鼠标悬停的超级链接                           |
  | a:active  | 正被激活的超级链接（按下按建但是还没有松开按建） |

- 爱恨准则：a标签的伪类书写，要按照”爱恨准则“的顺序，否则会有伪类不生效

  **L**O**V**E **HA**TE：`:link -> :visited -> :hover -> :active`

##### 伪类---按元素状态指定样式

伪类（伪类选择器），起字面意思是“假的类”。

事实上，伪类选中的是元素的状态或外界的关系。

伪类的语法：

常规选择器 伪类 {}

```html
<div>
  <a href="www.baidu.com">百度</a>
</div>
<style>
    /* 当光标悬停在a标签上时的样式 */
  a:hover{border:2px solid #000}
</style>
```

1. :active---激活状态

   元素激活状态，在鼠标按键按下时触发，在鼠标按键抬起时还原。通常用于链接和按钮的点击反馈。

   ```html
   <button>
     按钮
   </button>
   <style>
     /* 鼠标按下按钮时的样式，松开后还原样式 */
     button:active{border:2px solid #000}
   </style>
   ```

2. :focus---聚焦状态

   元素聚焦状态，一般当鼠标单击输入框或Tab切换至输入框时触发。

   ```html
   <div>
     输入框：<input>
   </div>
   <style>
     /* 当鼠标单击输入框或Tab切换至输入框的样式 */
     input:focus{border:2px solid #000}
   </style>
   ```

3. :checked---勾选状态

   它用于表示<input type=checkbox>、<input type=radio>或<option>元素的勾选状态。

   ```html
   <input type="checkbox" checked>选项一
   <input type="checkbox" checked:false>选项二
   <style>
     [type="checkbox"]:checked {outline:2px solid #000}
   </style>
   ```

4. :disabled---禁用状态

   它作用于

#### 元素关系选择器

| 名称           | 举例   | 意义                          |
| -------------- | ------ | ----------------------------- |
| 子选择器       | div>p  | div的子标签p                  |
| 相邻兄弟选择器 | img+p  | 图片后面紧跟着的段落将被选中  |
| 通用兄弟选择器 | p~span | p元素之后的所有同层级span元素 |

##### 子选择器

当使用 > 符号分隔两个元素时，它只会匹配那些作为第一个元素的直接后代元素，即两个标签为父子关系

- 子选择---通过“爸爸”找“儿子”

  有时我们只想选中一个元素的所有子元素，而不是其中所有的元素（后代选择）时，采用子选择

  ```html
  <div id="grandpa">
    我是爷爷
    <div>
      我是爸爸
      <div>
        我是儿子
      </div>
    </div>
    <div>
      我是爸爸
      <div>
        我是儿子
      </div>
    </div>
  </div>
  <style>
    div { padding: 18px}
    #grandpa > div {border:2px solid #000}
  </style>
  ```

##### 相邻兄弟选择器

相邻兄弟选择器(+)介于两个选择器之间，当第二个元素紧跟在第一个元素之后，并且两个元素都是属于同一个父元素的子元素，则第二个元素将被选中

- 相邻兄弟选择---找同级的一个“弟弟”，

  有时我们希望基于现有元素选择同级的“下一个”元素

  ```html
  <span>哥哥</span>
  <span id="me">我</span>
  <span>弟弟</span>
  <span>弟弟</span>
  <style>
    #me + span {border:2px solid #000}
  </style>
  ```

##### 通用兄弟选择器

- 通用兄弟选择---找所有同级的“弟弟”

  ```html
  <span>哥哥</span>
  <span id="me">我</span>
  <span>弟弟</span>
  <span>弟弟</span>
  <style>
    #me ~ span {
      border:2px solid #000
    }
  </style>
  ```

#### 序号选择器

| 举例                 | 意义                  |
| -------------------- | --------------------- |
| :first-child         | 第一个子元素          |
| :last-child          | 最后一个子元素        |
| :nth-child(3)        | 第3个子元素           |
| :nth-of-type(3)      | 第3个某类型子元素     |
| :nth-last-child(3)   | 倒数第3个子元素       |
| :nth-last-of-type(3) | 倒数第3个某类型子元素 |

##### 属性选择器

| 举例                  | 意义                                             |
| --------------------- | ------------------------------------------------ |
| img[alt]              | 选择有alt属性的img标签                           |
| img[alt="故宫"]       | 选择alt属性是故宫的img标签                       |
| img[alt^="北京"]      | 选择alt属性以北京开头的img标签                   |
| img[alt$="夜景"]      | 选择alt属性以夜景结尾的img标签                   |
| img[alt*=”美"]        | 选择有alt属性中含有美字的img标签                 |
| img[alt~“手机拍摄”]   | 选择有alt属性中有空格隔开的手机拍摄字样的img标签 |
| img[alt\|="参赛作品"] | 选择有alt属性以“参数作品-”开头的img标签          |

#### CSS3新增伪类

| 伪类      | 意义                               |
| --------- | ---------------------------------- |
| :empty    | 选择空标签                         |
| :focus    | 选择当前获得焦点的表单元素         |
| :enabled  | 选择当前有效的表单元素             |
| :disabled | 选择当前无效的表单元素             |
| :checked  | 选择当前已经勾选的单选按钮或复选框 |
| :root     | 选择根元素，即<html>标签           |

#### 伪元素

- CSS3新增了“伪元素”特效，顾名思义，表示虚拟动态创建的元素
- 伪元素用双冒号表示，IE8可以兼容单冒号

##### ::before和::after

- ::before 创建一个伪元素，其将称为匹配选中的**元素的第一个子元素**，必须**设置 content 属性**表示其中的内容
- ::after创建一个伪元素，其将称为匹配选中的**元素的最后一个子元素**，必须**设置 content 属性**表示其中的内容

##### ::selection

- ::selection CSS伪元素应用于**文档中被用户高亮的部分（使用鼠标圈选的部分）**

##### ::first-letter和::first-line

- ::first-letter 会被选中某元素中（必须是块级元素）第一行的第一个字母
- ::first-line 会选中某元素中（必须是块级元素）第一行全部文字

#### 层叠性和选择器权重计算

- CSS全名叫做“层叠式样式表”，层叠性是它很重要的性质
- 层叠性：**多个选择器可以同时作用于同一个标签，效果叠加**

##### 层叠性的冲突处理

- 如果多个选择器定义的属性有冲突呢？CSS有严密的处理冲突的规则
  - id权重 > class权重 > 标签权重
  - id最大类名第二标签最小

##### 复杂选择器权重计算

- 复杂选择器可以通过（id的个数，class的个数，标签的个数）的形式，计算权重

##### !important提升权重

- 如果我们需要**将某个选择器的某条属性提升权重，可以在属性后面写!important**
- 很多公司不允许使用!important，因为这会带来不经意的样式冲突



#### 组合选择器总结：(需要牢记)

- 后代选择器通过空格分隔
- 子代选择器通过>号分隔
- 并集选择器通过逗号分隔
- 交集选择器紧挨着不分隔

## 三、文本与字体属性（熟记）

### （一）常用文本样式属性

#### 1、color 属性

color属性：设置文本内容的前景色，主要可以用英文单词、十六进制、rgb()、rgba()等表示法。

- 十六进制表示法
  - 是所有设计软件中都通用的颜色表示法，设计师我们的设计图上面标注的颜色，通常为十六进制表示。
  - `color:#ff0000`，6位2位分一组，三组分别代表光学像素器的红绿蓝，ff就是十进制的255，每种颜色分量都是0~255的数字。
  - 如果颜色值是#aabbcc的形式，可以简写为#abc。
  - 黑色是#000，白色是#fff，常见灰色有#ccc、#333、#2f2f2f等。
- rgb()表示法`color:rgb(255,0,0)`
- rgba()表示法，最后一个参数表示透明度介于0~1之间，0表示纯透明，1表示纯实心。

#### 2、font-size 属性

- font-size属性用来设置字号，单位通常为px，但还有em、rem单位。

- 网页文字正文字号通常是16px，浏览器最小支持10px字号

#### 3、font-weight 属性

- font-weight 属性设置字体的粗细程度，通常用normal和bold两个值

  | 示例                  | 意义                       |
  | --------------------- | -------------------------- |
  | font-weight: normal;  | 正常粗细，与400等值        |
  | font-weight: bold;    | 加粗，与700等值            |
  | font-weight: lighter; | 更细，大多数中文字体不支持 |
  | font-weight: bolder;  | 更粗，大多数中文字体不支持 |

#### 4、font-style 属性

- font-style 属性设置字体的倾斜

  | 示例                 | 意义                                                  |
  | -------------------- | ----------------------------------------------------- |
  | font-style: normal;  | 取消倾斜，比如可以把天生倾斜的i、em等标签设置为不倾斜 |
  | font-style: italic;  | 设置为倾斜字体（常用）                                |
  | font-style: oblique; | 设置为倾斜字体（用常规字体模拟，不常用）              |

#### 5、text-decoration 属性

- text-decoration 属性用于设置文本的修饰线外观的（下划线、删除线）

  | 示例                           | 意义       |
  | ------------------------------ | ---------- |
  | text-decoration: none;         | 没有装饰线 |
  | text-decoration: underline;    | 下划线     |
  | text-decoration: line-through; | 删除线     |


### （二）字体 属性详解

#### 1、font-family 属性

- font-family 属性用于设置字体，如：`font-family: "微软雅黑";`

- 字体可以是列表形式，一般英语字体放在前面，**后面的字体是前面的字体的 “后备” 字体**，如：`font-family: serif, "Times New Roman", "微软雅黑";`，字体名称中有空格及中文字体必须用引号包裹。

- 中文字体也可以称呼它门的英语名字

  | 中文字体名              | 等价的英语字体名               |
  | ----------------------- | ------------------------------ |
  | font-family: "微软雅黑" | font-family: “Microsoft Yahei” |
  | font-family: "宋体"     | font-family: "SimSun"          |

- 字体通常必须是用户计算机中已经安装好的字体，所以一般来说设置为微软雅黑和宋体较多，设置其他字体较少

#### 2、自定义字体

### （三）段落和行相关属性

#### 1、text-indent属性

text-indent 属性定义**首行文本内容之前的缩进量**，缩进两个字符应该写作，如：`text-indent: 2em;`，em表示字符宽度。

#### 2、line-height 属性

➢ line-height 属于用于**定义行高**，

- 单位可以是以px为单位的数值；如`line-height: 30px;`。
- 单位也可以没有单位的数值，表示字号的倍数；如`line-height: 1.5;`这是推荐写法。
- 单位还可以是百分数，表示字号的倍数；如`line-height: 150%;`

#### 3、text-align 属性

➢ text-align 属性用于**设置文本水平对齐方式**

- 取值：left（左对齐） center（居中） right（右对齐）
- text-align : center 能让那些元素居中
  -  文本、span标签、a标签、input标签、img标签
- 注意点：如果需要让文本水平居中，text-align属性给文本所在标签（文本的父元素）设置

#### 4、单行文本垂直居中

垂直居中：设置**行高=盒子高度**，即可以实现单行文本垂直居中，

#### 5、font 合写属性

font 属性可以用来作为font-style，font-weight，font-size，line-height和font-family属性的写

### （四）继承性

- 文本相关的属性普遍具有继承性，只要要给祖先标签设置，即可在后代所有标签中生效，有继承性的属性：

  - color

  - font- 开头的

  - list- 开头的

  - text- 开头的

  - line- 开头的

- 因为文字相关属性有继承性，所以通常会设置body标签的字号、颜色、行高等，这样就能当作整个网页的默认样式了

- 就近原则：在继承的情况下，选择器权重计算失效，而是“就近原则”。

  

## 四、盒模型

### （一）盒模型基本概念

#### 1、认识盒模型

➢所有HTML标签都可以看成矩形盒子，由width、height、padding、border构成，称为“盒模型”

- 盒子的总宽度 = width + 左右padding + 左右border
- 盒子的总高度 = height + 上下padding + 上下border

#### 2、width 和 height 属性详解

➢width 属性

- width 属性表示盒子**内容的宽度**
- **width 属性的单位通常是px**，移动端开发也涉及百分数、rem等单位
- **当块级元素（div、h系列、li等）没有设置width属性时，它将自动撑满**，但这并不意味着width可以继承

➢height 属性

- height 属性表示盒子**内容的高度**
- **height 属性的单位通常是px**，移动端开发也涉及百分数、rem等单位
- 盒子的height属性如果不设置，它将自动被其内容撑开，如果没有内容，则height默认是0

#### 3、padding 属性详解

- padding是盒子的内边距，即盒子边框内壁到文字的距离

- padding是四个方向的，可以分别用小属性进行设置

  | 小属性         | 意义      |
  | -------------- | --------- |
  | padding-top    | 上padding |
  | padding-right  | 右padding |
  | padding-bottom | 下padding |
  | padding-left   | 左padding |

- padding属性的四数值写法以空格隔开进行设置，分别表示上、右、下、左。

- padding属性的三数值写法以空格隔开进行设置，分别表示上、左右、下。

- padding属性的两数值写法以空格隔开进行设置，分别表示上下、左右。

#### 4、margin 属性详解

- margin是盒子的外边距，即盒子盒其他盒子之间的距离

- margin也有四个方向

  | 小属性        |                    |
  | ------------- | ------------------ |
  | margin-top    | 上margin，“向上踹” |
  | margin-right  | 右margin，“向右踹” |
  | margin-bottom | 下margin，“向下踹” |
  | margin-left   | 左margin，“向左踹” |

- **竖直方向的margin有塌陷现象**：小的margin会塌陷到大的margin中，从而margin不叠加，只以大值为准

- 一些元素（比如body、ul、p等）都有默认的margin，在开始制作网页的时候，要将他们清除。

  ```css
  /* 通配符选择器，选择所有元素 */
  * {
      margin: 0;
      padding: 0;
  }
  /* 通配符有效率问题，应该使用并集选择器 */
  body,ul,p {
      margin: 0;
      padding: 0;
  }
  ```

- 盒子的水平居中，将盒子左右两边的margin都设置为auto，如`.box { margin: 0 auto; }`，上下是0，左右自动。

- 文本居中是`text-align:center;`和盒子水平居中是两个概念

- 盒子的垂直居中，需要使用绝对定位技术实现

#### 5、盒模型计算

width与height的范围是给盒子内容使用的面积

盒子的总宽度是：width宽度+左右内边距+左右边框的总和

盒子的总高度是：height高度+上下内边距+上下边框的总和

#### 6、box-sizing 属性

- 将盒子添加了`box-sizing: border-box;`之后，盒子的width、height数字就表示盒子实际占有的宽高（不含margin）了，即 **padding、border 变为“内缩”的，不再“外扩”**
- **box-sizing 属性大量应用于移动网页制作中**，因为它结合百分比布局、弹性布局等非常好用，在PC页面开发中使用较少

### （二）行内元素和块级元素

#### 1、display 属性 

| display 属性类型 | 是否能并排显示 | 是否能设置宽度 | 当不设置width属性时 | 举例                                  |
| ---------------- | -------------- | -------------- | ------------------- | ------------------------------------- |
| 块级元素         | 否             | 是             | width自动撑满       | div、section、header、h系列、li、ul等 |
| 行内元素         | 是             | 否             | width自动收缩       | a、span、em、b、u、i等                |

➢行内块

- img和表单元素是特殊的行内块，它们既能够设置宽度高度，也能够并排显示

#### 2、行内元素和块级元素的相互切换

- 使用`display: block;`即可将元素**转为块级元素**

- 使用`display: inline;`即可将元素**转为行内元素**，将元素转为行内元素的应用不多见

- 使用`display: inline-block;`即可将元素**转为行内块**

#### 3、元素的隐藏

- 使用`display: none;`可以将元素隐藏，**元素将彻底放弃位置**，如同没有写它的标签一样
- 使用`visibility: hidden;`可以也可以将元素隐藏，**但是元素不放弃自己的位置**



## 五、浮动定位与背景样式

### （一）浮动

#### 1、浮动的基本概念

- 浮动的最本质功能：**用来实现并排**

- 浮动使用要点：**要浮动，并排的盒子都要设置浮动**

- **父盒子要有足够的宽度**，否则子盒子会掉下去

- 浮动的顺序贴靠特性：子盒子会按顺序进行贴靠，**如果没有足够空间，则会寻找再前一个兄弟元素**

- 浮动的元素一定能设置宽高：**浮动的元素不再区分块级元素、行内元素**，已经脱离了标准文档流，**一律能够设置宽高**，即使它是 span 或者 a 标签等
- `float: right;`即可设置右浮动，右浮动是反正进行的，从右向左排

#### 2、使用浮动实现网页布局

➢注意事项

- 垂直显示的盒子，不要设置浮动，<font color=red>**只有并排显示的盒子才要设置浮动！**</font>
- “大盒子带小盒子跑”，一个大盒子中，又是一个小天地，内部可以继续使用浮动
- div是免费的！不要节约盒子！

#### 3、BFC规范合浏览器差异

BFC规范：BFC（Box Formatting Context，**块级格式化上下文**）是页面上的一个**隔离的独立容器**，容器里面的子元素不会影响到外面的元素，反之亦然

➢ 创建BFC

- 方法一：float的值不是none
- 方法二：position的值不是static或者relative
- 方法三：display的值是inline-block、flex或者inline-flex
- 方法四：`overflow:hidden;`表示溢出隐藏，溢出盒子边框的内容将会被隐藏，它是**非常好用的让盒子形成BFC的方法**

➢ BFC的其他作用

- BFC可以取消盒子margin塌陷
- BFC可以阻止元素被浮动元素覆盖

➢ 浏览器差异

- IE6、7浏览器使用haslayout机制，和BFC规范略有差异，比如IE浏览器可以使用zoom:1属性“让盒子拥有layout”

- 如果要制作兼容到IE6、7的网页时，尽量让网页布局变得简单，内部有浮动的盒子要设置height属性，规范编程，不要“玩杂技”

#### 4、清除浮动

### （二）定位 position

#### 1、相对定位

- 相对定位：盒子可以相对自己原来的位置进行位置调整，称为相对定位。

  ```css
  position: relative;
  top : 100px; /* 从上向下移动100px，可以是负值则向反向移动 */
  left: 100px; /* 从左向右移动100px，可以是负值则向反向移动*/
  ```

- 相对定位元素，会在“老家留坑”，本质上仍然是在原来的位置，只不过渲染在新的地方而已，渲染的图形可以比喻成“影子”，不会对页面其他元素产生任何影响。


➢ 相对定位的用途

- 相对定位用来微调元素位置
- 相对定位的元素，可以当做绝对定位的参考盒子

#### 2、绝对定位

- 绝对定位：盒子可以在浏览器中**以坐标进行位置精准描述**，拥有自己的绝对位置

  ```css
  position: absolute;
  top: 100px;
  left: 100px;
  ```

- `position: absolute;`快捷键输入：poa

- 位置描述词：left到左边的距离；right到右边的距离；top到上边的距离；bottom到下边的距离

- 绝对定位的元素是脱离标准文档流的，将释放自己的位置，对其他元素不会产生任何干扰，而是对它们进行压盖

- 脱离标准文档流的方法：浮动、绝对定位、固定定位

- 绝对定位的盒子并不是永远以浏览器作为基准点

- 绝对定位的盒子会以**自己祖先元素中，离自己最近的拥有定位属性的盒子**，当做基准点。这个盒子通常是相对定位的，所以这个性质也叫作“子绝父相”

- 绝对定位的盒子垂直居中是一个非常实用的技术

  ```css
  positon: absolute;
  /*垂直居中，将元素定位到50%的位置再通过margin移动自身的一半的值，就可以居中*/
  top: 50%;
  margin-top: -自己高度的一半;
  /*水平居中，*/
  left: 50%;
  margin-left: -自己高度的一半;
  ```

- 绝对定位的元素堆叠顺序z-index属性是一个没有单位的正整数，用于设置绝对定位元素的压叠顺序，数值大的能够压住数值小的

- 绝对定位的用途：

  - 用来制作“压盖”、“遮罩”效果
  - 用来结合CSS精灵使用
  - 可以结合JS实现动画

#### 3、固定定位

- 固定定位：不管页面如何卷动，它永远固定在哪里

  ```css
  position: fixed;
  top: 100px;
  left: 100px;
  ```

- 固定定位只能以页面为参考点，没有子固父相这个性质

- 固定定位脱离标准文档流

- 固定定位的用途：“返回顶部”、“楼层导航”

### （三）边框与圆角

#### 1、边框

##### 1）边框的三要素

- 边框的线宽度、线型、线颜色称为边框的三要素，如：`border: 1px solid red;`
  - 常用线型：solid(实线)、dashed(虚线)、dooted(点状线)

- 边框三要素可以拆分为小属性

  | 小属性       | 意义   |
  | ------------ | ------ |
  | border-width | 线宽   |
  | border-style | 线型   |
  | border-color | 线颜色 |

##### 2）四个方向的边框

| 属性          | 意义   |
| ------------- | ------ |
| border-top    | 上边框 |
| border-right  | 右边框 |
| border-bottom | 下边框 |
| border-left   | 左边框 |

> 四个方向可以拆分为小属性，如：`border-top-color: red;`
>
> 去掉边框：`border-left: none;`即可去掉左边框

利用边框制作三角形：将盒子宽高设为零，线宽为三角形的高度，三角形的底的方向即为保留颜色边框，其他边框设置均为透明色tarnsparent

#### 2、圆角

`border-radius: 5px`设置元素的圆角，参数为圆弧半径值，当设为50%即为圆形

#### 3、盒子阴影

- 设置 boxshadow 属性：

  ```css
  box-shadow: 10px 20px 30px rgba(0,0,0,4);
  /* 
  * 第一个参数：x轴偏移量
  * 第二个参数：y轴偏移量
  * 第三个参数：模糊量，数字偏大时影子会向四周延展
  * 第四个参数：颜色，由于影子多采用半透明色，故常用rgba配色
  */
  ```

- 内阴影：box-shadow 属性值前加 inset 单词，表示内阴影

  ```css
  /* 添加 inset 即为设置内阴影 */
  box-shadow: inset 5px 5px 20px rgba(0, 0, 0, 9);
  ```

- 多阴影：box-shadow属性值可以用逗号隔开多个，表示携带多个阴影

  ```css
  box-shadow: 5px 5px 20px #f57d7d, 10px 10px 30px #a3ef9f,15px 15px 40px #6c93ee;
  /* 以逗号分隔可以设置多个阴影效果 */
  ```

### （四）背景与渐变

#### 1、背景基础知识

##### 1）背景颜色基础

- background-color 属性用来设置背景颜色
- 背景颜色可以用十六进制、rgb()、rgba()表示法表示
- padding区域是有背景颜色的

##### 2）背景基础知识

- background-image 属性用来设置背景图片，图片路径要写到ur()圆括号中，可以是相对路径，也可以是https://开头的绝对路径，例如：`background-image: url( image/bg001.jpg);`
- 如果样式表是外链的，那么要书写从CSS出发到图片的路径，而不是从html出发
- 需要等比例设置的值，写auto

#### 2、背景图片高级属性

##### 1）背景图片的重复模式

background-repeat属性用来设置背景图片的重复模式

| 值         | 意义               |
| ---------- | ------------------ |
| repeat;    | x、y均平铺（默认） |
| repeat-x;  | x平铺              |
| repeat-y;  | y平铺              |
| no-repeat; | 不平铺             |

##### 2）背景图片尺寸

- background-size 属性用来设置背景图片的尺寸，兼容到IE9

- `background-size: 100px 200px;`参数1:宽、参数2:高，值也可以用百分数来设置，表示为盒子宽、高的百分之多少
- 为了不让图片变形保留图片的原宽高比例，一般设置两个参数的其中一个，另一个赋值auto
- contain 和 cover 是两个特殊的 background-size 的值
  - contain 表示将背景图片只能改变尺寸以容纳到盒子里（盒子控件有可能填不满）
  - cover 表示将背景图片智能改变尺寸以撑满盒子（图片显示有可能会缺失）

##### 3）背景图片裁切

- background-clip 属性用来设置元素的背景裁切到那个盒子。兼容到IE9

  | 值          | 意义                                                         |
  | ----------- | ------------------------------------------------------------ |
  | border-box  | 背景延伸至边框（默认值）                                     |
  | padding-box | 背景延伸至内边(padding)，不会绘制到边框处（仅在dotted、dashed边框可察觉） |
  | content-box | 背景被裁剪至内容区                                           |

  ```css
  /* 背景起源 */
  background-origin: content-box;
  ```

##### 4）背景图片固定

- background-attachment 属性决定背景图像的位置是在视口内固定，或者随着包含它的区块滚动。

| 值     | 意义                                   |
| ------ | -------------------------------------- |
| fixed  | 自己滚动条不动，外部滚动条不动         |
| local  | 自己滚动条动，外部滚动条动             |
| scroll | 自己滚动条不动，外部滚动条动（默认值） |

##### 5）背景图片位置（定位）

- background-positon 属性可以设置背景图片出现在盒子的什么位置

  ```css
  background-position: 100px 100px;
  /*
  * 参数1：x轴方向位置
  * 参数2：y轴方向位置
  */
  ```

- 可以用top、bottom、center、left、right描述图片出现的位置

- 可以 center 使图片居中

  

##### ➢ CSS精灵

- CSS精灵：**将多个小图标合并制作到一张图片上，使用background-position属性单独显示其中一个**，这样的技术叫做CSS精灵技术，也叫作CSS雪碧图

- CSS精灵可以减少HTTP请求数，加快网页显示速度。缺点也很明显：不方便测量、后期改动麻烦

##### 6）background综合属性

一些常用的背景相关小属性，可以合写到一条 background 属性中

例如:`background: white url(images/archer.png) no-repeat center center;`

#### 3、渐变背景

##### 1）线性渐变

- 盒子的background-image 属性可以用linear-gradient()形式创建线性渐变背景

  ```css
  background-image: linear-gradient(to right, blue, red);
  /*
  * 第一个参数(right)：设置渐变方向，也可以写成度数50deg,deg度数单位
  * 第二个参数(blue)：设置开始颜色，可以有多个颜色值，并且可以用百分数定义它们出现的位置
  * 第三个参数(red)：设置结束颜色
  */
  background-image: linear-gradient(50deg, blue, yellow 20%, red);
  background-image: linear-gradient(to right, blue, green, yellow, orange, red);
  ```

- 浏览器私有前缀：不同浏览器有不同的私有前缀，用来对试验性质的CSS属性加以标识

  | 品牌     | 前缀     |
  | -------- | -------- |
  | chrome   | -webkit- |
  | firefox  | -moz-    |
  | IE、Edge | -ms-     |
  | 欧朋     | -o-      |

##### 2）径向渐变

- 盒子的background-image属性可以用radial-gradient()形式创建径向渐变背景，也就圆形的渐变

  ```css
  background-image: radial-gradient(50% 50%, red, blue)
  /*
  * 参数1：设置渐变圆心坐标x轴方向与y轴方向位置
  * 参数2... 设置渐变的颜色
  */
  ```

## 六、2D与3D转换

### （一）2D变形

#### 1、旋转变形

- 将 transform 属性的值设置为rotate()，即可实现旋转变形`transform: rotate(15deg)`

- 若角度为证，则顺时针方向旋转，否则逆时针方向旋转

➢ transform-origin属性

- 可以使用transform-origin属性设置旋转元素的基点位置，属性值可以是百分比、em、px等，默认值自身的原点。

  ```css
  transform-origin: 0 0; /*指定以图片的左上角为中心点旋转*/
  transform: rotate(30deg);
  
  transform-origin: 50% 0; /*指定图片顶边水平中心点为基点旋转*/
  transform-origin: 100% 50%; /*指定图片右边垂直中心点为基点旋转*/
  ```

#### 2、缩放变形

- 将 transform 属性的值设为scale()，即可实现缩放变形
- `transform: scale(3);`参数3：数字3表示缩放倍数，大于1为放大倍数，小于1为缩小倍数

#### 3、斜切变形

- 将 transform 属性的值设置为skew()，即可实现斜切变形
- `transfrom: skeew(10deg, 20deg);` 参数1:x斜切角度，参数2:y斜切角度

#### 4、位移变形

- 将 transform 属性的值设置为translate()，即可实现位移变形
- `transform: translate(100px, 200px);`参数1:向右移动的值，参数2:向下移动的值
- 和相对定位非常像，位移变形也会“老家留坑”，“形影分离”

### （二）3D变形

#### 1、3D旋转

- 将 transform 属性的值设置为rotateX()或者rotateY()，即可实现绕横轴、纵轴旋转

- `transform: rotateX(30deg);`绕横轴30度、`transform: rotateY(30deg);`绕纵轴30度

  ```css
  /* 横轴旋转  上部向后转*/
  transform: rotateX(50deg);
  /* 纵轴旋转  右边向后转*/
  transform: rotateY(30deg);
  /* 横轴纵轴同时旋转 */
  transform: rotateX(30deg) rotateY(30deg);
  ```

- 实现3D旋转效果需要在父元素内设置 perspective 属性

  ```css
  /* 实现元素3D旋转效果需要在旋转元素所在的父盒子内设置 perspective 属性 */
  perspective: 300px;
  ```

➢ perspective 属性

- perspective 属性是用来定义透视强度，可以理解为“人眼到舞台的距离”，单位是px
- 父元素是舞台需要设置perspective，旋转的元素是演员需要设置transform

#### 2、空间移动

- 当元素进行3D旋转后，即可继续添加translateX()、translateY()、translateZ()属性让元素在空间进行移动
- translateX()、translateY()、translateZ()是以当前的旋转面形成的坐标轴
- 一定记住，空间移动要添加在3D旋转之后
- 例如：`transfrom:rotateX(30deg) translateX(30deg) tranlateZ(30deg);`

➢ 制作一个正方体

- 正方体的每个面都是从舞台经过不同的3D旋转、空间移动到自己的位置的

## 七、过渡与动画

### （一）过渡

#### 1、过渡的基本使用

- transtion 过渡属性是CSS3浓墨重彩的特性，过渡可以**为一个元素在不同样式之间变化自动添加“补间动画”**

- transition 属性4个要素 

  ```css
  transition: width 1s linear 0s;
  /*
  * 参数1(要素1)：设定什么属性要过渡
  * 参数2(要素2)：设定动画时长，单位为秒(s),单位必须书写
  * 参数3(要素3)：设定变化速度曲线（缓动参数）
  * 参数4(要素4)：设定延迟时间
  */
  ```

- 所有数值类型的属性，都可以参与过渡，比如width、height、left、top、border-radius

#### 2、过渡的缓动效果

- transition 的第三个参数就是缓动参数，也是变化速度曲线
- 常用缓动参数
  - ease：两头慢中间快
  - linear：直线匀速变化
  - ease-in：开始慢后加速
  - ease-out：开始快后减速
  - ease-in-out：两头慢中间快，但中间部分相对于 ease 要平缓一些
- 缓动参数还可以使用：贝塞尔曲线
  - 网站https://cubic-bezier.com可以生成贝塞尔曲线，可以自定义动画缓动参数
  - 如：`transition: width 1s cubic-bezier(0.1,0.7,1.0,0.1) os;`

#### 3、过渡效果实战课

```css
/* 案例一 鼠标悬停图片上动态显示标题--过渡效果*/
* {
  margin: 0;
  padding: 0;
}
.box {
  width: 1200px;
  /* 溢出部分设为：隐藏 */
  overflow: hidden;
  margin: 50px auto;
}
.box ul {
  list-style: none;
}
.box ul li {
  float: left;
  width: 380px;
  margin-right: 20px;
  position: relative; /* 子绝父相 */
}
.box ul li img {
  width: 380px;
  height: 210px;
}
.info {
  position: absolute;
  width: 370px;
  height: 30px;
  line-height: 30px;
  padding-left: 10px;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  /* 透明度设置为0，不是背景的透明度，而是元素整体的透明度 */
  opacity: 0;
  /* 过渡 */
  transition: opacity 1s linear 0s;
}
/* 当li标签被触碰时，内部info盒子就透明度属性值变为1 */
.box ul li:hover .info {
  opacity: 1;
}
```

```css
/* 案例二 鼠标悬停动态旋转效果--过渡+2D变化*/
* {
  margin: 0;
  padding: 0;
}
.box {
  width: 508px;
  height: 107px;
  margin: 50px auto;
}
.box ul {
  list-style: none;
}
.box ul li {
  width: 107px;
  height: 107px;
  float: left;
  margin-right: 20px;
  position: relative; /* 子绝父相 */
}
/* 使用伪元素::before 设置图片背景 */
.box ul li::before { /* 有共性的属性 统一设置 */
  /* 伪元素一定要设置content属性 */
  content: '';
  /* 伪元素默认是行内元素，转为块元素来设置宽高 */
  display: block;
  width: 107px;
  height: 107px;
  /* 设置过渡 */
  transition: transform 1s linear 0s;
}
/* 分别设置背景图片 */
.box ul li:nth-child(1)::before {
  background-image: url('/imgs/a_1.png');
}
.box ul li:nth-child(2)::before {
  background-image: url('/imgs/a_2.png');
}
.box ul li:nth-child(3)::before {
  background-image: url('/imgs/a_3.png');
}
.box ul li:nth-child(4)::before {
  background-image: url('/imgs/a_4.png');
}
/* 采用绝对定位将svg图放入圈内 */
.box ul li img {
  position: absolute;
  width: 60px;
  height: 60px;
  top: 50%;
  left: 50%;
  margin-top: -30px;
  margin-left: -30px;
}
.box ul li:hover::before{
  /* 伪类元素旋转360度 */
  transform:rotate(360deg)
}
```

```css
/* 案例三 图片开门效果--过渡+3D变化 */
.box1 {
  width: 200px;
  height: 200px;
  margin: 50px auto;
  /* 3D变化，父元素必须设置 景深!!! */
  perspective: 1000px;
  position: relative; /* 子绝父相 */
}
.box1 img {
  width: 200px;
  height: 200px;
  border: 1px solid #616ee9;
  border-radius: 50%;
}
.box1 img.dog {
  /* 小狗图片绝对定位 */
  position: absolute;
  top: 0;
  left: 0;
  /* 设置小狗图片旋转的轴点 */
  transform-origin: 0 0;  /* 纵向左边为轴 */
  transition: transform 1s linear 0s;      
}
.box1:hover img.dog {
  /* 3D旋转 */
  transform: rotateY(-180deg);
} 
/* 第二个图，重新设置旋转轴 右旋转 */
.two img.dog {
  transform-origin: 100% 100%;
}
/* 第二个图，重新设置旋转方向 */
.two:hover img.dog {
  transform: rotateY(180deg);
}
/* 第三个图，重新设置旋转轴 右旋转 */
.three img.dog {
  transform-origin: 0 0;
}
/* 第三个图，重新设置旋转方向 */
.three:hover img.dog {
  transform: rotateX(180deg);
}
```

```css
/* 案例四 旋转的正方形--3D效果 */
section {
  width: 200px;
  height: 200px;
  margin: 100px auto;
  perspective: 11000px;  /*子绝父相*/
}
.box {
  width: 200px;
  height: 200px;
  /* 设置景深（透视强度） */
  perspective: 11000px;  /*子绝父相*/
  position: relative; 
  /* 设置变形类型，保留它内部的3D效果 */
  /* 这个盒子又是舞台，又是演员，这个box整体带着里面的p旋转 */
  transform-style: preserve-3d;
  transition: all 10s linear 0s;
}
section:hover .box {
  transform: rotateX(360deg) rotateY(360deg);
}
/*采用绝对定位使每个p标签都在基准位置*/
.box p {
  position: absolute;
  top: 0;
  left: 0;
  width: 200px;
  height: 200px; 
}
.box p:nth-child(1) {
  background-color: rgba(239, 192, 192, 0.349);
  /* 正面-->直接向回拉150px */
  transform: translateZ(100px);
}.box p:nth-child(2) {
  background-color: rgba(134, 232, 107, 0.349);
  /* 顶面-->先向后旋转90度-->之后向上移动100px */
  transform: rotateX(90deg) translateZ(100px);
  /*这里为什么是z呢，由于元素旋转，坐标系发生变化，正面应为Z方向*/      
}.box p:nth-child(3) {
  background-color: rgba(233, 75, 247, 0.349);
  /* 背面-->先向后旋转180度-->向后退100px */
  transform: rotateX(180deg) translateZ(100px);
}.box p:nth-child(4) {
  background-color: rgba(215, 132, 167, 0.349);
  /* 底面-->先向前旋转90度-->之后向回下移动100px */
  transform: rotateX(-90deg) translateZ(100px);
}.box p:nth-child(5) {
  background-color: rgba(239, 225, 34, 0.349);
  /* 左侧面-->先向前旋转90度-->之后移动100px */
  transform: rotateY(90deg) translateZ(100px);
}.box p:nth-child(6) {
  background-color: rgba(29, 124, 192, 0.349);
  /* 右侧面-->先向前旋转90度-->之后移动100px */
  transform: rotateY(-90deg) translateZ(100px);
}
```

### （二）动画

#### 1、动画的定义和调用

- 可以使用@keyframes来定义动画，keyframes表示“关键帧”，在项目上线前，要补上@-webkit-这样的私有前缀

  ```css
  /* 
  * 动画的定义
  * @keyframes是定义动画的关键字
  * name是动画的名字
  */
  /*基本的两帧动画*/
  @keyframes name {
      from { /* 起始状态 */
          transform: rotate(0);
      }
      to { /* 结束状态 */
          transform: rotate(360deg);
      }
  }
  /* 多帧动画 */
  @keyframes changeColor {
    0% {
  	background-color: red;
    }
    20% {
  	background-color: yellow;
    }
    40% {
  	background-color: blue;
    }
    60% {
  	background-color: green;
    }
    80% {
  	background-color: purple;
    }
    100% {
  	background-color: orange;
    }
  }
  ```

- 定义动画之后，就可以使用 animation 属性调用动画

  ```css
  /* 动画的调用 */
  animation: name 1s linear 0s;
  /* 
  * 参数1：动画名字
  * 参数2：总时长，单位秒
  * 参数3：缓动效果
  * 参数4：延迟时间，单位秒
  * 参数5：（非必须参数）动画的执行次数或对应的参数
  */
  ```

  ➢参数5对应的参数

  - 如果想让动画不要停，对应参数：infinite，如：`animation: name 2s linear 0s infinite`
  - 如果想让动画的第2、4、6...(偶数次)自动逆向执行，那么对应参数：alternate，在交替变化的应用非常实用，如：`animation: name 2s linear 0s alternate`
  - 如果想让动画停止在最后结束状态，那么对应参数：forwards，如：`animation: name 2s linear 0s forwards`

#### 2、动画效果实战

```css
/* 动画效果实例一 */
.dengpao {
  position: absolute;
  top: 200px;
  left: 200px;
}
.guang {
  position: absolute;
  top: 126px;
  left: 129px;
  opacity: 0;
  /* 设置动画 持续反复 */
  animation: light 0.5s linear 0s infinite alternate;
}
@keyframes light { /* 设置透明度制作闪光效果 */
  from {
	opacity: 0;
  }
  to {
	opacity: 1;
  }
}
```



## 八 、慕云游静态项目

### （一）项目起步准备

1. 创建 reset.css 文件，采用 YUI 3.5.0 reset.css 对项目重置，消除所有默认样式

   ```css
   /* YUI 3.5.0 reset.css */
   html{color:#000;background:#FFF}
   body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,
   pre,code,form,fieldset,legend,input,textarea,p,
   blockquote,th,td{margin:0;padding:0}
   table{border-collapse:collapse;border-spacing:0}
   fieldset,img{border:0}
   address,caption,cite,code,dfn,em,
   strong,th,var{font-style:normal;font-weight:normal}
   ol,ul{list-style:none}caption,th{text-align:left}
   h1,h2,h3,h4,h5,h6{font-size:100%;font-weight:normal}
   q:before,q:after{content:''}
   abbr,acronym{border:0;font-variant:normal}
   sup{vertical-align:text-top}
   sub{vertical-align:text-bottom}
   input,
   textarea,
   select{font-family:inherit;font-size:inherit;font-weight:inherit}
   input,textarea,select{*font-size:100%}legend{color:#000}
   #yui3-css-stamp.cssreset{display:none}
   ```

2. 创建公共类的 base.css文件 

   ```css
   /* BieKe 公共类 */
   /* 清除浮动 */
   .clearfix {
     overflow: hidden;  /*溢出内容不显示*/
   }
   /*伪类清除浮动：*/
   .cliearfix::after {
     content: '';       /*必要设置选项*/
     display: block;    /*以块级元素呈现*/
     clear: both;       /*清除元素两侧浮动*/
     overflow: hidden;  /*将元素隐藏*/
   }
   /* 文字水平居中 */
   .tac {
     text-align: center;
   }
   /* 盒子水平居中 */
   .center {
     margin: 0 auto;
   }
   /* 转为块级元素 */
   .db {
     display: block;
   }
   /* 转为行内块元素 */
   .dib {
     display: inline-block;
   }
   ```

3. 创建项目的css.css文件

4. 在主页中引入三个样式文件，做好项目起步工作

   ```html
   <link rel="stylesheet" href="css/reset.css">
   <link rel="stylesheet" href="css/base.css">
   <link rel="stylesheet" href="css/css.css">
   ```

### （二）页面顶部开发

#### 1. 页面顶部的开发

从网页的头部开始：有一个黑色的长条，在长条内部有一个居中的部分，这种是常见的布局形式，叫做通栏有版心，就是它贯穿了一个底色，但是内容是居中的。它需要两个盒子嵌套进行制作，外部盒子负责黑色背景内部盒子用来居中。

##### ➢ （1）自定义字体

```css
/* 自定义字体 */
@font-face {
  font-family: "PingFangSCRegular";
  src: url(../fonts/pingFangSCRegular.ttf) format('truetype');
}
/* 使用 */
body {
  font-family: 'PingFangSCRegular';
}
```

##### ➢ （2）坑点

- 当ul li 标签内有嵌套 ul li 标签时，例如弹出下拉栏，设置样式不能用后代选择器，应采用子代选择器>号 
- 导航条菜单右边有三角形图形附着，是通过设置padding留出位置，通过绝对定位放置的

导航条下拉菜单旁小箭头制作

##### ➢（3）导航条小箭头制作

通过两个盒子的叠加形成小箭头，一个盒子嵌套两个子盒子

```css
/* .arrow 为父盒子， b i 分别为子盒子 */
.site-head .topbar .shortcut-links > ul >li.have-menu .arrow {
  /* 为父盒子：绝对定位并居中 */
  position: absolute;
  right: 0;
  top: 50%;
  margin-top: -6px;
  width: 12px;
  height: 12px;
  transition: transform 0.5s ease 0s;
}
/* 子盒子 b、i：绝对定位让两个盒子旋转后形成错位，形成小箭头 */
.site-head .topbar .shortcut-links > ul >li.have-menu .arrow b {
  position: absolute;
  left: 3px;
  top: 2px;
  width: 6px;
  height: 6px;
  background-color: white;
  transform: rotate(45deg);
}
.site-head .topbar .shortcut-links > ul >li.have-menu .arrow i {
  position: absolute;
  left: 3px;
  top: 0px;
  width: 6px;
  height: 6px;
  background-color: #2a2a2a;
  transform: rotate(45deg);
/* 鼠标悬停时，箭头180旋转 */
}.site-head .topbar .shortcut-links > ul >li.have-menu:hover .arrow {
  transform: rotate(180deg);
}
```

#### 2. 字体图标的使用

在阿里巴巴矢量图标库选择收集要用的图标，下载代码引用

**（1）拷贝项目下面生成的 `@font-face`**

```css
@font-face {
  font-family: 'iconfont';
  src: url('iconfont.ttf?t=1679204586940') format('truetype');
}
```

**（2）定义使用 iconfont 的样式**

```css
.iconfont {
  font-family: "iconfont" !important;
  font-size: 16px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

**（3）挑选相应图标并获取字体编码，应用于页面**

```html
<span class="iconfont">&#x33;</span>
```

> "iconfont" 是你项目下的 font-family。可以通过编辑项目查看，默认是 "iconfont"。

#### 3.使用CSS制作菜单



页面中部开发

1.大Banner的布局

2.垂直菜单开发

3.新鲜甩尾部分开发

4.机酒自由行部分开发

5.当地玩乐部分开发

6.公共类的使用

7.过渡和变形在实战中的应用

页面底部开发



