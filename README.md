# sewise播放器3.2.1_release版本

## 主要特性 
1、 全新的架构，代码结构更加合理清晰，简洁易懂，易扩展，易维护。 
2、 flash和html5播放器共用一套皮肤。 
3、 支持一个页面多个播放器实例同时播放 
4、 轻松支持插件扩展 
## 播放器使用方式： 
### 一：(1)播放器嵌入方式（一个页面只能嵌入一个播放器）

.点播，实际地址播放
```html
<div style="width: 640px; height: 360px; "> 
<script type="text/javascript" src="sewise.player.min.js#url=http://www.w3schools.com/html/mov_bbb.mp4&autostart=true&starttime=0&lang=en_US&logo=http://onvod.sewise.com/libs/swfplayer/skin/images/logo.png&title=VodVideo&buffer=5&skin=vodWhite"></script> 
</div>
```
.点播，节目ID播放。
```html
<div style="width: 640px; height: 360px; "> 
<script type="text/javascript" src="sewise.player.min.js#url=vod://192.168.3.88/eQgPHj4N&autostart=true&starttime=0&lang=en_US&logo=http://onvod.sewise.com/libs/swfplayer/skin/images/logo.png&buffer=5&skin=vodWhite"></script> 
</div>
```
.直播，实际地址播放。
```html
<div style="width: 640px; height: 360px; "> 
<script type="text/javascript" src="sewise.player.min.js#url=rtmp://219.232.161.204/livestream/mtzysunq&autostart=true&shifttime=&lang=en_US&logo=http://onvod.sewise.com/libs/swfplayer/skin/images/logo.png&title=LiveVideo&skin=liveWhite"></script> 
</div>
```
.直播，节目ID播放。
```html
<div style="width: 640px; height: 360px; "> 
<script type="text/javascript" src="sewise.player.min.js#url=live://192.168.3.88/vk5nx2cj/rtmp&autostart=true&shifttime=&lang=en_US&logo=http://onvod.sewise.com/libs/swfplayer/skin/images/logo.png&skin=liveWhite"></script> 
</div>
```
### (2)播放器实例化方式（支持一个页面多个播放器实例） 
.点播实际地址播放
```javascript
var config={ 
elid:"container1",//包裹播放器的div容器ID属性值 
autostart:true, 
url:"video/test.mp4", 
skin:"vodWhite" 
}; 
var config2={ 
elid:"container2",//包裹播放器的div容器ID属性值 
autostart:true, 
url:"video/test2.m3u8", 
skin:"vodTransparent" 
}; 
$(document).ready(dowReady);//页面加载完成 
var player,player2; 
function dowReady(){ 
player=new Sewise.SewisePlayer(config); 
player.startup(); 
player2=new Sewise.SewisePlayer(config2); 
player2.startup(); 
}; 
```
.点播节目ID播放 
只要把上面config对象的url属性设置成如下格式: url:"vod://192.168.3.88/dff999"。 
"dff999"表示节目ID。

.直播实际地址播放 
```javascript
var config={ 
elid:"container1",//包裹播放器的div容器ID属性值 
autostart:true, 
url:"rtmp://192.168.1.53:1935/livestream/2bsprtda", 
duration:3600, 
skin:"liveWhite" 
}; 
var config2={ 
elid:"container2",//包裹播放器的div容器ID属性值 
autostart:true, 
server:"live", 
url:"http://192.168.1.53:1935/livestream/3ggprtda.m3u8", 
duration:3600, 
skin:"liveWhite" 
}; 
$(document).ready(dowReady);//页面加载完成 
var player,player2; 
function dowReady(){ 
player=new Sewise.SewisePlayer(config); 
player.startup(); 
player2=new Sewise.SewisePlayer(config2); 
player2.startup(); 
};
```
.直播节目ID播放
只要把上面config对象的url属性设置成如下格式:
直播rtmp  url:"live://192.168.3.88/dff999/rtmp"
直播m3u8  url:"live://192.168.3.88/dff999/hls"
"dff999"表示节目ID。

## 二:API接口调用和说明
播放器嵌入方式：var player= window.SewisePlayer;
播放器实例化方式：var player=new Sewise.SewisePlayer(config);
### (1)点播直播通用接口
`
/*
 * 播放
 */
player.play();

/*
 * 暂停
 */
player.pause();

/*
 * 停止
 */
player.stop();

/*
 * 跳转到指定时间播放,
 * @param time 
 * time类型点播时为数值表示要跳转到的位置（秒），直播时为字符串表示要跳转到的日期（如：’20110503123456’）
 */
player.seek(time);

/*
 * 设置声音
 * @param volume 值0-1
 */
player.setVolume(volume);

/*
 * 设置是否静音
 * @param bool 值true,false
 */
palyer.muted(bool);

/*
 * 根据节目id播放视频
 * @param programId 节目ID
 * @param startTime 点播时值为(秒)，直播时值为(日期：’20110503123456’)
 * @param autostart 是否自动播放
 */
player.playProgram(programId, startTime, autostart);

/*
 * 根据视频地址播放
 * @param videoUrl 视频地址
 * @param title 节目标题
 * @param startTime 点播时为数值表示开始播放的位置（秒）。 直播时为字符串表示开始播放位置的日期:’20110503123456’
 * @param autostart 是否自动播放true false
 */
player.toPlay(videoUrl, title, startTime, autostart);

/*
 * 返回视频总时长(秒)
 */
player.duration();

/*
 * 返回当前播放时间位置、日期
 * 点播返回当前视频播放到的位置（秒），直播返回当前视频播放到的时间点（日期）
 */
player.playTime ();

/*
 * 获取播放器根容器
 */
player.getPlayerContainer();

/*
 * 获取视频容器
 */
player.getVideoContainer(); 

/*
 * 获取皮肤容器
 */
player.getSkinContainer();

/*
 * 获取视频元素对象
 */
player.getVideo();

/*
 * 设置播放速率(只支持html5)
 * 1.0 正常速度
 * 0.5 半速（更慢）
 * 2.0 倍速（更快）
 * -1.0 向后，正常速度
 * -0.5 向后，半速
 */
player.setPlaybackRate(value);

/*
 * 获取播放速率(只支持html5)
 */
player.getPlaybackRate();

/**
 * 强制刷新皮肤页面布局
 */
player.forceRefreshSkinSize();

/**
 * 开启全屏（必须用户手动触发，比如通过点击按钮事件调用这个接口触发）
 */
player.fullScreen();

/**
 * 退出全屏
 */
player.normalScreen();

### (2)点、直播专用接口方法

/* 点播方法
 * 更新多清晰度播放列表
 * jsonObj(json对象)--- 对应播放器参数videosjsonurl
 */
player.updateVideosjsonurl(jsonObj);

/* 直播方法
 * 回到直播
 */
player.live();

/* 直播方法
 * 返回当前视频最新的直播时间日期
 */
player.liveTime();

/*直播方法
 * 设置直播时间跨度
 * value类型为数值，表示播放进度条上规化的时长
 * 默认值3600
 */
player.setDuration (value);
`
## 三、播放器回调的函数 
/* 
播放器准备好了 
*/ 
player.on("playerReady",function(){ 
});

/* 
*视频开始播放后回调的函数 
*/ 
player.on("start",function(){ 
});

/* 
*视频暂停播放后回调 
*/ 
player.on("pause",function(){ 
});

/* 
* 视频播放前回调 
*/ 
player.on("beforePlay",function(){ 
});

/* 
*视频停止播放后回调 
*/ 
player.on("ended",function(){ 
});

/* 
* 视频时长改变时回调 
*/ 
player.on("durationChange",function(){ 
});

/* 
*视频实时播放回调 
*/ 
player.on("timeupdate",function(){ 
});

/* 
* 视频加载进度回调 
* @parame pt 
*/ 
player.on("loadProgress",function(pt){ 
});

/* 
* 视频缓冲开始回调 
*/ 
player.on("bufferBegin",function(){ 
});

/* 
* 视频缓冲结束回调 
*/ 
player.on("bufferComplete",function(){ 
});

/* 
* 播放器获取到视频metadata信息后回调 
*/ 
player.on("metadata",function(obj){ 
});

/* 
* 视频时移播放后回调的函数 
/ 
player.on("seek",function(e){ 
}); 

/ 
* 皮肤控制条改变显示状态时回调 
*/ 
player.on("controlbarShowState",function(obj){ 
console.log(obj.isShow); 
});

/* 
* 全屏后回调 
*/ 
player.on("fullScreen",function(){ 
});

/* 
* 退出全屏后回调 
*/ 
player.on("cancelFullScreen",function(){ 
});

/* 
* flash端播放hls流时相关事件回调 
*/ 
player.on("hlsEvents",function(obj){ 
console.log("hls----"+obj.eventName+":"+obj.data); 
}); 
## 四：播放器参数说明

### 1、点、直播通用参数：

autostart 
* 说明：[可选]加载视频地址等信息后是否自动开始播放 
* 类型：字符串 
* 取值：”true”、”false”，为空表示：”true” 
* 对应：通用

skin 
说明：播放器皮肤 
类型：字符串 
取值：如，”vodOrange” 
对应：通用

type 
说明：[可选]播放视频类型，此参数不是必须的，播放器内部会通过url参数自行判断类型，如果视频地址比较特殊,需要设置此参数 
类型：字符串 
取值：”rtmp”、”flv”、”mp4”、”m3u8” 
对应：通用

title 
说明：[可选]所播放节目的标题 
类型：字符串 
取值：如，”深圳卫视” 
对应：通用

server 
说明：[可选]服务器类型 
类型：字符串 
取值：”vod”、live”，值为vod时播放器将启用点播模式，值为live时播放器将启用直播模式。 
对应：通用

lang 
说明：[可选]播放器显示语言 
类型：字符串 
取值：”en_US”或”zh_CN” 
对应：通用

logo 
说明：[可选]播放器logo 
类型：字符串 
取值：如，http://sewise.com/logo.png 
对应：通用

volume 
说明：[可选]播放器默认音量值 
类型：字符串 
取值：0 - 1 
对应：通用

poster 
说明：[可选]视频播放前显示的图像 
类型：字符串 
取值：如，http://www.sewise.com/img/01.png 
对应：通用

claritybtndisplay 
说明：[可选]是否显示多码率按钮 
类型：字符串 
取值：”enable”、”disable”，缺省默认值为：”enable” 
对应：通用

timedisplay 
说明：[可选]是否显示播放控制栏上的时间 
类型：字符串 
取值：”enable”、”disable”，缺省默认值为：”enable” 
对应：通用

controlbardisplay 
说明：[可选]是否显示播放控制栏 
类型：字符串 
取值：”enable”、”disable”，缺省默认值为：”enable” 
对应：通用

topbardisplay 
说明：[可选]是否显示顶部标题 
类型：字符串 
取值：”enable”、”disable”，缺省默认值为：”enable” 
对应：通用

bigplaybtndisplay 
说明：[可选]是否显示皮肤中间的大播放按钮 
类型：字符串 
取值：”enable”、”disable”，缺省默认值为：”enable” 
对应：通用

primary 
说明：[可选]播放器启用的优先模块，当视频、流同时支持HTML5或Flash播放时，该参数用于确定优先HTML5还是Flash播放。 
类型：字符串 
取值：如，”html5”, “flash”，缺省默认值为：”html5” 
对应：通用

playsinline 
说明：[可选]给html5的video标签增加webkit-playsinline属性 
类型：字符串 
取值：如true,false 
对应：通用

### 2.点播专用参数

url 
* 说明：点播视频时的播放地址 
* 类型：字符串 
* 取值：(1)视频地址播放 http://192.168.1.219:5080/flvseek/data/25102442M.flv (2)节目ID播放 vod://192.168.1.210/节目ID (3)当不想传入播放地址时，可以设置为url:"#" 
* 对应：flv、mp4、m3u8

videosjsonurl 
说明：点播视频时的JSON集播放地址(配合vodFlowPlayer皮肤用于多码率切换)，播放器同时必须设置type参数 
类型：字符串或JSON对象 
取值：如， 
```javascript
videosjsonurl: { 
“programname”:”节目名”, 
“videos”: [ 
{ “name”:”普通”, “url”:”http://219.232.161.206:5080/flvseek/201311/TRo4TUsO.flv” }, 
{ “name”:”标清”, “url”:”http://219.232.161.202:5080/flvseek/201402/OVNNwRk1.flv” } 
] 
} 
```
对应：flv、mp4、m3u8

fallbackurls 
说明：点播视频播放时的兼容回退地址，当url地址不支持时将一一验证回退地址的可播放性 
类型：字符串或JSON对象 
取值：如， 
```javascript
fallbackurls:{ 
mp4: "http://192.168.1.11/materials/mov_bbb.mp4", 
ogg: "http://192.168.1.11/materials/mov_bbb.ogg”, 
webm: "http://192.168.1.11/materials/mov_bbb.webm", 
m3u8: "http://192.168.1.11/materials/mov_bbb.m3u8" 
}
```
starttime 
说明：[可选]视频播放的开始时间 
类型：数值 
取值：开始播放的时间，如：234.341，缺省默认值为：从头开始 
对应：flv、mp4、m3u8

### 3.直播专用参数

url 
* 说明：直播视频时的播放地址 
* 类型：字符串 
* 取值：(1)视频地址播放rtmp://192.168.1.219:5080/livestream/v2qrgj3a；http://192.168.1.219:5080/hls/v2qrgj3a.m3u8 
(2)节目ID播放 live://192.168.1.219/节目ID/rtmp; live://192.168.1.219/节目ID/hls; 
(3)当不想传入播放地址时，可以设置为url:"#" 
* 对应：http、rtmp

duration 
说明：[可选]直播时播放器的进度条代表的时间跨度 
类型：数字 
取值：如：3600 
对应：http、rtmp

shifttime 
说明：[可选]直播启动播放时的开始播放时间 
类型：字符串 
取值：14位绝对时间字符串，如，20130413102312 
对应：http、rtmp

## 五：目录结构说明 
### (1)文件夹说明 
css文件夹：播放器css文件 
flash文件夹：flash播放器 
html文件夹：播放器皮肤文件 
js文件夹：播放器需要调用的js库文件 
plugin文件夹：播放器插件源代码（比如弹幕插件，浏览器播放m3u8视频插件） 
sewise.player.dev.js: 未压缩版本播放器源文件 
sewise.player.min.js: 压缩版本播放器源文件

### (2)皮肤介绍 
html文件夹里有四套点播皮肤(vod开头的文件夹)和一套直播皮肤(live开头的文件夹)； 
以vodWhite皮肤为例: skin.css 播放器皮肤的样式文件 
skin.html 播放器皮肤的DOM元素 
skin.html.js 播放器皮肤js格式的DOM元素,用于兼容跨域加载 
sewise.player.dev.js源代码里的SkinController类控制皮肤逻辑,自定义皮肤时可以修改里面的代码。