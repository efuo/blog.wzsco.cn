---
title: 网站缩略图生成器
date: 2024-02-18 17:56:56
---

<div align="center">
    <h1>网站缩略图生成器</h1>

</div>

<style>
.tijiaoform {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin-top: 20px;
}

.tijiaoform input,
.tijiaoform select {
    width: 300px;
    height: 40px;
    margin-bottom: 10px;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
    margin-right: 10px;
}

.tijiaoform input[type="button"] {
    background-color: var(--sco-maskbg);
    cursor: pointer;
    transition: all .3s;
}

.tijiaoform input[type="button"]:hover {
    background-color: var(--sco-main);
    transition: all .3s;
    color: var(--sco-white);
}

.wrapper {
    width: 80vh;
    margin: 40px auto;
    height: 60vh;
    overflow: hidden;
}

.wrapper iframe{
    transform-origin: top left;
    margin: 0;
    padding: 0;
    position: relative;
}

.display {
    position: relative;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: var(--sco-maskbg);
}

.mobile, .tablet, .desktop , .laptop {
    position: absolute;
}

.mobile {
    z-index: 4;
    background: center / contain no-repeat;
    background-image: url('https://p.wzsco.top/919f3fa7ae27ea6a327bbb7b741c2d91.png/cover');
    position: absolute;
    width: 130px;
    height: 268px;
    top: 40vh;
    left: 55vh;
}

.mobile iframe {
    border-radius: 45px;
    width: 360px;
    height: 777px;
    top: 13.5px;
    left: 9px;
    transform: scale(0.310);
}

.tablet {
    width: 246px;
    height: 400px;
    z-index: 3;
    position: absolute;
    left: 60vh;
    top: 32vh;
    background: center / contain no-repeat;
    background-image: url('https://p.wzsco.top/918c9ac42232209f0ca95928c0596a0c.png/cover');
    z-index: 3;
}

.tablet iframe {
    border-radius: 20px;
    left: 10.5px;
    top: 50px;
    width: 823px;
    height: 1100px;
    transform: scale(0.273);
    transform-origin: top left;
}

.laptop {
    width: 600px;
    height: 550px;
    top: 25vh;
    left: 2.5vh;
    background: center / contain no-repeat;
    background-image: url('https://p.wzsco.top/788a973ac3ef2abc6d7ab175c0907b89.png/cover');
    z-index: 2;
}

.laptop iframe {
    border-radius: 15px 15px 0 0;
    left: 54px;
    top: 101px;
    width: 1600px;
    height: 1034px;
    transform: scale(0.308);
    transform-origin: top left;
}

.desktop {
    width: 900px;
    height: 650px;
    top: 2vh;
    left: 7vh;
    background: center / contain no-repeat;
    background-image: url('https://p.wzsco.top/c513367eb192752eeb6086add4566da6.png/cover');
    z-index: 1;
}

.desktop iframe {
    left: 23px;
    top: 11px;
    width: 2772.5px;
    height: 1563px;
    transform: scale(0.308);
    transform-origin: top left;
}

.hide-title {
    color: var(--sco-red);
    display: none;
}

@media (max-width: 1800px) {
    .display, .desktop, .laptop, .tablet, .mobile {
        transform: scale(0.8);
    }

    .desktop {
        left: 4vh;
        top: -1vh;
    }

    .laptop {
        left: -1vh;
        top: 22vh;
    }

    .tablet {
        left: 59vh;
        top: 29vh;
    }

    .mobile {
        left: 55vh;
        top: 37vh;
    }
}
@media (max-width: 1600px) {
    .display, .desktop, .laptop, .tablet, .mobile{
        transform: scale(0.7);
    }

    .desktop {
        left: -1vh;
        top: -4vh;
    }

    .laptop {
        left: -5vh;
        top: 19vh;
    }

    .tablet {
        left: 58vh;
        top: 27vh;
    }

    .mobile {
        left: 55vh;
        top: 36vh;
    }
}

@media (max-width: 1400px) {
    .display, .desktop, .laptop, .tablet, .mobile{
        transform: scale(0.6);
    }

    .desktop {
        left: -8.5vh;
        top: -8vh;
    }

    .laptop {
        left: -10vh;
        top: 14vh;
    }

    .tablet {
        left: 56vh;
        top: 23vh;
    }

    .mobile {
        left: 54vh;
        top: 33vh;
    }
}

@media (max-width: 1200px) {
    .display, .desktop, .laptop, .tablet, .mobile{
        transform: scale(0.5);
    }

    .desktop {
        left: -12vh;
        top: -12vh;
    }

    .laptop {
        left: -15vh;
        top: 9vh;
    }

    .tablet {
        left: 54vh;
        top: 19vh;
    }

    .mobile {
        left: 52vh;
        top: 30vh;
    }
}

@media (max-width: 1199px) {
    .wrapper {
        display: none;
    }

    .hide-title {
        display: block;
    }
}

</style>

<div class="btnID" x-data="{style:'',url:'',murl:'',mobile:'https://blog.wzsco.cn/',desktop:'https://blog.wzsco.cn/'}"
      :style="style" style="">

<div class="tijiaoform" style="margin-bottom: 20px;">
    <input x-model="url" type="text" placeholder="请输入电脑端网址" name="url">
    <input x-model="murl" type="text" placeholder="请输入手机端网址(自适应可为空)" name="murl">
    <input type="button" value="生成" name="submit"
           @click='if(url){mobile=url;desktop=url;}else{utils.snackbarShow("电脑端网址禁止为空");}if(murl){mobile=murl;}'>
</div>

<div class="tijiaoform" style="margin-bottom: 20px;">
    <input type="text" id="colorInput" placeholder="16进制代码/颜色值/颜色名">
    <select id="colorSelect">
        <option value="">选择颜色</option>
        <option value="#000000">黑色</option>
        <option value="#ffffff">白色</option>
        <option value="#00ffff">青色</option>
    </select>
    <input type="button" value="确定" name="submit" @click="changeBackgroundColor()">
</div>

<script>
    function changeBackgroundColor() {
        var colorInput = document.getElementById("colorInput");
        var colorSelect = document.getElementById("colorSelect");
        var displayElement = document.querySelector(".display");

        var selectedColor = colorInput.value || colorSelect.value;
        if (selectedColor) {
            displayElement.style.backgroundColor = selectedColor;
        }
    }
</script>


<div class="wrapper">
    <!--在浏览器控制台选中该元素后使用ctrl+shift+p然后搜索"截图"选择按元素截图即可-->
    <section class="display">
        <div class="mobile ui-draggable">
            <div class="trim">
            <iframe :src="mobile" id="mobile" frameborder="no" border="0" marginwidth="0" marginheight="0"
                    scrolling="no" src="https://blog.wzsco.cn/">
            </iframe>
            </div>
        </div>
        <div class="tablet ui-draggable">
            <div class="trim">
            <iframe :src="desktop" id="tablet" frameborder="no" border="0" marginwidth="0" marginheight="0"
                    scrolling="no" src="https://blog.wzsco.cn/">
            </iframe>
            </div>
        </div>
        <div class="laptop ui-draggable">
            <div class="trim">
            <iframe :src="desktop" id="desktop" frameborder="no" border="0" marginwidth="0" marginheight="0"
                    scrolling="no" src="https://blog.wzsco.cn/">
            </iframe>
            </div>
        </div>
        <div class="desktop ui-draggable">
            <div class="trim">
            <iframe :src="desktop" id="desktop" frameborder="no" border="0" marginwidth="0" marginheight="0"
                    scrolling="no" src="https://blog.wzsco.cn/">
            </iframe>
            </div>
        </div>
    </section>
</div>
<h1 class="hide-title" align="center">分辨率太低！！！</h1>
</div>
<script src="https://cdn.staticfile.org/alpinejs/3.9.6/cdn.min.js" defer=""></script>