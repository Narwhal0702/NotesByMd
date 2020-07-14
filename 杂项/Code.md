











```js

```














```js
//适应性代码
var doc=document;
var win=window;
var docEl = doc.documentElement, resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize';
function recalc(){
	var clientWidth = docEl.clientWidth;
	if (!clientWidth) return;docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
};
win.addEventListener(resizeEvt, recalc, false);
recalc();
```


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no, minimal-ui">
    <title>华宸信托</title>
</head>
<style>
*{margin: 0;padding: 0;}

img {width: 100%;vertical-align: top;pointer-events: none; }
.conimg{display: none;}
.bottom{font-size:0;position: fixed;bottom: 0;width: 100%;}
.action{position: absolute;bottom: 0;height: 60px;width: 100%}
.action .btn{float: left; width: 25%;height: 60px;}
.detail-btn{position: absolute;width: 100%;height: 3.7rem;top: 9rem;left: 0;}
.mine-login{
	position: absolute;left: 0;top: .5rem;z-index: 100;
	width: 7.5rem;height: 3rem;
}
.detail-btn1{
	position: absolute;
	left: 0;
	top: 4rem;
	width: 100%;
	height: 10rem;
}
.tips-bar{
	position: fixed;
	left: 0;right: 0;
	bottom: 41px;
	padding: 0 0.2rem
}
.dialog-panel{
	display: none;
	position: fixed;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	z-index: 10;
}
.dialog-panel img{
	width: 100%;
	position: absolute;
    bottom: 0;
}

</style>
<body>
<div class="content">
	<img src="indexImg/home-1.png" class="conimg has-1-login" style="display: block;"/>
	<img src="indexImg/home-2.png" class="conimg" />
	<img src="indexImg/home-3.png" class="conimg has-3-login" />
	<img src="indexImg/home-4.png" class="conimg has-4-login" />
	
	
	<a href="zc-Index-detail.html" class="detail-btn btn-act"></a>
	<a href="zc-login.html" class="mine-login"></a>
	<a href="zc-Index-detail.html" class="detail-btn1" style="display: none;"></a>
</div>

<div class="tips-bar" style="display: none;">
	<img src="indexImg/tips-bar.png" class="tips-bar-img" />
</div>

<!-- <div class="dialog-panel">
	<img src="indexImg/dialog1.png" class="dialog-img1" />
	<img src="indexImg/dialog2.png" class="dialog-img2" style="display: none;"/>
	<img src="indexImg/dialog3.png" class="dialog-img3" style="display: none;"/>
	<img src="indexImg/dialog4.png" class="dialog-img4" style="display: none;"/>
</div> -->

<div style="height: 1rem;background-color: #f8f9fb;"></div>
<div class="bottom">
	<img src="indexImg/nav-1.png" class="btnimg" />
	<div class="action">
		<span href="javascript::" class="btn"></span>
		<span href="javascript::" class="btn"></span>
		<span href="javascript::" class="btn"></span>
		<span href="javascript::" class="btn"></span>
	</div>
</div>
</body>
</html>
```

```js
<script src="js/jquery1.9.1.js"></script>
<script>
	
var doc=document;
var win=window;
var docEl = doc.documentElement, resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize';
function recalc(){
	var clientWidth = docEl.clientWidth;
	if (!clientWidth) return;docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
};
win.addEventListener(resizeEvt, recalc, false);
recalc();



$.getUrlParam = function (name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
    var r = window.location.search.substr(1).match(reg);
    if (r != null) return decodeURI(r[2]); return null;
}

function tab(index){
	if(!index==0){
		$(".btn-act").hide();
	}else{
		$(".btn-act").show();
	};
	if(index==3){
		$(".mine-login").show();
	}else{
		$(".mine-login").hide();
	}
	if(index==1){
		$(".detail-btn1").show();
		if(status == 1){
			$(".tips-bar").show();
		}else{
			$(".tips-bar").hide();
		}
		
	}else{
		$(".detail-btn1").hide();
		$(".tips-bar").hide();
	}
	$(".conimg").eq(index).show().siblings(".conimg").hide();
	$(".btnimg").attr("src",btnimgArr[index])
}

var index = 0;
var status = window.sessionStorage.getItem("statusDemo1");
// var imgArr=["indexImg/case7-img1.png","indexImg/case7-img2.png","indexImg/case7-img3.png","indexImg/case7-img4.png"];
var btnimgArr=["indexImg/nav-1.png","indexImg/nav-2.png","indexImg/nav-3.png","indexImg/nav-4.png"];
if(index==3){
	$(".mine-login").show();
}else{
	$(".mine-login").hide();
}
if(window.sessionStorage.getItem("statusDemo1") == 1){
	$(".has-4-login").attr("src","indexImg/home-4-act.png");
	$(".has-1-login").attr("src","indexImg/home-1-act.png");
	$(".has-3-login").attr("src","indexImg/home-3-act.png");
}
$(".btn").click(function(e){
	e.preventDefault();
	tab($(this).index());
	index = $(this).index();
	// window.sessionStorage.setItem("status",0);
})
$(".mine-login").click(function(){
	console.log(window.sessionStorage.getItem("statusDemo1"))
	if(window.sessionStorage.getItem("statusDemo1") == 1) return;
	window.location.href = "zc-login.html";
})

var tabimgindex=0;
$(".tips-bar").click(function(){
	$(".dialog-panel").show();
	abimgindex=0;
})

$(document).on("click",".dialog-panel",function(){
	abimgindex++;
	$(".dialog-panel img").eq(abimgindex).show().siblings().hide();
	if(abimgindex == 4){
		$(".dialog-panel").hide().find("img").eq(0).show().siblings().hide();
		$(".tips-bar").hide();
	}
})
</script>
```

```vue
<template>
	<compframe :param="param" :style="{backgroundImage: linearStyle.backgroundImage}" class="pos-r">
	  <div class="pos-r">
	    <div :style="{ paddingTop: (isIphoneXApp ? '98px' : '60px')}" class="flex-row align-center pl30 pb190">
        <div class="flex-row align-center" v-if="isLogin">
          <image :src="perImg" class="perImg mr20"></image>
  	      <text class="font-18 c-white lh64">{{welcome}}</text>
        </div>
	      <text v-else class="font-15 c-white lh64" @click="jump('login')">Hi, 请登录</text>
	    </div>
	  </div>
	  <div style="width:750px;height:250px;"></div>
    <image :src="bgBottomImg" class="bgBottomImg"></image>
	  <div :style="{top: (isIphoneXApp?'178px':'140px')}" class="align-center justify-center  pos-a boxs"  >
      <image :src="itemBg" class="itemBg"></image>
      <div style="position:relative;z-index:15;" class="align-center justify-center">
          <div class="h40"></div>
          <text class="font-30 font-white" >{{communicationData.assetEyeState?shareInfo.totalcapital:'***'}}</text>
          <div class="flex-row  mb10 align-center justify-center  pos-r">
            <text class="font-12 mr16 font-white opacity-6">总资产(元)</text>
            <div @click="eyeClick()">
              <text class="vector-iconfont font-30 ml10 " style="margin-top:5px;color:#fff"  v-if="communicationData.assetEyeState">&#xe685;</text>
              <text class="vector-iconfont font-30 ml10"  style="margin-top:10px;color:#fff"  v-else>&#xe610;</text>
            </div>
          </div>
            <!--昨日收益  持有收益  累计收益(元)  -->
          <div class="h120 flex-row align-center justify-center pl30 pr30 mb20" style="width:750px;">
              <div class="row-item align-center justify-center">
                <text class=" font-18 mb5 font-white font-bold line44">{{shareInfo.totallastincome | formatMoney(true) | canSee(communicationData.assetEyeState)}}</text>
                <text class=" font-12 font-white opacity-6">昨日收益(元)</text>
              </div>
              <div class="row-item align-center justify-center">
                <text class=" font-18 mb5 font-white font-bold line44">{{shareInfo.totalgainbalance | formatMoney(true) | canSee(communicationData.assetEyeState)}}</text>
                <text class=" font-12 font-white opacity-6" >持有收益(元)</text>
              </div>
              <div class="row-item align-center justify-center">
                <text class=" font-18 mb5 font-white font-bold line44">{{shareInfo.totalincome | formatMoney(true) | canSee(communicationData.assetEyeState)}}</text>
                <text class=" font-12 font-white opacity-6" >累计收益(元)</text>
              </div>
            </div>
      </div>
    </div>
	    <!--快捷图标列表-->
    <div class="flex-row align-center justify-center pb40 pt20" style="position:relative;z-index:111">
      <div class="row-item flex-column justify-center align-center rel" @click="jump(item.url, item.param)" v-for="item in iconList">
        <image :src="item.icon" class="img-icon mb20"></image>
        <text class="m-color-1 font-14 line40">{{item.title}}</text>
        <div class="quick-fix align-center justify-center" v-if="item.key == 'jyjl' && isDIS">
          <div class="status-num" >
            <text class="font-12 c-white">扣款中</text>
          </div>
        </div>
        <div class="quick-fix align-center justify-center" v-else-if="item.key == 'dqr' && !isNaN(parseInt(totalrecords)) && parseInt(totalrecords) > 0">
          <div class="wait-num">
            <text class="font-12 c-white">{{totalrecords}}</text>
          </div>
        </div>
      </div>
    </div>
	</compframe>
</template>
<script>
  import $ from '@/common';
  import config from '@/config';
  import color from "@/common/color";
  import Light from 'light';
  import assetoverviewService from '@/service/market/ui/assetoverview';

  export default {
  	mixins: [assetoverviewService],
    data() {
      return {
        navStyle:{
          "background-color": config.primaryColor
        },
        isIphoneXApp: $.platform.isApp() && $.platform.isIPhoneX(),
        linearStyle: {
          backgroundImage: 'linear-gradient(to bottom,'+config.primaryColor+','+color.lighter(config.primaryColor)+')'
        },

        containerStyle: {
          "borderColor": "transparent"
        },
        isDIS: false, //是否扣款中
        totalrecords: 0, //待确认数
        perImg:"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAMAAACdt4HsAAABqlBMVEUAAAD///////////////////////////////////////////////////////////////////////////////////////////+GsfmHsvmHsviHsfn///+IsvmGtPqHsfiGsfmGsviGsvmIsfqHsfiHsvmKsfuHtPqIs/+Stv+Pv/+JxP+Qt/qcwfz////96+GGsfg6ODj+7ONNSkpIRkZHREREQkL+7uVVUlJTUFBPTExCQEBAPj7//v1ZVlVLSEg+PDw8OjpcWVn+8elXVFRRTk7/+vb/9/Oop6dhXVz6/P//+/mKtPmXuvX/9vD+8+z26eTY19fOzMzg0ci/vb1va2n5+fmmxfmNtvnj4+Py4djbzMSsq6ukoqKwpJ6Rj4+BfXx8eHdRTUzh7P7a5/7S4v2zz/uty/u+1Prs7OzV2uvo6Oje3ej76eD5593R0NDYycHPwbqYjoloZGNiYWHr8v/N3/2dwPmQtvbz8/OfvfOsxfLx8fHB0PG9zfGuxvHm4N3o29Xp2dDEw8PGwsC/v7+2tbW7rqienJymnpqbko52dHRybW1KSEjd3Hi/AAAALnRSTlMA+up/YQOO7uzf1dLLxKWNc1M7Mx4VEA357erUsX9h38vEpY1zUzszHhUQDY5iNuo6vwAAAy9JREFUWMOVlmdbGkEUhQeXKAhSVBBU7N1kCxbQCLFFBVRExN577+m99/+cIGBgz8zu+n7YD/Pcc2bmzszdS1g47JzFbDTodAaj2cLZHeROlFhNvAyTtUSrusxWyFMptJURdZxcAc+kgHOq6fV5vCJ5ekV5aRGvSlEpW18M09PIK2YuX8drQkffxr18XjP59yj6Sv4OVKIDzK9MPuyfERhb+7W+Ms0jeln+qfk7Otvo73vY3dWZ+ISZLM45f8r5LaxcS9JAyuBRx8ZBenj2KHOa2fcB78/s2oAkZRn09izPJscD32O3N0opATG/JOUaPO4JjU3HZtZDC5gGZx4sv1NCA/9wcHAw9DvrSmZeFifXvxiWmAYrWXFc+v3D+12W0GAzaRAcvHqd/bpT9cEGGbiWmCuYyQm0kSRQfw6kjstvF0tL8Xh8tTvXYExWo27qHyzgTLoQMpz3ZBusyUOTddIKBl+kReGWjxv/DP7c5CDYNyYPtRJCTGAwMyBkc36Z6O3wX/1c+iGBgYkQB48GXYKM09PkN44GvIPY0eDzpkDlpH8ZYu2EQ4PpoEDH/xViOWJBg/chhkECC4OFmOVDAd9JgmGw/iEgjzYTo3woKgirVHlyfFIebSQG+ZBPEBap8uR4VB5tIDo0UGAIKhsaDCkZTIIBbmFUySACW8Ak8l6lHWASzTA2wtR7IxBspl2kUcYafCMYayEcjwS8VD1PgYPHxD6JKC3SDs+ZfRIjtEgHFBTYg+IOTKmShkxqXIAViirLwTtKDSuBsg5nCfNDWSc2nkrECwkAbPBrg0yiAf7a4C7BbWAZcPB7Zxp4qR2nU6XD8qkY6LHFYd+mCA8UqTRZgWhOJQjABkoV27yt/Skhh6m53Sf0Ng/TEN7enRfF58fZ+uMJURTn97YgAdDqhnf2xsUUE4dT6dkPX4ppxue2/7e62GyHn86l1RmPV2/fvJsQcxh/tnPTbGO7H96fF7VxP6lHHri0yV1VhEFTuRZ9eRNh0lKrrq9tIUpUlatMX0VUaPO42XK3p42o095QQZdXNLQTjTTXV4C6vpncidZGT11NtdvlclfX1HkaWwmDv7ElZ0eJgJiOAAAAAElFTkSuQmCC",
        itemBg:"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAt4AAAFsCAMAAADMoE6OAAAAWlBMVEX///////////8AAAD///8AAAD///////////////8AAAD///////8AAAAAAAAAAAD///8AAAD///////////////////////////////////////////+0tLSNR07gAAAAHnRSTlMkJioDLQExOjVDBjxADAkRRhRleE5TSWhYelVvYBnJx852AAANmElEQVR42uzY226rMBRFUU6bA8RchBwIVpL+/28Wq7sxsG1jgqlatKYjtW99GVlynfxH6LCBNzpw4I0OHHijAxfC+x2hX1gIb7BGfzwfb9BGB8jFG7bRMbLyBm50lCy8gRsdJ8Y7WLdA6JcU5pvzBmr0p1rwnbh0f2RK9uMkQpHr3d09XSbd5fnD5Ttx6C7kQ6nO1CIUq27067SbSd2U6TF89Jkldf3gvXH4Tuy6W6napiwLXlZkCG2s4JWjzt811JVqr5MvSae7qUd/UXbfiWO7u6bI85Q6IRS9VB/9c1L+LNOHmn8HxvwH8Uo69jux3rularJ8rDrVn3lvCK3IpZziyKmMchK/tqq/sPu3i7fIHm0x6Kbz1AzaaHO+IWe+2YRz3uT7cT8LK2+uWyjV6O1+2k6x2ihe1vkm33y+je+C4rybVvVSMN823kIIqcqcbONGgvbIPuA231nA7aS5qv4ywOW8LbpF35UpfZ/0B7hR9Ph++337eTc3eRHMN+ctvngXwx/CciPWfsJpv72370XeIpj3KfXj/ofQyjy++X573k44787Fm+uuNW/2P+Xc9hsOztozE+7/95LNN+NNffGumW8r79rwduCGbZwNZxzpGgkPmO+SmvGul3iLCe8RcQw3zj4T7nk9MbhX8BYLvGu+3hhunNjH5Lt9k272dmLnXXPec93E+zQOuHH2A35y+s6pgMs38Z755rxrw5vrHh88naB1+XwTbdfbYCDv+gXewI32BT5fb9d8G97US7yrgTd0I2pH4C7fAZdvzrvy8ybdmndbMN2gjeK07NtyPQniTb79vKsJb+hGsfNev/Xh8x3CuwrkLQ1v4EY7ZDARsOW3k9d5v3Pe0I12zIBa9E3rvY63LoA3dCNqZ9/s7cRx+Y7H24w3dKPYeebb9nYShXdt5e3AnSC0Irtvzntxvblv4j0UypuPN3ijLbn2m2Jv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",
        bgBottomImg:"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAu4AAAFeBAMAAAAoEYcRAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAASUExURUdwTP///////////////////4gZPH8AAAAFdFJOUwCRTNIcGRgPBgAABM9JREFUeNrt2lFuGkkQgGFszQEWCO8BOwdw0LwD5gIWqvtfZbG9XimytQuG6eoevv8xiRPpU6u6epTJRLqZtggyuu8ZZLQIBgk9B/eMKRPcE+p67hk9BPeE7oJ7ygrJPWeF5J6zQnLPGu7cM1ZI7sX7FdwThzv34t8HuJev55473LkXbBvck4c795zhzj1nuHNP2Ny5l+uu555Q94mde4kWwb2G4c69yHAP7hkPpp57xp26CO4VPJi4p92p3HPuVO6D36nBvZ47lXv5dyr3vDuV+6Btg3tCu+BezecB7nmrDPcBmwf3hB6Ce22rDPehugvu9a0y3AdaZU5g5158g+Q+TCexcy++QXIfoufgXuXizj1ncec+wOIe3Ct9L3FPZede+L3EPZWde9lnKvcrNw/u9X4d4J7Mzj2HnXsOO/fLWwb3hJ6De0Lb4N4OO/ccdu457Nxz2LkX32S4Z+zt3DNPO/ckdu4Fv8lwT2fnnsPO/Tstgnv5uiuwc89h557Dzv3MzvrPeNxrY+d+VtsI7i2zcy/6WuL+jebBvdn9kfuZi8x12bmf1l0f3JteZLjnLDLcT75R58G9/RuV+2mjvQ/u5VtGcB/HaOeeM9q554x27sW3du6ZM4Z7zozhnjNjuOfMGO45M4b7l2+lhwju5WdMH9zH8z3mk/uMddEL9cM9Xja8Pw57H+Xc4/AX8WE/Pn7tHvEbetHD/uEeTzc/a+5LHvZ/3ePww2HPcD/Omhs+8uXWmM/ucfhpZ89wj7jNVX7XR7J7vNzeke/mEenut3fkl31U4R5Pt3Tkd4uIStyPR35jxGS4x8vjTagvI+pyv4ldfttHfe6jf74mDvb/dB/3/Xo/j6jVfbzD5v4homb3OIxxme+mEZW7j3Cz6ZZ9NOA+sjFfj/r/ukdMN9Qz3EfygK1lrp/hfrxgN9QT3FuX380j2nRvWX5bofrp7kf5Fm/Yui7Tb7kf5X83tlXup5Wqn+f+us839JJazaPeJuf+wMvMUc9wf71ifzrqCe61j5td5Uf9Avd6D/1u2QD6Be6vh35V22K5X66jkSaX/PChpnnTEPql7m+vqcc6xktL6Fdwf6dPHThdExfp9d3fBk7WrN8t59Fik6v9TetZ6YnTrRo86Fd3f5s4s32xW7Rd86u7v4+cwc/9cbY0bT6I+z/2w8z7brecrmMMTQb7mw9P09UVp85+NRbygd3f8dfT2YX63W5c4kXcP3adpyP/an/W7Nm/es/XfYyySdF/7bBeT6fT5Wq1etzv990fzpvjrxx/YzU7/on1WLmT3L+qP8QNNglx5y7u3MWdu7hzF3fu4s6du7hzF3fu4s5d3LmLO3fu4s5d3LmLO3dx5y7u3MWdO3dx5y7u3MWdu7hzF3fu3MWdu7hzF3fu4s5d3LlzF3fu4s5d3LmLO3dx5y7u3LmLO3dx5y7u3MWdu7hz5y7u3MWdu7hzF3fu4s6du7hzF3fu4s5d3LmLO3dx585d3LmLO3dx5y7u3MWdO3dx5y7u3MWdu7hzF3fu3MWdu7hzF3fu4s5d3LmLO3fu4s5d3LmLO3dx5y7u3LmLO3dx5y7u3MWdu7hzF3fu3MWdu7hzF3fu4s5d3LlzF3fu4s5d3LmLO3dx585d3LmLO3ddo78BQMw+8M3xKqAAAAAASUVORK5CYII="
      }
    },
    computed: {
      headerBgColor(){
        let RgbValueArry = color.hexToRgb(this.param.bgcolor||config.primaryColor);
        var $grayLevel = RgbValueArry[0] * 0.299 + RgbValueArry[1] * 0.587 + RgbValueArry[2] * 0.114;
        if ($grayLevel >= 192) { //浅色
          return false;
        } else {//深色
          return true;
        }
      }
    },
    created(){
      	this.getTradeRecord();
      if ($.platform.isApp()) {
        $.broadcast.receive("B_LOGIN", (isLogin) => {
          if (isLogin) {
            this.getTradeRecord();
          } else {
            this.isDIS = false;
            this. totalrecords = 0;
          }
        });
        
        $.broadcast.receive('B_REFRESH_SHAREDATA', () => {
          this.getTradeRecord();
        })

        $.broadcast.receive('B_RECORDWITHDRAW', () => {
          this.getTradeRecord();
        })

      }
      if(this.param.bgcolor){
        this.linearStyle={
          'backgroundImage': 'linear-gradient(to bottom,'+(this.param.bgcolor||config.primaryColor)+','+(color.lighter(this.param.bgcolor||config.primaryColor))+')'
        }
      }
    },
    methods:{
    }
  }
</script>
<style src="@/css/global.css" scoped></style>
<style scoped>
  .bgc-blue {
    background-color: #4A90E2;
  }
  .pb190 {
    padding-bottom:190px;
  }
  .mb15 {
   margin-bottom:15px;
  }
  .pt52 {
    padding-top:52px;
  }
  .eye-img {
    width: 48px;
    height: 32px;
    margin-left:16px;
  }

  .mt5 {
    margin-top: 5px;
  }

  .eye-img2 {
    width: 48px;
    height: 22px;
  }

  .font-red {
    color: #FF4500;
  }
  .font-30 {
    font-size:60px;
  }
  .mb36 {
    margin-bottom:36px;
  }
  .c-gray {
    color:#999999;
  }
 
  .line40 {
    line-height:40px;
  }
  .boxs {
    border-radius:8px;
    width:734px;
    height:364px;
    left:8px;
  }
  .img-icon {
      width:56px;
      height: 56px;
    }
    .pl46 {
      padding-left:46px;
    }
    .h120 {
      height:118px;
    }
    .pt40 {
      padding-top:40px;
    }
    .pt50 {
      padding-top:50px;
    }
    
    .perImg{
      width:64px;
      height:64px;
    }
    .h40{
      height:40px;
    }
    .itemBg{
      position:absolute;
      left:0;
      right:0;
      top:0;
      bottom:0;
      z-index:11;
    }
  .bgBottomImg{
    position:absolute;
    bottom:0;
    left:0;
    right:0;
    height:350px;
  }
  .line44{
    line-height:44px;
  }
  .lh64{
    line-height:64px;
  }
  .h180 {
  height: 180px;
}

.status-num {
  /* position: absolute;
  right: 10px;
  top: 0px;
  min-width: 32px; */
  height: 32px;
  padding-left: 10px;
  padding-right: 10px;
  border-radius: 32px;
  background-color: #fc6054;
  margin-left: 80px;
}
.rel{
  position:relative
}
.quick-fix{
  position: absolute;
  right: 0;
  left: 0;
  top:0px;
  height:32px;
}
</style>
```

```js
define([], function () {
    var action = {
        constant: {
            custname: "",
            idno: "",
            validDateEnd: "",
            sex: "",
            imageFileList:[],//上传的文件集合
            imageFileList2:[]
        },
        init: function () {
            action.events();
            action.openclock = action.openclock("smscodebtn");
            // action.initBanks();
            action.initPage();
            $.hsf.Event.addListener("selectBank", function (selectBankIndex) {
                action.constant.selectCard = selectBankIndex;
                action.selectBankProcess(selectBankIndex);

            });
            action.pdictForm();
            action.initdictSel("国籍代码","nationnalSel");
            action.initdictSel("职业","workcodeSel");
        },
        initPage: function () {
            $.hsf.startLoading();
            var that = this;
            $.when(action.initBanks(), action.getPersonInformation())
                .done(function(r1, r2) {
                    var bankResult = r1[0];
                    if (bankResult.successful) {
                        $.hsf.stopLoading();
                        action.constant.bankcards = bankResult.bankcards;
                        if (bankResult.bankcards.length == 0) {
                            $.UIAlert("没有银行卡", function () {
                                $.hsf.hsBack();
                            });
                        } else {
                            that.selectBankProcess(0);
                        }
                        if (r2[0].successful) {
                            var personInfo = r2[0];
                            var planItems = personInfo.result.Item;
                            if ($.hsf.qyjhbhBlackList && $.hsf.qyjhbhBlackList.length > 0) {
                                var blackListStr = '|' + $.hsf.qyjhbhBlackList.join('|') + "|";
                                var isInBlackList = false;
                                $.each(planItems, function (index, plan) {
                                    if (blackListStr.indexOf("|" + plan.QYJHBH + "|") !== -1) {
                                        isInBlackList = true;
                                        return false;
                                    }
                                });
                                if (isInBlackList) {
                                    // 不允许修改密码
                                    $.UIAlert("对不起，您暂时无法重置年金密码", function () {
                                        $.hsf.hsBack();
                                    });
                                }
                            }
                        }
                    } else {
                        $.hsf.callFailProcess(bankResult);
                    }
                }).fail(function () {
                $.hsf.stopLoading();
            })
        },
        getPersonInformation:function () {
            return $.hsf.ajax.app("changjiangpension/personalPlanInformation/queryPersonalPlanInformation", "", "personalPlanInformationCallback", function() {});
        },
        selectProvince: function (value) {
            var key = value + "城市";// system/dictionary
            var provinceText = $("#province").find("option:selected").text();
            var bankWeb = provinceText + "分行";
            $("#bankweb").UITextField("value", bankWeb);
            $("#bankweb").attr("m-placeholder", bankWeb).find("input").attr("placeholder", bankWeb);
            $.hsf.ajax.app("atomicquery/account/dict", "dictname=" + key, "cdictCallback", action.cdictCallback);
        },
        initdictSel: function (dictname,selId) {
            var that = this;
            $.hsf.ajax.app("atomicquery/account/dict", "dictname="+dictname, "initdictSel", function (jsonResult) {
                if (jsonResult.successful) {
                    var list = jsonResult.dictResult.items;
                    if (null != list && list.length > 0) {
                        var html = "";
                        for (var item in list) {
                            var dictObj = list[item];
                            if (dictObj.key=='156'){
                                html += "<option selected='selected' value='" + dictObj.key + "'>" + dictObj.value + "</option>"
                            }else {
                                html += "<option value='" + dictObj.key + "'>" + dictObj.value + "</option>"
                            }
                        }
                        if ("" != html) {
                            $("#"+selId).html(html);
                        }
                    }
                }
            });
        },
        pdictForm: function () {
            var that = this;
            $("#provincecode").UISelectField("change", function (value) {
                that.selectProvince(value);
            });
            $.hsf.ajax.app("atomicquery/account/dict", "dictname=省份", "pdictForm", function (jsonResult) {
                if (jsonResult.successful) {
                    var list = jsonResult.dictResult.items;
                    if (null != list && list.length > 0) {
                        var html = "";
                        for (var item in list) {
                            var dictObj = list[item];
                            html += "<option value='" + dictObj.key + "'>" + dictObj.value + "</option>"
                        }
                        if ("" != html) {
                            $("#province").html(html);
                        }
                    }
                    var codesel = $("#provincecode").UISelectField("value");
                    that.selectProvince(codesel);
                } else {
                    $.hsf.callFailProcess(jsonResult);
                }
            });
        },
        cdictCallback: function (jsonResult) {
            if (jsonResult.successful) {
                var list = jsonResult.dictResult.items;
                if (null != list && list.length > 0) {
                    var html = "";
                    for (var item in list) {
                        var dictObj = list[item];
                        html += "<option value='" + dictObj.key + "'>" + dictObj.value + "</option>"
                    }
                    if ("" != html) {
                        $("#city").html(html);
                    }
                }
            } else {
                $.hsf.callFailProcess(jsonResult);
            }
        },
        initBanks: function () {
            // var that = this;
            return $.hsf.ajax.app("changjiangpension/assetManagementEntrance/getOpenAccoBankFormNP", "", "bankcardFormCallback", function(){});
        },
        // function (jsonResult) {
        //     if (jsonResult.code == "ETS-5BP00000") {
        //         action.constant.bankcards = jsonResult.bankcards;
        //         if (jsonResult.bankcards.length == 0) {
        //             $.UIAlert("没有银行卡。", function () {
        //                 $.hsf.hsBack();
        //             });
        //         } else {
        //             that.selectBankProcess(0);
        //         }
        //     } else {
        //         $.hsf.callFailProcess(jsonResult);
        //     }
        // }
        openProcess: function () {
            //首先验证验证码
            var mobile = $("#tel").UITextField("value").trim();
            var identitytype = "0";
            var identityno = $("#idNo").UITextField("value").trim().toUpperCase();
            var accoreqserial = action.constant.accoreqserial;
            var capitalmode = action.constant.capitalmode;
            var bankserial = action.constant.bankserial;
            var bankacco = $("#bankacco").UITextField("value");
            var originalorderid = action.constant.accoreqserial;
            var customername = action.constant.customername = $("#username").UITextField("value");
            var otherserial = action.constant.otherserial;
            var mobileauthcode = $("#valid").UITextField("value").trim();
            var data = "mobile=" + mobile + "&identitytype=" + identitytype + "&identityno=" + identityno + "&accoreqserial="
                + accoreqserial + "&capitalmode=" + capitalmode + "&bankserial=" + bankserial + "&bankacco=" + bankacco + "&originalorderid="
                + originalorderid + "&customername=" + customername + "&otherserial=" + otherserial + "&mobileauthcode=" + mobileauthcode;

            $.hsf.ajax.app("changjiangpension/assetManagementEntrance/fastAuthNP", data, "fastAuthCallback", function (jsonResult) {
                if (jsonResult.successful) {
                    action.constant.authcode = $("#valid").UITextField("value").trim();//获得正确的验证码
                    action.constant.tel = $("#tel").UITextField("value").trim();
                    action.constant.yinliancdcard = jsonResult.yinliancdcard;
                    $("#one").hide();
                    $("#two").show();
                    $("#three").hide();
                    $("#four").hide();
                    $.hsf.stopLoading();
                    return false;
                } else if (jsonResult.code == "ETS-1BQ08") {
                    $.hsf.stopLoading();
                    $.UIAlert("您的验证码已失效 ,请重新获取");
                    return false;
                } else {
                    $.hsf.callFailProcess(jsonResult);
                }
            });
        },
        selectBankProcess: function (result) {
            $(".selectedBankName").html(action.constant.bankcards[result].bankname);
            $(".selectedBankcardIcon").removeAttr("class").addClass("selectedBankcardIcon bank-logo bank-" + action.constant.bankcards[result].alias);
            action.constant.alias = action.constant.bankcards[result].alias;
            action.constant.bankserial = action.constant.bankcards[result].bankserial;
            action.constant.capitalmode = action.constant.bankcards[result].capitalmode;
            action.constant.bankname = action.constant.bankcards[result].bankname;
        },
        events: function () {
            $("#njback").bind("tap", function () {
                $("#one").show();
                $("#two").hide();
                $("#three").hide();
                return false;
            });
            $("#openZg").bind("tap", function () {
                $.hsf.hsOpen("nj-open-form2.html");
                return false;
            });
            $("#bankcardSelect").bind("tap", function () {
                var $banklist = $("#bankList");
                var bankcards = action.constant.bankcards;
                $.doTemplate("bankList-tempalte", bankcards);
                $banklist.UITableView("refresh");
                action.choose();
                return false;
            });
            $("#bankList").UITableView("mark", function (result) {
                $.hsf.Event.trigger("selectBank", null, result);
                $("#n5").hide();
                $("#one").show();
                return false;
            });
            $("#smscodebtn").on("tap", function () {
                if (this.getAttribute("m-state") != "disabled") {
                    var mobile = $("#tel").UITextField("value").trim();
                    var identitytype = 0;
                    var identityno = $("#idNo").UITextField("value").trim().toUpperCase();
                    var bankacco = $("#bankacco").UITextField("value");
                    var customername = $("#username").UITextField("value");
                    var bankserial = action.constant.bankserial;
                    var capitalmode = action.constant.capitalmode;
                    action.constant.zjhm = identityno || "";
                    if (action.validateyzm()) {
                        $.hsf.startLoading("正在获取...");
                        var data = "mobile=" + mobile + "&identitytype=" + identitytype + "&identityno=" + identityno + "&capitalmode="
                            + capitalmode + "&customername=" + customername + "&bankserial=" + bankserial + "&bankacco=" + bankacco;
                        $.hsf.ajax.app("changjiangpension/assetManagementEntrance/sendMobileAuthCodeNP", data, "", function (jsonResult) {
                            $.hsf.stopLoading();
                            if (jsonResult.successful) {
                                action.constant.zjhm  = identityno || "";
                                action.constant.tel = $("#tel").UITextField("value").trim();
                                action.constant.accoreqserial = jsonResult.accoreqserial;
                                action.constant.otherserial = jsonResult.otherserial;
                                $.UIAlert("手机验证码已发送！请注意查收短信！");
                                action.openclock.start();
                            } else {
                                $.hsf.callFailProcess(jsonResult);
                            }
                        });
                    } else {
                        $.UIAlert("输入数据错误。");
                        return false;
                    }
                }
            });
            $("#nextBtn").bind("tap", function () {
                $.hsf.startLoading();
                if (action.validate1()) {
                    var data = "idcode=" + action.constant.zjhm;
                    action.constant.username = $("#username").UITextField("value");
                    action.constant.bankname = $(".selectedBankName").html();
                    action.constant.bankacco = $("#bankacco").UITextField("value");
                    action.constant.tel = $("#tel").UITextField("value");
                    $.hsf.ajax.app("changjiangpension/bindingAccount/queryNjIsOpenAcco", data, "", function (jsonResult) {
                        if (jsonResult.njIsOpenAcco == "1") {
                            // $.hsf.stopLoading();
                            action.openProcess();
                            return false;
                        } else {
                            $.hsf.stopLoading();
                            $.UIConfirm({
                                "html": "您暂无我司年金账户，无法开通该功能。如需购买个人养老保障产品，请开通资管服务。",
                                "submitText": "是",
                                "cancelText": "否"
                            }, function (result) {
                                if (result == "yes") {
                                    //跳到开通资管承诺函
                                    $.hsf.hsOpen("account-openAcco-warningLetter.html");
                                    return false;
                                } else if (result == "no") {
                                    $.hsf.hsOpen("index.html");
                                    return false;
                                }
                            });
                        }
                    });
                } else {
                    $.hsf.stopLoading();
                }
            });
            $("#kaitong").bind("tap", function () {
                //验证输入数据
                if (action.validate2()) {
                    //重置密码
                    action.resetPwd();
                }
            });
            $("#ktzg").bind("tap", function () {
                action.ktzg();
            });
            $(".back").bind("tap",function () {
                $(".m-bg-3").children().slice(1,5).hide();
                $(this).parents('div:eq(3)').prev().show();
            })
            $("#long-term").bind("tap",function () {
                var self=$(this);
                if (self.attr("m-checked") != 'yes'){
                    $("#enddate1").parent().show();
                }else {
                    $("#enddate1").parent().hide();
                }
            })
            $("#uploadimg").bind("tap", function () {
                //验证输入数据
                if (action.validateZG()) {
                    $("#ktzgForm").hide();
                    $("#uploadcard").hide();
                    $("#uploadpwd").show();
                    $("#ktzgResult").hide();
                }
            });
            $("#sevenstn").bind("tap", function () {
                var dateFormat =/^(\d{4})-(\d{2})-(\d{2})$/;
                var ocridno = $("#ocridno").html();
                var ocrinvalidate = $("#ocrinvalidate").html();
                if(ocrinvalidate != "长期"){
                    if(!dateFormat.test(ocrinvalidate)){
                        $.UIAlert("证件有效期识别错误，请重新上传！", function(){
                            $.hsf.hsOpen("nj-open-form.html");
                        });
                        return false;
                    }
                }
                var cerfiticate18 = /^((11|12|13|14|15|21|22|23|31|32|33|34|35|36|37|41|42|43|44|45|46|50|51|52|53|54|61|62|63|64|65|71|81|82|91)\d{4})((((19|20)(([02468][048])|([13579][26]))0229))|((20[0-9][0-9])|(19[0-9][0-9]))((((0[1-9])|(1[0-2]))((0[1-9])|(1\d)|(2[0-8])))|((((0[1,3-9])|(1[0-2]))(29|30))|(((0[13578])|(1[02]))31))))((\d{3}(x|X))|(\d{4}))$/;
                if (ocridno.length == 0) {
                    $.UIAlert("身份证号识别错误，请重新上传！", function(){
                        $.hsf.hsOpen("nj-open-form.html");
                    });
                    return false;
                }
                if(!cerfiticate18.test(ocridno)){
                    $.UIAlert("身份证号识别错误，请重新上传！", function(){
                        $.hsf.hsOpen("nj-open-form.html");
                    });
                    return false;
                }
                $("#ktzgForm").show();
                $("#uploadcard").hide();
                $("#uploadpwd").hide();
                $("#ktzgResult").hide();
                $("#seven").hide();
            });
            // 画图 加载身份证正面图片
            $("#pic").on("change", function (e) {
                var $that = $(this);
                var f_flag = action.checkFile(e);
                var file = e.target.files[0];
                var fileSize = e.target.files[0].size;
                if (!f_flag) {
                    return false;
                }
                var reader = new FileReader();
                reader.readAsDataURL(file);
                //这个函数带有两重回调  只有未压缩的可以 直接获取返回值 所以 取值直接在页面上获取
                action.renderPic('id_cropped_image', reader, file, fileSize, 2.5, 0.3);

                $("#id_cropped_image").attr("style", "display:block");
                //获得第一张图片
                action.constant.getFirstPic = true;
                //判断是否两张图片已加载,按钮变色
                if (action.constant.getFirstPic && action.constant.getSecondPic) {
                    //按钮变色成黄色
                    $("#submitId").css("background-color", "#1565C0");

                }
                return false;
            });
            $("#submitId").bind("tap", function () {
                // 按钮颜色判断
                var btnColor = action.checkColor('#submitId');
                if (!btnColor) {
                    return false;
                }
                // 两张图片一样
                var same_flag = action.isSamePictures();
                if (!same_flag) {
                    return false;
                }
                action.ocrIdcardUpload();
            })
            //背面
            $("#pic1").bind("change", function (e) {
                var $that = $(this);
                var f_flag = action.checkFile(e);
                var file = e.target.files[0];
                var fileSize = e.target.files[0].size;
                if (!f_flag) {
                    return false;
                }
                var reader = new FileReader();
                reader.readAsDataURL(file);
                action.renderPic('id_cropped_image1', reader, file, fileSize, 2.5, 0.3);

                //显示图片 并把图片获得标志置为true
                $("#id_cropped_image1").attr("style", "display:block");
                //获得第二张图片标志位
                //判断是否两张图片已加载,按钮变色
                action.constant.getSecondPic = true;
                if (action.constant.getFirstPic && action.constant.getSecondPic) {
                    $("#submitId").css("background-color", "#1565C0").attr("m-disabled", "");
                }
                return false;
            });
        },
        ktzg: function () {
            var tradepassword = $("#zgmima").UITextField("value") || "";
            var tradepassword2 = $("#zgmima2").UITextField("value") || "";
            var passwordValid = /^[0-9a-zA-Z]{6,8}$/;
            if (tradepassword == "") {
                $.UIAlert("请输入交易密码!");
                return false;
            }
            if (!passwordValid.test(tradepassword)) {
                $.UIAlert("交易密码必须为6-8位数字或字母!");
                return false;
            }
            if (tradepassword2 == "") {
                $.UIAlert("请输入密码确认!");
                return false;
            }
            if (!passwordValid.test(tradepassword2)) {
                $.UIAlert("交易密码必须为6-8位数字或字母!");
                return false;
            }
            if (tradepassword2 != tradepassword) {
                $.UIAlert("两次输入交易密码不一致!");
                return false;
            }
            if ($("[m-name='checkBox']").attr("m-checked") != "yes") {
                $.UIAlert("您还没有勾选并同意《投资事项确认与风险提示》和《浦发集中代收付授权书》！");
                return false;
            }
            action.merOpenAcco();//调用商户级别开户
        },
        merOpenAcco: function () {
            $.hsf.startLoading("正在提交");
            var identityno = action.constant.zjhm;
            var birthday = action.getBirthdayFromCard(identityno) || "1979-12-31";//从身份证中获取生日
            var sex = action.getSexFromCard(identityno);//从身份证中获取性别
            var workcode = $("#workcode").UISelectField("value");
            var tradepassword = $("#zgmima").UITextField("value");
            var communicationaddr = $("#communicationaddr1").UITextField("value");
            // var zipcode = $("#zipcode1").UITextField("value");
            var handset = $("#handset").UITextField("value");
            var email = $("#email1").UITextField("value");
            var bankfullname = $("#bankfullname").UITextField("value");
            var provincecode = action.constant.provincecode;
            var cityno = action.constant.cityno;
            var nationnal=$("#nationnal").UISelectField("value");
            var g = $.formGenerate();
            g.add("tradepassword", tradepassword)
                .add("sex", sex)
                .add("birthday", birthday)
                .add("workcode", workcode)
                .add("communicationaddr", communicationaddr)
                .add("reckoningsendtype", "1")
                .add("reckoningmailtype", "2")
                .add("invalidate", action.constant.validDateEnd)
                .add("nationality2", nationnal)
                .add("provincecode", provincecode)
                .add("cityno1", cityno)
                .add("handset", action.constant.tel)
                .add("bankname", bankfullname)
                .add("email", email)
                .add("bankacco", action.constant.bankacco)
                .add("bankserial", action.constant.bankserial)
                .add("bankacconame", action.constant.customername)
                .add("detailcapitalmode", "01")
                .add("capitalmode", "AK")
                .add("customerappellation", action.constant.customername)
                .add("identityno", action.constant.zjhm)
                .add("identitytype", "0")
                .add("yinliancdcard", action.constant.yinliancdcard)
                .add("accoreqserial", action.constant.accoreqserial)
                .add("modifycrsinfo", "true")
                .add("crsjson", encodeURIComponent('{main:{oricustflag:0}}'));
            var data = g.generate();
            $.hsf.ajax.app("changjiangpension/assetManagementEntrance/openAccoNP", data, "merOpenCallback", function (jsonResult) {
                if (jsonResult.successful) {
                    //$.hsf.stopLoading();
                    $("input[name='allotno']").val(jsonResult.applyserial);
                    // var data = "requestno="+jsonResult.applyserial+"&tradeacco="+jsonResult.tradeacco+"&tradeflag=1";
                    // $.hsf.hsTools.uploadSaveIPInfo(data);
                    action.idcardUpload("idrecoform");
                    // $("#ktzgForm").hide();
                    // $("#ktzgResult").show();
                } else {
                    $.hsf.callFailProcess(jsonResult);
                }
            });
        },
        getBirthdayFromCard: function (identityno) {
            var year = 2000;
            var month = 12;
            var day = 31;
            if (identityno.length == 15) {
                year = "19" + identityno.substr(6, 2);
                month = identityno.substr(8, 2);
                day = identityno.substr(10, 2);
            } else if (identityno.length == 18) {
                year = identityno.substr(6, 4);
                month = identityno.substr(10, 2);
                day = identityno.substr(12, 2);
            }
            return year + "-" + month + "-" + day;
        },
        getSexFromCard: function (identityno) {
            var sex = 0;
            if (identityno.length == 15) {
                sex = identityno.substr(13, 1);
            } else if (identityno.length == 18) {
                sex = identityno.substr(16, 1);
            }
            return sex % 2;
        },
        choose: function () {
            $("#n5").show();
            $("#one").hide();
        },
        validateyzm: function () {
            var mobile = action.constant.tel = $("#tel").UITextField("value").trim();
            var identitytype = "0";
            var identityno = $("#idNo").UITextField("value").trim();
            var bankacco = $("#bankacco").UITextField("value");
            var customername = $("#username").UITextField("value");

            var bankserial = action.constant.bankserial;
            var capitalmode = action.constant.capitalmode;
            var mobilereg = /^[0-9]{11}$/;
            var cerfiticate18 = /^((11|12|13|14|15|21|22|23|31|32|33|34|35|36|37|41|42|43|44|45|46|50|51|52|53|54|61|62|63|64|65|71|81|82|91)\d{4})((((19|20)(([02468][048])|([13579][26]))0229))|((20[0-9][0-9])|(19[0-9][0-9]))((((0[1-9])|(1[0-2]))((0[1-9])|(1\d)|(2[0-8])))|((((0[1,3-9])|(1[0-2]))(29|30))|(((0[13578])|(1[02]))31))))((\d{3}(x|X))|(\d{4}))$/;
            if (!mobilereg.test(mobile)) {
                $.UIAlert("手机号错误。");
                return false;
            }
            if (!cerfiticate18.test(identityno)) {
                $.UIAlert("身份证号码错误。");
                return false;
            }
            if (customername.length == 0 || customername == "") {
                $.UIAlert("姓名不能为空。");
                return false;
            }
            if (bankserial.length == 0 || bankserial == "") {
                $.UIAlert("不能为空。");
                return false;
            }
            if (capitalmode.length == 0 || capitalmode == "") {
                $.UIAlert("不能为空。");
                return false;
            }
            return true;
        },
        validate1: function () {
            var idType = "1";//身份证
            var username = $("#username").UITextField("value");
            var bankname = $(".selectedBankName").html();
            var bankacco = $("#bankacco").UITextField("value");
            var tel = $("#tel").UITextField("value");
            var idNo = $("#idNo").UITextField("value");
            //先验证身份证号码是否正确
            var cerfiticate18 = /^((11|12|13|14|15|21|22|23|31|32|33|34|35|36|37|41|42|43|44|45|46|50|51|52|53|54|61|62|63|64|65|71|81|82|91)\d{4})((((19|20)(([02468][048])|([13579][26]))0229))|((20[0-9][0-9])|(19[0-9][0-9]))((((0[1-9])|(1[0-2]))((0[1-9])|(1\d)|(2[0-8])))|((((0[1,3-9])|(1[0-2]))(29|30))|(((0[13578])|(1[02]))31))))((\d{3}(x|X))|(\d{4}))$/;
            if (username.length == 0) {
                $.UIPopup("请输入姓名！");
                return false;
            }
            if (bankname.length == 0) {
                $.UIPopup("请选择银行名称！");
                return false;
            }
            if (!cerfiticate18.test(idNo)) {
                $.UIPopup("请输入正确的18位身份证号码！");
                return false;
            }
            return true;

        },
        validate2: function () {
            var communicationaddr = action.constant.communicationaddr = $("#communicationaddr").UITextField("value");

            var zjhm = $("#idNo").UITextField("value");
            var yhkh = action.constant.bankacco = $("#bankacco").UITextField("value");
            var khyh = action.constant.bankname = $(".selectedBankName").html();
            var ylsjh = action.constant.tel = $("#tel").UITextField("value");
            var validatedCode = action.constant.authcode;

            var username = action.constant.username = $("#username").UITextField("value");
            var email = action.constant.email = $("#email").UITextField("value");
            // var zipcode = action.constant.zipcode = $("#zipcode").UITextField("value");
            var tradepassword = action.constant.tradepassword = $("#tradepassword").UITextField("value");
            var tradepassword2 = $("#tradepassword2").UITextField("value");
            var provincecode = action.constant.provincecode = $("#provincecode").UISelectField("value");
            var province = action.constant.province = $("#province").find("option:selected").text();
            var cityno = action.constant.cityno = $("#cityno").UISelectField("value");
            var city = action.constant.city = $("#city").find("option:selected").text();
            var bankweb = action.constant.bankweb = $("#bankweb").UITextField("value");
            var emailreg = /^([a-zA-Z0-9_\.\-])+@([a-zA-Z0-9_-])+((\.[a-zA-Z0-9_-]{2,3}){1,2})$/;//验证邮箱
            var zipreg = /^\d{6}$/;
            var pwdreg = /^\d{6}$/;
            if (communicationaddr.length == 0) {
                $.UIPopup("通讯地址不能为空");
                return false;
            }
            //验证邮箱
            if (email.length != 0 && !emailreg.test(email)) {
                $.UIPopup("邮箱格式不正确");
                return false;
            }
            if (bankweb.length == 0) {
                $.UIPopup("网点名称不能为空");
                return false;
            }
            if (validatedCode.length == 0) {
                $.UIPopup("验证码不能为空");
                return false;
            }
            //验证邮编
            // if (!zipreg.test(zipcode)) {
            //     $.UIPopup("邮编输入不正确！");
            //     return false;
            // }
            if (!pwdreg.test(tradepassword) || !pwdreg.test(tradepassword2)) {
                $.UIPopup("输入密码必须是6位纯数字");
                return false;
            }
            //新密码
            if (tradepassword.length == 0 || tradepassword2.length == 0) {
                $.UIPopup("密码不能为空");
                return false;
            }
            if (tradepassword.length != 6) {
                $.UIPopup("密码长度需要为6");
                return false;
            }
            if (tradepassword != tradepassword2) {
                $.UIPopup("两次输入密码不一致");
                return false;
            }
            return true;
        },
        validate3: function () {
            var pw1 = $("#password").UITextField("value");
            var pw2 = $("#password2").UITextField("value");
            var pwdreg = /^\d{6}$/;

            if (pw1.length == 0 || pw2.length == 0) {
                $.UIPopup("交易密码不能为空");
                return false;
            }
            if (pw1 != pw2) {
                $.UIPopup("两次输入的交易密码不一样");
                return false;
            }
            if (!pwdreg.test(pw1) || !pwdreg.test(pw2)) {
                $.UIPopup("输入密码必须是6位数字");
                return false;
            }
            if (pw1.length != 6 || pw2.length != 6) {
                $.UIPopup("密码长度必须是6位");
                return false;
            }
            return true;

        },
        openclock: function (id) {
            var counter = 0;
            var $btn = $("#" + id);
            return {
                start: function () {
                    var run = function () {
                        if (counter == 0) {
                            $btn.attr("m-state", "").html("获取");
                        } else {
                            $btn.html("剩余" + (counter--) + "秒");
                            setTimeout(run, 1000);
                        }
                    }
                    counter = 60;
                    $btn.attr("m-state", "disabled").html("剩余" + (counter--) + "秒");
                    setTimeout(run, 1000);
                },
                readyStart: function () {
                    return counter == 0;

                }
            }
        },
        //重置密码
        resetPwd: function () {
            //给资管页面赋值
            $("#communicationaddr1").UITextField("value", action.constant.communicationaddr);
            // $("#zipcode1").UITextField("value", action.constant.zipcode);
            $("#email1").UITextField("value", action.constant.email);
            $("#bankfullname").UITextField("value", action.constant.bankweb);
            $("#cityno1").html(action.constant.city);
            $("#provincecode1").html(action.constant.province);

            //年金重置密码
            var password = action.constant.tradepassword;
            var idcode = action.constant.zjhm;
            var data = "password=" + password + "&idcode=" + action.constant.zjhm + "&idtype=1";
            $.hsf.ajax.app("changjiangpension/resetPersonalPassword/queryResetPersonalPassword", data, "", function (jsonResult) {
                if (jsonResult.successful) {
                    action.openNj();
                } else {
                    $.UIAlert("找回密码失败,请重新找回年金密码！", function () {
                        $.hsf.hsOpen("nj-open-form.html");
                        return false;
                    });
                }
            });
        },
        convertBankname: function (bankname) {
            var name = bankname;
            if (bankname == "浦发银行") {
                name = "上海浦东发展银行";
            }
            if (bankname == "光大银行") {
                name = "中国光大银行";
            }
            return name;
        },
        //绑定银行卡
        bindCard: function () {
            //查询银行卡
            var data = "zjhm=" + action.constant.zjhm + "&zjlx=1";
            $.hsf.ajax.app("changjiangpension/njBankCard/queryNjBankCard", data, "", function (jsonResult) {
                if (jsonResult && jsonResult.code == "ETS-5BP00000" && jsonResult.result.Item) {

                } else {//没有绑定
                    var xm = action.constant.username;
                    var zjlx = "1";
                    var zjhm = action.constant.zjhm;
                    var yhkh = action.constant.bankacco;
                    var khyh = action.convertBankname(action.constant.bankname);
                    var ylsjh = action.constant.tel;
                    var lxdz = action.constant.communicationaddr;
                    // var yzbm = action.constant.zipcode;
                    var khyhszs = action.constant.province;
                    var khyhszshi = action.constant.city;
                    var khyhwdqc = action.constant.bankweb;
                    var data = "xm=" + xm + "&yhkh=" + yhkh + "&khyh=" + khyh + "&ylsjh=" + ylsjh + "&lxdz=" + lxdz + "&khyhszs=" + khyhszs + "&khyhszshi=" + khyhszshi + "&khyhwdqc=" + khyhwdqc + "&zjlx=1" + "&zjhm=" + action.constant.zjhm;
                    $.hsf.ajax.app("changjiangpension/njBindingBankCard/queryNjBindingBandCard", data, "", function (jsonResult) {
                        if (jsonResult.code == "ETS-5BP00000") {

                        } else {
                            //$.hsf.callFailProcess(jsonResult);
                        }
                    });
                }
            });
        },
        validateZG: function () {
            var communicationaddr = action.constant.communicationaddr = ($("#communicationaddr1").UITextField("value") || "").trim();
            var username = action.constant.username = $("#username").UITextField("value");
            var email = action.constant.email = ($("#email1").UITextField("value") || "").trim();
            var tradepassword = action.constant.tradepassword = $("#tradepassword").UITextField("value");
            var tradepassword2 = $("#tradepassword2").UITextField("value");
            var provincecode = $("#provincecode").UISelectField("value");
            var province = action.constant.province = $("#province").find("option:selected").text();
            var cityno = $("#cityno").UISelectField("value");
            var city = action.constant.city = $("#city").find("option:selected").text();
            var bankweb = action.constant.bankweb = $("#bankweb").UITextField("value");
            var emailreg = /^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+((\.[a-zA-Z0-9_-]{2,3}){1,2})$/; //验证邮箱
            if (communicationaddr.length == 0) {
                $.UIAlert("通讯地址不能为空。");
                return false;
            }
            //验证邮箱
            // if(email == ""){
            //     $.UIAlert("请输入邮箱!");
            //     return false;
            // }
            // 邮箱非必填
            if (email != "" && !emailreg.test(email)) {
                $.UIAlert("邮箱格式不正确");
                return false;
            }
            if (bankweb.length == 0) {
                $.UIAlert("请输入网点名称");
                return false;
            }
            // //验证邮编
            // if(!zipreg.test(zipcode)){
            //     $.UIAlert("邮编输入不正确！");
            //     return false;
            // }
            if ($("[m-name='checkBox']").attr("m-checked") != "yes") {
                $.UIAlert("您还没有勾选并同意《投资事项确认与风险提示》和《浦发集中代收付授权书》！");
                return false;
            }
            return true;
        },
        idcardUpload: function (id) {
            var formData = new FormData();
            formData.append("allotno", $("input[name='allotno']").val());
            for (var i = 0; i < action.constant.imageFileList2.length; i++) {
                formData.append(action.constant.imageFileList2[i].key, action.constant.imageFileList2[i].value);
            }
            $.ajax({
                url: $.hsf.appBaseUrl+"fileupload", // 提交的URL, 默认使用FORM  ACTION
                type: 'post',
                data: formData,
                dataType : "json",
                processData: false, // 告诉jQuery不要去处理发送的数据
                contentType: false, // 告诉jQuery不要去设置Content-Type请求头
                success: function (data) {
                    $.hsf.stopLoading();
                    $("#ktzgForm").hide();
                    $("#uploadcard").hide();
                    $("#uploadpwd").hide();
                    $("#ktzgResult").show();
                },
                error: function (data) {
                    $.hsf.stopLoading();
                    $("#ktzgForm").hide();
                    $("#uploadcard").hide();
                    $("#uploadpwd").hide();
                    $("#ktzgResult").show();
                }
            });
        },
        ocrIdcardUpload: function(){
            $.hsf.startLoading();
            action.constant.imageFileList = [];
            action.constant.imageFileList2 = [];
            var formData = new FormData();
            var logo_file = document.getElementById("pic");
            var logoFileObj = logo_file.files[0];
            logoFileObj.id="sfzzm";
            var logo_file1 = document.getElementById("pic1");
            var logoFileObj1 = logo_file1.files[0];
            logoFileObj1.id="sfzfm";
            action.constant.imageFileList.push(logoFileObj);
            action.constant.imageFileList.push(logoFileObj1);
            action.getBase64(action.constant.imageFileList).then(function(imageFileCompress) {
                for (var i = 0; i < imageFileCompress.length; i++) {
                    formData.append(imageFileCompress[i].key, imageFileCompress[i].value);
                }
                $.ajax({
                    url: $.hsf.appBaseUrl+"changjiangpension/identityAndLiveDetect/cardRecognize.json", // 提交的URL, 默认使用FORM  ACTION
                    type: 'post',
                    data: formData,
                    dataType : "json",
                    processData: false,  // 告诉jQuery不要去处理发送的数据
                    contentType: false,  // 告诉jQuery不要去设置Content-Type请求头
                    success: function (data) {
                        $.hsf.stopLoading();
                        if("ETS-5BP00000" == data.code){
                            var vail = data.content.validDateEnd;
                            if("长期" == vail){
                                data.content.validDateEnd = "99991231";
                            }
                            action.constant.custname=data.content.name;
                            action.constant.idno=data.content.cardNo;
                            action.constant.validDateEnd=data.content.validDateEnd;
                            action.constant.sex=data.content.gender;
                            $("#username").UITextField("value", action.constant.custname);
                            $("#idNo").UITextField("value", action.constant.idno);
                            var checkdata = "autoflag=0&identityno="+ action.constant.idno + "&identitytype=0&fullcustomname=" + action.constant.custname;
                            $.hsf.startLoading();
                            $.hsf.ajax.app("account/check/checkBlackList", checkdata, "", function (jsonResult) {
                                if (jsonResult.successful) {
                                    $.hsf.stopLoading();
                                    if(jsonResult.blackflag == "1"){//是黑名单用户
                                        $.UIAlert("您是黑名单用户，不能开户");
                                        return false;
                                    }else{//不是黑名单用户
                                        $("#ocrcustname").html(data.content.name);
                                        $("#ocridno").html(data.content.cardNo);
                                        if("长期" == vail){
                                            $("#ocrinvalidate").html(vail);
                                        }else{
                                            $("#ocrinvalidate").html($.hsf.hsTools.yyyy_mm_dd(data.content.validDateEnd));
                                        }
                                        $("#ocrinvalidate").html($.hsf.hsTools.yyyy_mm_dd(data.content.validDateEnd));
                                        $("#ktzgForm").hide();
                                        $("#uploadcard").hide();
                                        $("#uploadpwd").hide();
                                        $("#ktzgResult").hide();
                                        $("#seven").show();
                                    }
                                } else {
                                    $.hsf.callFailProcess(jsonResult);
                                }
                            })
                        }else{
                            $.hsf.stopLoading();
                            $.UIAlert("识别失败，请靠近您的身份证件重新拍摄/上传清晰照片！");
                        }
                    },
                    error: function (data) {
                        $.hsf.stopLoading();
                        $.UIAlert("识别失败，请重新上传", function() {
                            history.back();
                        });
                    }
                })
            },function (error) {
                $.hsf.stopLoading();
                $.UIAlert("图片压缩失败！");
            });
        },
        getBase64: function (files) {
            var that = this;
            var imageFileCompress = [];//记录压缩过的个图片集合
            function dealImage(base64, w, callback, currentTarget) {
                var newImage = new Image();
                var quality = 0.6;    //压缩系数0-1之间
                newImage.src = base64;
                newImage.setAttribute("crossOrigin", 'Anonymous');	//url为外域时需要
                var imgWidth, imgHeight;
                newImage.onload = function () {
                    imgWidth = this.width;
                    imgHeight = this.height;
                    var canvas = document.createElement("canvas");
                    var ctx = canvas.getContext("2d");
                    if (Math.max(imgWidth, imgHeight) > w) {
                        if (imgWidth > imgHeight) {
                            canvas.width = w;
                            canvas.height = w * imgHeight / imgWidth;
                        } else {
                            canvas.height = w;
                            canvas.width = w * imgWidth / imgHeight;
                        }
                    } else {
                        canvas.width = imgWidth;
                        canvas.height = imgHeight;
                        quality = 0.6;
                    }
                    ctx.clearRect(0, 0, canvas.width, canvas.height);
                    ctx.drawImage(this, 0, 0, canvas.width, canvas.height);
                    var base64 = canvas.toDataURL("image/jpeg", quality); //压缩语句
                    // 如想确保图片压缩到自己想要的尺寸,如要求在50-150kb之间，请加以下语句，quality初始值根据情况自定
                    while (base64.length / 1024 > 100) {
                    	quality -= 0.01;
                    	base64 = canvas.toDataURL("image/jpeg", quality);
                    }
                    // 防止最后一次压缩低于最低尺寸，只要quality递减合理，无需考虑
                    // while (base64.length / 1024 < 50) {
                    // 	quality += 0.001;
                    // 	base64 = canvas.toDataURL("image/jpeg", quality);
                    // }
                    callback(base64,currentTarget);//必须通过回调函数返回，否则无法及时拿到该值
                }
            }
     
            function printing(base64,currentTarget) {
                var type = base64.match(/data:image\/[\s\S]*;base64,/).toString();
                var fileextname = type.replace("data:image/", "").replace(";base64,", "");//截取文件类型
                imageFileCompress.push({ key: currentTarget.name, value: base64 });
                imageFileCompress.push({ key: currentTarget.name + "type", value: fileextname });

                // 识别成功后上传的数据
                base64 = base64.replace(/data:image\/[\s\S]*;base64,/, "");
                action.constant.imageFileList2.push({key: currentTarget.name, value: base64});
                action.constant.imageFileList2.push({key: currentTarget.name+"type", value: fileextname});
                if (imageFileCompress.length == action.constant.imageFileList.length + action.constant.imageFileList.length) {
                    deferred.resolve(imageFileCompress);//将base64传给done上传处理
                }
            };
            var deferred = $.Deferred();
            var images = [];
            for (var i = 0; i < files.length; i++) {
                var objUrl = that.getObjectURL(files[i]);
                var image = new Image();
                image.crossOrigin = '';
                image.src = objUrl;
                image.sizes = files[i].size;
                image.name = files[i].id;
                images.push(image);
                if (objUrl) {
                    images[i].onload = function (e) {
                        var base64 = "";
                        var _currtName = e.currentTarget.name == "sfzzm" ? "#id_cropped_image":"#id_cropped_image1";
                        base64 = $(_currtName).attr("src");
                        base64 = dealImage(base64, 800, printing, e.currentTarget);
                    }
                }
            }
            return deferred.promise();
        },
        getObjectURL:function(file) {
            var url = null;
            if (window.createObjectURL != undefined) { // basic
                url = window.createObjectURL(file);
            } else if (window.URL != undefined) { // mozilla(firefox)
                url = window.URL.createObjectURL(file);
            } else if (window.webkitURL != undefined) { // webkit or chrome
                url = window.webkitURL.createObjectURL(file);
            }
            return url;
        },
        //渲染压缩图片
        //长宽压缩比例rateRatio  图片压缩大小比例sizeRatio
        renderPic: function (imgId, reader, file, fileSize, rateRatio, sizeRatio) {
            //控制大于多少才压缩： 300K
            var zipSize = 1024 * 300;
            var image = new Image(),
                canvas = document.createElement("canvas");
            //图片元素加载
            reader.onload = function (e) {
                //获取缓存的图片对象
                image.src = reader.result;
                var newImageData = '';
                newImageData = e.target.result;
                $('#' + imgId).attr("src", newImageData);
            }
        },
        checkColor: function (cls) {
            var color = $(cls).css('background-color');
            return color === 'rgb(21, 101, 192)';
        },
        // 是一样的图片
        isSamePictures: function () {
            var img1 = $('#id_cropped_image').attr('src');
            var img2 = $('#id_cropped_image1').attr('src');
            if (img1 === img2) {
                $.UIAlert('两张图片相同。');
                return false;
            }
            return true;
        },
        // 查看格式
        checkFormat: function (type) {
            return type === "image/jpeg" || type === "image/jpg" || type === "image/png" || type === "image/bmp";
        },
        //图片类型验证
        checkFile: function (e) {
            try {
                var filepath = e.target.value;
                if (filepath === "") {
                    return false;
                }
                var file = e.target.files[0];
                var fileSize = e.target.files[0].size;
                var is_format = action.checkFormat(file.type);
                var perM = 1048576; //1024*1024;
                if (parseFloat(fileSize / perM) > 8.0) {
                    $.UIAlert("您上传的文件超出限制大小！请保证单张影印件在8M以内。");
                    return;
                }
                if (fileSize <= 0) {
                    return false;
                }
                //判断文件格式
                if (!is_format) {
                    $.UIAlert("文件类型必须是bmp,jpeg,jpg,png中的一种");
                    return false;
                }
                return true;
            } catch (e) {
                console.log(e);
                return false;
            } finally {
                //
            }
        },
        //开通资管
        openZg: function () {
            //是否已经开通资管
            $("#four").show();
            $("#one").hide();
            $("#two").hide();
            $("#three").hide();
            $("#n5").hide();
            this.checkFiscalResident();
            return false;
        },
        // 是否是居民身份
        checkFiscalResident: function() {
            $.UIConfirm({html:'<div style="font-weight:normal;"><h3 style="text-align:center;padding-bottom:.5em;font-size:1.2em;">请确认是否为中国税收居民</h3><p style="color:#666;text-align: center;">根据相关法规，非中国税收居民无法直接开户及申购。请确认是否为中国税收居民或联系客服热线400-820-9966</p></div>',cancelText:'确认',submitText:'取消'},
                function(isOk){
                    if(isOk === "yes"){
                        $.hsf.hsOpen("bind.html");
                    }
                }
            )
        },
        //开通年金
        openNj: function () {
            var certificatetype = "0";
            var mobile = action.constant.tel;
            var identityno = action.constant.zjhm;
            var n = "sendintent=openacco" + "&mobile=" + mobile + "&identityno=" + identityno + "&identitytype=" + certificatetype;
            $.hsf.startLoading();
            var data = "certificatetype=" + certificatetype + "&lognumber=" + action.constant.zjhm + "&password=" + action.constant.tradepassword + "&channel=" + $.platform.channel + "&bindwx=1" + "&mobile=" + action.constant.tel;
            $.hsf.ajax.app("changjiangpension/bindingAccount/queryBindingNJAccount", data, "", function (jsonResult) {
                if (jsonResult.code == "ETS-5BP00000") {
                    //绑定银行卡
                    $.hsf.stopLoading();
                    action.bindCard();
                    //判断是否已开资管户
                    $.when(action.isBindZg()).done(function (r) {
                        if (r.successful) {//已开资管户，自动绑定
                            var data = "certificatetype=0" + "&lognumber=" + action.constant.zjhm + "&channel=" + $.platform.channel + "&bindwx=1" + "&mobile=" + action.constant.tel;
                            $.hsf.ajax.app("changjiangpension/bindingAccount/queryBindingZGAccount", data, "", function (jsonResult) {
                                $.UIAlert("成功开通年金及资管服务。", function () {
                                    $.hsf.hsOpen("index.html");
                                    return false;
                                });
                            });

                        } else {//未开资管户，提示去开户
                            $.UIConfirm({
                                "html": "开通年金成功，是否需要开通资管账户服务？",
                                "submitText": "是",
                                "cancelText": "否"
                            }, function (result) {
                                if (result == "yes") {
                                    $("#one").hide();
                                    $("#two").hide();
                                    action.openZg();
                                } else if (result == "no") {
                                    $("#one").hide();
                                    $("#two").hide();
                                    $("#three").show();
                                    $("#four").hide();
                                }
                            });
                        }
                    });
                } else {
                    $.hsf.stopLoading();
                    $.UIAlert("找回密码成功，请去绑定页面进行绑定！", function () {
                        $.hsf.hsOpen("bind.html");
                        return false;
                    });
                }
            })
        },
        isBindZg: function () {
            //查询资管用户是否已经开通接口
            var identityno = action.constant.zjhm;
            var data = "identityno=" + identityno + "&identitytype=0";
            return $.hsf.ajax.app("changjiangpension/assetManagementEntrance/getIsOpenAcco", data, "", function (jsonResult) {
            });
        },
        //通过select获取的banklist
        banklistOrigin: [
            {"bankserial": "002", "msg": "中国工商银行"},
            {"bankserial": "012", "msg": "光大银行"},
            {"bankserial": "020", "msg": "平安银行"},
            {"bankserial": "009", "msg": "浦发银行"},
            {"bankserial": "003", "msg": "中国农业银行"},
            {"bankserial": "005", "msg": "中国建设银行"},
            {"bankserial": "004", "msg": "中国银行"},
            {"bankserial": "011", "msg": "兴业银行"},
            {"bankserial": "017", "msg": "华夏银行"},
            {"bankserial": "008", "msg": "中信银行"},
            {"bankserial": "006", "msg": "交通银行"}
        ],
        banklistChangjiang: [
            {"bankserial": "01020000", "msg": "中国工商银行"},//1
            {"bankserial": "01030000", "msg": "中国农业银行"},//5
            {"bankserial": "01040000", "msg": "中国银行"},//7
            {"bankserial": "01050000", "msg": "中国建设银行"},//6
            {"bankserial": "03010000", "msg": "交通银行"},//12
            {"bankserial": "03100000", "msg": "上海浦东发展银行"},//4
            {"bankserial": "03090000", "msg": "兴业银行"},//8
            {"bankserial": "03020000", "msg": "中信银行"},//11
            {"bankserial": "03040000", "msg": "华夏银行"},//9
            {"bankserial": "03030000", "msg": "中国光大银行"},//2
            {"bankserial": "03135840", "msg": "平安银行"},//3
        ]

    };


    return action;
});
```

