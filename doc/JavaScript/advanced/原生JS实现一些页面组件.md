[TOC]

## 1. tab切换表单效果

使用原生JS来实现点击tab实现显示对应内容的效果：

```html
<style>
    .tab ul, .tab li {
        list-style: none; margin: 0; padding: 0;
    }
    .tab {
        border: 1px solid #ccc; border-top: none;
    }
    .tab .tab-header::after {
        content: ''; display: block; clear: both;
    }
    .tab .tab-header > li {
        float: left; border: 1px solid #ccc;
        width: calc(25% - 2px);
        text-align: center;
        line-height: 30px; cursor: pointer;
    } 
    .tab .tab-header > li.active {
        background-color: #ccc; color: #fff;
    }
    .tab .tab-container > li {
        display: none; height: 100px; padding: 10px;
    }
    .tab .tab-container > li.active { display: block; }
</style>
<div class="tab">
    <ul class="tab-header">
        <li>HTML</li>
        <li class="active">CSS</li>
        <li>Javascript</li>
        <li>Http</li>
    </ul>
    <ul class="tab-container">
        <li> <p>HTML 的内容</p> </li>
        <li class="active"> <p>CSS 的内容</p> </li>
        <li> <p>Javascript 的内容</p> </li>
        <li> <p>Http 的内容</p> </li>
    </ul>
</div>
<script>
    var tabHeaders = document.querySelectorAll('.tab .tab-header>li')
    var tabPanels = document.querySelectorAll('.tab .tab-container>li')
    tabHeaders.forEach(function(tab){
        tab.onclick = function() {
            tabHeaders.forEach(function(node){
                node.classList.remove('active')
            })
            this.classList.add('active')
            var index = Array.prototype.indexOf.call(tabHeaders, this)
            tabPanels.forEach(function(node){
                node.classList.remove('active')
            })
            tabPanels[index].classList.add('active')
        }
    })  
</script>
```

