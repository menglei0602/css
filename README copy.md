# CSS规则

## 术语

### 规则声明
“规则声明”是赋予一个选择器（或一组选择器）以及一组属性的名称。这是一个例子：
```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```
### 选择器
在规则声明中，“选择器”是确定 DOM 树中哪些元素将由定义的属性设置样式的位。选择器可以匹配 HTML 元素，以及元素的类、ID 或其任何属性。以下是选择器的一些示例：
```css
.my-element-class {
  /* ... */
}
[aria-hidden] {
  /* ... */
}
```
### 特性
最后，属性赋予规则声明中选定的元素其样式。属性是键值对，规则声明可以包含一个或多个属性声明。属性声明如下所示：

```css
/* some selector */ {
  background: #f1f1f1;
  color: #333;
}
```

## CSS

### 格式化
* 使用软制表符（2 个空格）进行缩进。
* 在类名中优先使用破折号而不是驼峰式命名。
  如果您使用 BEM，下划线和 PascalCasing 是可以的（请参阅下面的OOCSS 和 BEM）。
* 不要使用 ID 选择器。
* 在规则声明中使用多个选择器时，为每个选择器指定自己的行。
* 在规则声明中的左大括号之前放置一个空格{。
* 在属性中，在字符后面而不是前面放置一个空格:。
* 将规则声明的右大括号放在}新行上。
* 在规则声明之间放置空行。

**坏的**
```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```
**好的**
```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```
### 评论
* 能用行注释（//在 Sass-land 中）就不用块注释。

### OOCSS 和 BEM
出于以下原因，我们鼓励 OOCSS 和 BEM 的某种组合：

* 它有助于在 CSS 和 HTML 之间创建清晰、严格的关系
* 它帮助我们创建可重用、可组合的组件
* 它允许更少的嵌套和更低的特异性
* 它有助于构建可扩展的样式表

**OOCSS**

OOCSS或“面向对象的 CSS”是一种编写 CSS 的方法，它鼓励您将样式表视为“对象”的集合：可在整个网站中独立使用的可重用、可重复的片段来增强CSS代码的可维护性和重用性的方法论。

**BEM**
BEM或“块元素修饰符”是HTML 和 CSS 中类的命名约定，考虑到了大型代码库和可扩展性，并且可以作为实施 OOCSS 的一套可靠指南。

推荐使用 PascalCased“块”的 BEM 变体，与组件（例如 React）结合使用时效果特别好。下划线和破折号仍然用于修饰符和子元素。

**例子**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```
```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```
 * .ListingCard是“块”并代表更高级别的组件
 * .ListingCard__title是一个“元素”，代表它的后代，.ListingCard有助于将块组成一个整体。
 * .ListingCard--featured是一个“修饰符”，代表块上的不同状态或变化.ListingCard。

## ID选择器
尽量避免在css中使用ID选择器：虽然可以在 CSS 中通过 ID 选择元素，但它通常应被视为反模式。ID 选择器为您的规则声明引入了不必要的高水平特异性，并且它们不可重用。

## JavaScript 钩子
避免在 CSS 和 JavaScript 中绑定到同一个类。将两者混为一谈通常会导致开发人员在重构过程中浪费时间，因为开发人员必须交叉引用他们正在更改的每个类，而最糟糕的是，开发人员因担心破坏功能而不敢进行更改。

我们建议创建要绑定的特定于 JavaScript 的类，前缀为.js-：

<button class="btn btn-primary js-request-to-book">Request to Book</button>

### 变量
优先使用破折号命名的变量名称（例如$my-variable），而不是驼峰命名或蛇形命名的变量名称。可以在仅在同一文件中使用的变量名前添加下划线（例如$_my-variable）。

### 混入
Mixins 应该用于干燥代码、增加清晰度或抽象复杂性——就像命名良好的函数一样。不接受参数的 Mixin 对此很有用，但请注意，如果您不压缩有效负载（例如 gzip），这可能会导致结果样式中出现不必要的代码重复。
--todo
### 扩展指令
@extend应避免使用，因为它具有不直观且潜在危险的行为，尤其是与嵌套选择器一起使用时。如果选择器的顺序后来发生变化（例如，如果它们位于其他文件中并且文件加载的顺序发生变化），即使扩展顶级占位符选择器也可能会导致问题。Gzipping 应该可以处理您通过使用 获得的大部分节省@extend，并且您可以使用 mixin 很好地干燥您的样式表。
--todo

### 嵌套选择器
选择器的嵌套深度不要超过三层！
```css
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```
永远不要嵌套 ID 选择器：如果您发现自己这样做，则需要重新审视您的标记，或者弄清楚为什么需要如此强的特异性。如果您正在编写格式良好的 HTML 和 CSS，则永远不需要这样做。
