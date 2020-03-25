## 步骤
### 1. 在 Typora 正文顶部引用

```html
<script type="text/javascript" src="2html/jquery-3.3.1.min.js"></script>
<script type="text/javascript" src="2html/2html.js"></script>
<link rel="stylesheet" type="text/css" href="2html/style.css">
```

> **特别说明**
> 可能大家用的markdown工具都不一样，也可以：
> 先将md文件导出成html后，然后在html代码中加入以上三行js及css

### 2. 然后用typora 导出为 html


## 效果图


![](https://github.com/icanleric/other/blob/master/PrtScn.png)


## 用到的JS/CSS

### jquery可在官网下载

### 2thml.js
```javascript

//是否显示导航栏
 var showNavBar = true;
 //是否展开导航栏
 var expandNavBar = true;

 $(document).ready(function(){
    var h1s = $("body").find("h1");
    var h2s = $("body").find("h2");
    var h3s = $("body").find("h3");
    var h4s = $("body").find("h4");
    var h5s = $("body").find("h5");
    var h6s = $("body").find("h6");

   var links = document.links;
   for (var i = 0; i < links.length; i++) {
    if (!links[i].target) {
        if (
            links[i].hostname !== window.location.hostname || 
            /\.(?!html?)([a-z]{0,3}|[a-zt]{0,4})$/.test(links[i].pathname)
        ) {
            links[i].target = '_blank';
            } 
        }
    }

    var headCounts = [h1s.length, h2s.length, h3s.length, h4s.length, h5s.length, h6s.length];
    var vH1Tag = null;
    var vH2Tag = null;
    for(var i = 0; i < headCounts.length; i++){
        if(headCounts[i] > 0){
            if(vH1Tag == null){
                vH1Tag = 'h' + (i + 1);
            }else{
                vH2Tag = 'h' + (i + 1);
            }
        }
    }
    if(vH1Tag == null){
        return;
    }

    $("body").prepend('<div class="BlogAnchor">' + 
        
        '<p class="html_header">' + 
            '<span></span>' + 
        '</p>' + 
        '<div class="AnchorContent" id="AnchorContent"> </div>' + 
    '</div>' );

    var vH1Index = 0;
    var vH2Index = 0;
    $("body").find("h1,h2,h3,h4,h5,h6").each(function(i,item){
        var id = '';
        var name = '';
        var tag = $(item).get(0).tagName.toLowerCase();
        var className = '';
        if(tag == vH1Tag){
            id = name = ++vH1Index;
            name = id;
            vH2Index = 0;
            className = 'item_h1';
        }else if(tag == vH2Tag){
            id = vH1Index + '_' + ++vH2Index;
            name = vH1Index + '.' + vH2Index;
            className = 'item_h2';
        }
        $(item).attr("id","wow"+id);
        $(item).addClass("wow_head");
        $("#AnchorContent").css('max-height', ($(window).height() - 80) + 'px');
        $("#AnchorContent").append('<li><a class="nav_item '+className+' anchor-link" onclick="return false;" href="#" link="#wow'+id+'">'+""+""+$(this).text()+'</a></li>');
    });

    
    $(".anchor-link").click(function(){
        $("html,body").animate({scrollTop: $($(this).attr("link")).offset().top}, 500);
    });

    var headerNavs = $(".BlogAnchor li .nav_item");
    var headerTops = [];
    $(".wow_head").each(function(i, n){
        headerTops.push($(n).offset().top);
    });
    $(window).scroll(function(){
        var scrollTop = $(window).scrollTop();
        $.each(headerTops, function(i, n){
            var distance = n - scrollTop;
            if(distance >= 0){
                $(".BlogAnchor li .nav_item.current").removeClass('current');
                $(headerNavs[i]).addClass('current');
                return false;
            }
        });
    });

    if(!showNavBar){
        $('.BlogAnchor').hide();
    }
    if(!expandNavBar){
        $(this).html("目录▼");
        $(this).attr({"title":"展开"});
        $("#AnchorContent").hide();
    }
 });


 $(window).resize(function() {
  $("#AnchorContent").css('max-height', ($(window).height() - 80) + 'px');
});


//插入title的ico图标  
var ico_link = "<link rel=icon type=image/png sizes=32x32 href=2html/ico.png>";
$("head").prepend(ico_link);


```


### style.css 

``` css


    /*markdown_box*/
    html{background: #F4F6F9; font-family:"Microsoft YaHei", "微软雅黑", Arial; font-weight: 400}
    body{background:#F4F6F9;font-size: 16px; color: #515254; line-height: 188%; margin: 0 !important; padding: 0 !important;}
    .html_header{display:block; height: 60px; line-height: 46px; border-bottom: 1px solid #E6ECF1; text-align: left !important;}
    .html_header span::after{content: "Title"; font-size: 17px; font-weight: bold;}
    .html_header span::before{content: "❖"; font-size: 19px; font-weight: bold; margin:0 8px 0 5px; color: #1284d9}
    blockquote{border-radius:0 4px 4px 0;color:#708090;border-left:3px solid #1284d9; background:rgba(238,242,249,.7); padding:8px 16px; font-size: 15px;}
    code{padding: 2px 4px 1px; font-weight: bold; margin:0 3px; border:1px solid rgba(255,130,130,.3);background:rgba(255,130,120,.05); color:#F66; font-family:arial;}
    a{color: #1284d9}
    a:visited{color:#1284d9}
    a:hover{text-decoration: none; color: #087cd2}

    h2{margin: 40px 0 20px; font-size: 36px; font-weight: 400}
    h3{margin-top: 40px; font-size: 30px; font-weight: 400}
    img{border-radius:5px;margin:30px 0 46px !important;width:100%;max-width: 1100px; opacity: .6; transition: opacity .3s}
    img:hover{opacity: 1}


    #write{margin:50px 50px 50px 260px; padding: 20px 60px; max-width: unset; background: #fff;border: 1px solid #E6ECF1; box-shadow: 0 2px 8px rgba(116, 129, 141, .08); border-radius: 4px}
    .BlogAnchor {width: 210px !important}

    @media screen and (max-width: 1620px) {
        #write{margin:40px 40px 40px 250px; padding: 20px 40px;}
        .BlogAnchor {width: 210px !important}
    }

    @media screen and (max-width: 1370px) {
        #write{margin:30px 30px 30px 230px; padding: 20px 40px;}
        .BlogAnchor {width: 200px !important}
    }

    @media screen and (max-width: 1220px) {
        #write{margin:20px 20px 20px 220px; padding: 20px 40px;}
    }

    @media screen and (max-width: 820px) {
        #write{margin:20px 20px 20px 200px; padding: 20px 20px; font-size: 15px; line-height: 170%}
        .BlogAnchor {width: 180px !important}
        .html_header span::before{ margin-left: 0}
        .html_header span::after{ font-size: 15px;}
        h2{ font-size: 30px; }
        h3{ font-size: 24px; }
    }

    @media screen and (max-width: 640px) {
        #write{margin:10px; padding: 16px; font-size: 14px; line-height: 160%}
        .BlogAnchor {display: none;}
        h2{ font-size: 28px; }
        h3{ font-size: 22px; }
    }


/*scroll_style*/
.AnchorContent {
    overflow-y: auto !important;
    overflow-x: hidden !important;
    margin-right:0 !important
}

.AnchorContent::-webkit-scrollbar {
    width: 6px;
    height: 10px;
    background-color: rgba(0,0,0,0) !important;
    position: absolute;
    right: 10px
}
.AnchorContent::-webkit-scrollbar-track {
    -webkit-box-shadow: none;
    border-radius: 0;
    background-color: rgba(0,0,0,0) !important
}
.AnchorContent::-webkit-scrollbar-thumb {
    border-radius: 0px;
    -webkit-box-shadow: none;
    background-color: none;
    opacity: 0 !important;
    transition: all .3s
}

.AnchorContent:hover::-webkit-scrollbar-thumb {
    border-radius: 0px;
    -webkit-box-shadow: none;
    background-color: #d4d6d8;
    border-right:2px solid #fff;
    opacity:1;
}

.AnchorContent::-webkit-scrollbar-thumb:hover {
    background-color: #c0c2c4 !important
}


/*导航*/
    .BlogAnchor {
        background: #fff;
        padding: 10px 0 ;
        line-height: 180%;
        position: fixed;
        height: 100%;
        width: 200px;
        left: 0;
        top: 0;
        border-right: 1px solid #E6ECF1;

    }
    .BlogAnchor p {
        font-size: 20px;
        color: #444;
        margin: 0 16px;
        text-align: center;
    }
    .BlogAnchor .AnchorContent {
        padding: 5px 0px;
        overflow: auto;
    }
    .BlogAnchor li{
        text-indent: 1.5rem;
        font-size: 14px;
        list-style: none;
        padding: 0 0px;
    }
    .BlogAnchor li .nav_item{
        padding:3px 16px;

    }


    .BlogAnchor li .item_h1{
        margin-left: 0rem;
        padding-left:3px;
        font-weight: bold;
    }
    .BlogAnchor li .item_h2{
        margin-left: 0;
        font-size: 0.8rem;
        padding-left: 18px;
        color: #708090
    }
    .BlogAnchor li .nav_item.current{
        color: #087cd2;
        background-color: rgba(238,242,249,.8);
        border-left:4px solid #087cd2;
        text-indent: 20px;
        font-weight: bold;

    }
    #AnchorContentToggle {
        font-size: 13px;
        font-weight: normal;
        color: #FFF;
        display: inline-block;
        line-height: 20px;
        background: rgb(7,196,189);
        font-style: normal;
        padding: 1px 8px;
    }
    .BlogAnchor a:hover {
        color: #087cd2  ;
        background:rgba(238,242,249,.5);
    }
    .BlogAnchor a {
        text-decoration: none;
        color: #333;
        display: block;
        border-radius: 0px;
    }

```

