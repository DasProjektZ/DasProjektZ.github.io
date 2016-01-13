---
layout: post
title:  "Using Jekyll and D3 to build our data visualization system"
categories: data
---

這幾天一直在進行jekyll的美化。
效果不好。
於是我準備把學習和實現的過程記錄下來。

## 方案

我們採用html來確定網頁的結構。

{% highlight html %}
<div class="container">
    <div class="header">这是头部</div>
    <div class="page clearfix">
        <div class="left">left sidebar</div>
        <div class="content">main content</div>
        <div class="right">right sudebar</div>
    </div>
    <div class="footer">footer section</div>
</div>
{% endhighlight %}

然後使用css或者css3來進行結構優化和美化。

{% highlight css %}
html,body{
  margin:0;
  padding:0;
  height:100%
}

.container{
  min-height:100%;
  height:auto !important;
  height:100%;/*ie6不识别min-height,如上述处理*/
  position:relative;
}

.header{
  background:#ff0;
  padding:10px;
}

.page{
  width:960px;
  margin:0 auto;
  padding-bottom:60px;/*padding等于footer的高度*/
}

.footer{
  position:absolute;
  bottom:0;
  width:100%;
  height:60px;/*footer的高度*/
  background:#6cf;
  clear:both;
}

.left{
  width:220px;
  height:800px;
  float:left;
  margin-right:20px;
  background:lime;
}

.content{
  background:orange;
  width:480px;
  float:left;
  margin-right:20px;
}

.right{
  width:220px;
  float:right;
  background:green;
}

.clearfix:after,
.clearfix:before{content:"";display:table}
.clearfix:after{clear:both;overflow:hidden}
.clearfix{zoom:1;}
{% endhighlight %}

實現這頁腳永遠固定在頁面的底部，我們只需要四個`div`，其中`div#container`是一個容器，在這個容器之中，我們包含了`div#header`(頭部)，`div#page`(頁面主體部分，我們可以在這個`div`中增加更多的`div`結構，如上面的代碼所示)，`div#footer`(頁腳部分)。

### 實現原理和解釋

**`<html>`和`<body>`標籤**：`html`和`body`標籤中必須將高度(height)設置為「100%」,這樣我們就可以在容器上設置百分比高度，同時需要將`html`,`body`的`margin`和`padding`都移除，也就是`html`,`body`的`margin`和`padding`都為0；

**`div#container`容器**：`div#container`容器必須設置一個最小高度(`min-height`)為100％；這主要使他在內容很少(或沒有內容)情況下，能保持100％的高度，不過在IE6是不支持`min-height`的，所以為了兼容IE6，我們需要對`min-height`做一定的兼容處理，具體可以看前面的代碼，另外我們還需要在`div#container`容器中設置一個`position:relative`以便於裡面的元素進行絕對定位後不會跑了`div#container`容器；

**`div#page`容器**：`div#page`這個容器有一個很關鍵的設置，需要在這個容器上設置一個padding-bottom值，而且這個值要等於(或略大於)頁腳`div#footer`的高度(height)值，當然你在`div#page`中可以使用border-bottom人水-width來替代padding-bottom，但有一點需要注意，此處你千萬不能使用margin-bottom來代替padding-bottom，不然會無法實現效果；

**`div#footer`容器**：`div#footer`容器必須設置一個固定高度，單位可以是px(或em)。
`div#footer`還需要進行絕對定位，並且設置`bottom:0`；讓`div#footer`固定在容器`div#container`的底部，這樣就可以實現我們前面所說的效果，當內容只有一點時，`div#footer`固定在屏幕的底部(因為`div#container`設置了一個`min-height:100%`)，當內容高度超過屏幕的高度，`div#footer`也固定在`div#container`底部，也就是固定在頁面的底部。
你也可以給`div#footer`加設一個`width:100%`，讓他在整個頁面上得到延伸；

**其他div**：至於其他容器可以根據自己需求進行設置，比如說前面的`div#header`,`div#left`,`div#content`,`div#right`等。

### 优点：

結構簡單清晰，無需js和任何hack能實現各瀏覽器下的兼容，並且也適應iphone。

### 缺點：

不足之處就是需要給`div#footer`容器設置一個固定高度，這個高度可以根據你的需求進行設置，其單位可以是px也可以是em，而且還需要將`div#page`容器的`padding-bottom`(或`border-bottom-width`)設置大小等於(或略大於)`div#footer`的高度，才能正常運行。
