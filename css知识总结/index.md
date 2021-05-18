# CSS知识总结


# CSS知识总结

1. 浏览器渲染原理

   * 根据HTML构建HTML树（DOM）
   * 根据CSS构建CSS树（CSSOM）
   * 将两棵树合并成一颗渲染树（render tree)
   * layout布局（文档流、盒模型、计算大小和位置）
   * Paint绘制（把边框颜色、文字颜色、阴影等画出来）
   * Compose合成（根据层叠关系展示画面）
   * ![image-20210518134009118](/Users/vb/Library/Application Support/typora-user-images/image-20210518134009118.png)

2. CSS 动画的两种做法（transition 和 animation）

   * 使用两次transform，配合transition过渡

   * 使用animation

     声明关键帧

     添加动画

3. 总结

   css动画建议用animation，想要制作出好看的动画想象力必不可少，掌握常用属性，多次尝试，达到理想效果。


