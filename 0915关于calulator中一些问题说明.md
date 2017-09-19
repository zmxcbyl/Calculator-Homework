# 问题1：为什么我画出来的按钮那么丑，那么小一个按钮，外面还有一个框框

* 这个问题要分两部分回答，但是核心就是，你就是这么给他写样式的

* 首先先说按钮，简单的说就是代码里不存在规定button样式的css代码，所以系统就用默认样式了

* 然后说外面一个框框，外面的框框是button外面的div的样式啊，我把相关的代码摘出来

        <!-- 先摘出来html部分的代码 -->
        <div class="button_one">
            <button type="button">7</button>
        </div>

        /** 然后摘出来css的部分 */
        .button_one{
            width: 70px ;
            height: 70px ;
            margin: 5px ;
            padding : 5px ;
            border: 1px solid #C1BBBB ; /* 这个样式就是外面那个框框 */
            float: left ;
        }

* 说一下一些调试样式的技巧，chrome - f12 打开调试台，查看自己感觉有异常的元素，查看钙元素上的绑定的css，这样有利于进行调试

# 问题2：为什么那天画按钮的时候前几行按钮也在外面套了框框，我这样没套框框也实现了，但是后面画等号的时候出了问题

* 等于号的故事回来再说，先说前两行的情况。慢慢说，我们现在对于按钮的布局使用的是float：left，通过控制.button_one这个框框的宽度和这些框框的父级元素的宽度实现换行的。也就是说，如果我们外面的框框因为某种因素变化了，那么我们不一定能实现在我们希望的地方进行换行。

* 现在解释为什么我会选择在第一行的四个按钮的框框之外又套了一行叫.row的框框。因为有时候，我们不希望随着外面框框导致我们的元素换行的位置变化了，所以我们干脆用框框给他框起来，这样在调整样式的时候，不容易出现问题

# 问题3：

* 严格的说，出现这个问题的原因是以为样式书写不规范导致的，我不太会解释因为有float：left和没有float：left的元素扔在一起会发生怎么样的情况，记住规则：同一层级的block元素，如果需要进入浮动层，需要float：left，那么请全部float：left，如果不需要，则请全部取消float：left

* 我们聊一下细节，首先我们给每个框框起个名字，先把后两行代码贴出来

        <div class="row5_l">  <!-- “左面大框” -->
            <div class="button_one">
                <button type="button">1</button>
            </div>
            <div class="button_one">
                <button type="button">2</button>
            </div>
            <div class="button_one">
                <button type="button">3</button>
            </div>
            <div>   <!-- "零点大框" -->
                <div class="button_zero"> <!-- “” -->
                    <button type="button">0</button>
                </div>
                <div class="button_one">
                    <button type="button">.</button>
                </div>
            </div>
        </div>
        <!-- 画等号 -->
        <div class="row5_r"> <!-- "右面大框" -->
            <div class="button_result">
                <button type="button">=</button>
            </div>
            <div style="clear:both"></div>
        </div>

* 首先说一下现在代码中的情况，首先“左面大框”是在浮动层中的，“右面大框”是不再浮动层的（这个怀疑css名字写错了，毕竟有一个叫.row_r但是没有被用到的样式）， “零点大框”之前的几个按钮框框是在浮动层的，但是零点大框不是浮动层

* 仔细研究了一下，依然懒得解释为什么会出现现在这个情况，有点眩晕，不太懂