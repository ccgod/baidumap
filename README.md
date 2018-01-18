---
title: 调用百度地图接口
---
欢迎来到本CCgod的博客! 与大家一起学习 进步 grow up

## vue调用百度地图api
先去百度地图申请秘钥 [点击这里进入百度地图秘钥申请地址](http://lbsyun.baidu.com/apiconsole/key/create) '这个我就不做多解释了。。。。'。
如果不想申请 可以使用我的秘钥 但是如公开请 注明出处 谢谢  [点击这里查看demo](https://github.com/ccgod/baidumap) 喜欢的话点个星 Thank you ToT

然后呢打开vue的 index.html文件 在下面引入百度秘钥
``` bash
 <!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <title>map</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="text/javascript" src="http://api.map.baidu.com/api?v=2.0&ak=秘钥"></script>
  </body>
</html>
```


### 然后开始第二步吧 来不及了 先上代码 下面再解释

``` bash
<template>
  <div class="map">
    <h1>{{ msg }}</h1>
    <!-- 记得吧地图显示区域样式加上 -->
    <div id="l-map"></div>
    <a href="http://lbsyun.baidu.com/jsdemo.htm#i8_1" target="_bank">请点击此地方跳转到百度地图APi接口详细地址</a>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: "调用百度地图API"
    };
  },
  mounted() {
    // 请在此地方调用
    this.$nextTick(() => {
      this.BMap();
    });
  },
  methods: {
    BMap: function() {
      var map = new BMap.Map("l-map");
      var point = new BMap.Point(116.331398, 39.897445);
      map.centerAndZoom(point, 12);
      var geolocation = new BMap.Geolocation();
      geolocation.getCurrentPosition(
        function(r) {
          if (this.getStatus() == BMAP_STATUS_SUCCESS) {
            var mk = new BMap.Marker(r.point);
            map.addOverlay(mk);
            map.panTo(r.point);
            alert("您的位置：" + r.point.lng + "," + r.point.lat);
          } else {
            alert("failed" + this.getStatus());
          }
        },
        { enableHighAccuracy: true }
      );
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
  margin-top: 20px;
}
body,
html {
  width: 100%;
  height: 100%;
  margin: 0;
  font-family: "微软雅黑";
}
#l-map {
  height: 400px;
  margin: 30px auto;
  width: 100%;
}
#r-result {
  width: 100%;
  font-size: 14px;
  line-height: 20px;
}
</style>
```
切记使用的时候请写在methods钩子里面写调动事件  然后再 mounted调用  不然会一直报错 注：好像是'cg'这个错误  
调用事件里面的是  [百度地图的API ](http://lbsyun.baidu.com/jsdemo.htm#i8_1)


OK 结束了 ！！！！

### 顺便附上demo 记得喜欢的亲们来个star 谢谢各位老板

我的[demo](https://github.com/ccgod/baidumap)地址里面有我个人的秘钥

末尾 感谢大家的观看。。。。。

