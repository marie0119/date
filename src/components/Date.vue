<template>
  <div class="date">
    <div class="header">
      <div class="left" @click="preMonth">left</div>
      <div class="center">{{year}}年{{month}}月</div>
      <div class="right" @click="nextMonth">right</div>
    </div>
    <div class="container">
      <div class="item" v-for="item in header">{{item}}</div>
      <div class="item gray" v-for="item in lastMonthDays">{{item}}</div>
      <div class="item" v-for="(item,index) in monthDays" @click="choose(index)">
        <div class="day" :class="{active:index==day,'choose-item':chooseId==index,'sign-item':item.sign==1}">
          {{item.day}}
        </div>
      </div>
      <div class="item gray" v-for="item in endWeekDay">{{item}}</div>
    </div>
    <div>
      <label>照相机</label>
      <input type="file" id='image' accept="image/*" capture='camera' multiple @change="changeFn" ref="inputfile">
    </div>
  </div>
</template>

<script>
  export default {
    name: "Date",
    data() {
      return {
        header: ['日', '一', '二', '三', '四', '五', '六'],
        monthDays: [],
        lastMonthDays: [],
        year: '',
        month: '',
        day: '',//控制当天样式
        chooseId: -1,//当前点击id
        signDays: [],//签到过日期
        startDay: '',//当前月第一天是周几
        endWeekDay:'',
      }
    },
    mounted() {

      //-------------------

      var now = new Date();
      var year = now.getFullYear();
      var month = now.getMonth() + 1;
      var day = now.getDate();
      this.year = year;
      this.month = month;
      this.day = day;
      let curMonth=new Date(year, month, 0).getDate()
      this._initDate(curMonth);

    },
    methods: {
      changeFn(e){
        console.log(e.target.files[0])
        // let file=fileChoose.files[0],
        let file=e.target.files[0];
         let  reader=new FileReader();

        reader.onLoad=()=>{

          img.src=reader.result

        };

        reader.readAsDataURL(file)
      },
      nextMonth() {
        if (this.month == 12) {
          this.year = this.year + 1;
          this.month = 1;
        } else {
          this.month = this.month + 1
        }
        let curMonth=new Date(this.year, this.month, 0).getDate()
        this._initDate(curMonth);
      },
      preMonth() {
        if ((this.month) == 1) {
          this.year = this.year - 1;
          this.month = 12;
        } else {
          this.month = this.month - 1
        }
        let curMonth=new Date(this.year, this.month, 0).getDate()
        this._initDate(curMonth);
      },
      choose(index) {
        this.chooseId = index;
      },
      _initDate(args) {
        // getTime() 时间戳
        this.startDay = new Date(this.year, this.month - 1, 1).getDay(); //----------当前月第一天是周几
        let lastMonthDaysWei;
        lastMonthDaysWei = this.startDay;
        let lastMonthDaysCount = new Date(this.year, this.month - 1, 0).getDate(); //上个月的天数
        let lastMonthDaysArr = [];
        for (let i = lastMonthDaysCount - lastMonthDaysWei; i < lastMonthDaysCount; i++) {
          lastMonthDaysArr.push(i+1);
        }
        this.lastMonthDays = lastMonthDaysArr;
        //-----------------上月尾数
        let endWeekDay=new Date(this.year, this.month,0).getDay();
        this.endWeekDay=6-endWeekDay;
        //-----------本月最后一天是周几，周四的话下个月有3天在本月显示，下个月的天数
        let temp = [];
        for (let i = 0; i < args; i++) {
          let obj = {};
          obj.day = i + 1;
          obj.sign = 0
          for (let val of this.signDays) {
            if (val == i + 1) {
              obj.sign = 1;
            }
          }
          temp.push(obj)
        }
        this.monthDays = temp;
      },

    }
  }
</script>

<style scoped lang="less">
  .date {
    line-height: 1;
    .header {
      width: 6.5rem;
      padding: 0 .5rem;
      height: 1rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      /*background-color: #42b983;*/
      border-bottom: 1px solid #f5f5f5;
      background-color: #fff;
    }
    .container {
      background-color: #fff;
      width: 7rem;
      padding: .5rem .25rem;
      display: flex;
      flex-flow: row wrap;
      .item {
        height: .8rem;
        line-height: .8rem;
        text-align: center;
        width: 1rem;
        .day {
          width: .7rem;
          height: .7rem;
          line-height: .7rem;
          margin: .05rem auto;
        }
        .active {
          background-color: #3EA1F4;
          border-radius: 50%;
          color: #fff;
        }
        .choose-item {
          background-color: #30c082;
          border-radius: 50%;
          color: #fff;
        }
        .sign-item {
          background-color: #f00;
          border-radius: 50%;
          color: #fff;
        }
      }
      .gray {
        color: #999;
      }
    }
  }
</style>
