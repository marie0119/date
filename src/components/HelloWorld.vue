<template>
  <div class="hello">
    <div id="allmap">

    </div>
    <div>{{address}}</div>
  </div>
</template>

<script>
var lng;
var lat;
export default {
  name: 'HelloWorld',
  data () {
    return {
      address:''
    }
  },
  mounted(){
    // 百度地图API功能
    var map = new BMap.Map("allmap");
    var point = new BMap.Point(116.331398,39.897445);
    map.centerAndZoom(point,12);
    var that=this;
    var geolocation = new BMap.Geolocation();
    geolocation.getCurrentPosition(function(r){
      if(this.getStatus() == BMAP_STATUS_SUCCESS){
        var mk = new BMap.Marker(r.point);
        map.addOverlay(mk);
        map.panTo(r.point);
        // alert('您的位置：'+r.point.lng+','+r.point.lat);
        lng=r.point.lng;
        lat=r.point.lat;
        // map.centerAndZoom(new BMap.Point(116.404, 39.915), 11);
// 创建地理编码实例
        var myGeo = new BMap.Geocoder();
// 根据坐标得到地址描述
        myGeo.getLocation(new BMap.Point(lng,lat), function(result){
          if (result){
            // alert(result.address);
            that.address=result.address;
          }
        });
      }
      else {
        alert('failed'+this.getStatus());
      }
    },{enableHighAccuracy: true})
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
