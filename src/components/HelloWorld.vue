<template>
  <div class="hello">
    <div id="allmap">

    </div>

  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  data () {
    return {
    }
  },
  mounted(){
    var map = new BMap.Map("allmap");
    var point = new BMap.Point(116.331398,39.897445);
    map.centerAndZoom(point,12);

    var geolocation = new BMap.Geolocation();
// 开启SDK辅助定位
    geolocation.enableSDKLocation();
    geolocation.getCurrentPosition(function(r){
      if(this.getStatus() == BMAP_STATUS_SUCCESS){
        var mk = new BMap.Marker(r.point);
        map.addOverlay(mk);
        map.panTo(r.point);
        alert('您的位置：'+r.point.lng+','+r.point.lat);
      }
      else {
        alert('failed'+this.getStatus());
      }
    });
  },
  methods: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #allmap {
    width: 100%;
    height: 300px;
  }
</style>
