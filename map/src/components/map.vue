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
    // 如遇见2个报错 请使用this.$nextTick ***（上次写项目的时候遇见了，这次 不见了。。。。。。）

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
