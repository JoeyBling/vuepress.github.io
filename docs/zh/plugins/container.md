---
sidebarDepth: 3
---

# vuepress-plugin-container <GitHubLink repo="vuepress/vuepress-plugin-container"/>

`vuepress-plugin-container` 是一个用于注册 markdown 容器的 VuePress 插件。

## 用法

### 全局安装

```bash
npm install -g vuepress-plugin-container
# 或者
yarn global add vuepress-plugin-container
```

### 局部安装

```bash
npm install vuepress-plugin-container
# 或者
yarn add vuepress-plugin-container
```

### 添加到 `config.js`

```js
module.exports = {
  plugins: [
    // 你可以多次使用这个插件
    // 因此我们推荐使用 babel-style
    ['container', {
      type: 'right',
      defaultTitle: '',
    }],
    ['container', {
      type: 'theorem',
      before: info => `<div class="theorem"><p class="title">${info}</p>`,
      after: '</div>',
    }],
  ]
}
```

```stylus
// index.styl
.theorem
  margin 1rem 0
  padding .1rem 1.5rem
  border-radius 0.4rem
  background-color #f0f4f8
  .title
    font-weight bold

.custom-block
  &.right
    color transparentify($textColor, 0.4)
    font-size 0.9rem
    text-align right
```

## 示例

**Input**

```md
::: theorem 牛顿第一定律
假若施加于某物体的外力为零，则该物体的运动速度不变。

::: right
From [维基百科](https://zh.wikipedia.org/wiki/%E7%89%9B%E9%A1%BF%E8%BF%90%E5%8A%A8%E5%AE%9A%E5%BE%8B)
:::
:::
```

**Output**

::: theorem 牛顿第一定律
假若施加于某物体的外力为零，则该物体的运动速度不变。

::: right
来自 [维基百科](https://zh.wikipedia.org/wiki/%E7%89%9B%E9%A1%BF%E8%BF%90%E5%8A%A8%E5%AE%9A%E5%BE%8B)
:::

## 配置

### type

- **类型:** `string`
- 这是一个必需的选项

容器的类型。举个例子，如果 `type` 被设置为 `foo`，则仅有下面的语法会被解析为 markdown 容器：

```md
::: foo bar
随便写点啥 ~
:::
```

### defaultTitle

- **类型:** `string`
- **默认值:** `type` 的大写形式

容器的默认标题。如果没有提供标题，则会使用 `defaultTitle` 作为容器的标题。

### localeTitle

- **类型:** `object`
- **默认值:** `{}`

容器在不同地区下的标题。它们会在使用对应语言时覆盖 `defaultTitle`。

### before

- **类型:** `string | Function`
- **默认值:** `undefined`

要插入在容器前的 HTML。如果设置为一个函数，将传入当前的 `info` 作为第一个参数。（在上面的例子中，`info` 的值为 `bar`。）如果设置了这个值，它将覆盖 `defaultTitle` 和 `localeTitle` 的效果。

### after

- **类型:** `string | Function`
- **默认值:** `undefined`

要插入在容器后的 HTML。如果设置为一个函数，将传入当前的 `info` 作为第一个参数。（在上面的例子中，`info` 的值为 `bar`。）如果设置了这个值，它将覆盖 `defaultTitle` 和 `localeTitle` 的效果。

### validate

- **类型:** `Function`
- **默认值:** `undefined`

一个用于判定容器是否结束的函数。当认定容器范围结束时应返回一个 `true`。

### render

- **类型:** `Function`
- **默认值:** `undefined`

容器开头和结束 token 的渲染函数。如果设置了这个值，它将覆盖 `before`, `after`, `defaultTitle` 和 `localeTitle` 的效果。

### marker

- **类型:** `string`
- **默认值:** `':'`

用于分隔符的字符。
