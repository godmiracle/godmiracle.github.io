# Html常用标签


# 常用标签

1. a标签的用法

   **HTML `<a>` 元素**（或称锚元素）可以通过[它的 `href` 属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a#href)创建通向其他网页、文件、同一页面内的位置、电子邮件地址或任何其他 URL 的超链接。`<a>` 中的内容**应该**应该指明链接的意图。如果存在[ `href` 属性](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a#href)，当 `<a>` 元素聚焦时按下回车键就会激活它。

   ```html
   <a href=""></a>
   ```

2. img标签的用法

   **HTML `<img>` 元素**将一份图像嵌入文档。

   ```html
   <img src="" alt="">
   ```

   * `src` 属性是**必须的**，它包含了你想嵌入的图片的文件路径。
   * `alt` 属性包含一条对图像的文本描述，这不是强制性的，但对可访问性而言，它**难以置信地有用**——屏幕阅读器会将这些描述读给需要使用阅读器的使用者听，让他们知道图像的含义。如果由于某种原因无法加载图像，普通浏览器也会在页面上显示`alt` 属性中的备用文本：例如，网络错误、内容被屏蔽或链接过期时

3. table标签的用法

   **HTML**的 **`table`** 元素表示表格数据 — 即通过二维数据表表示的信息。

   ```html
   <table>
       <thead>
       <tr>
           <th colspan="2">The table header</th>
       </tr>
       </thead>
       <tbody>
       <tr>
           <td>The table body</td>
           <td>with two columns</td>
       </tr>
       </tbody>
   </table>
   ```

4. 其他感想

   标签可用的属性很多，但常用的就那几个。


