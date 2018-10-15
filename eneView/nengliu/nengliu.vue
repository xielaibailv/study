<template>
  <div style="height:100%">
    <div class="main-content">
      <div class="page-name">区域能流全景</div>
      <div class="video-year">
        <div class="year" v-bind:class="{ active: year == 2016 }" v-on:click="getEnergyFlow(2016)">2016</div>
        <div class="year year2" v-bind:class="{ active: year == 2017 }" v-on:click="getEnergyFlow(2017)">2017</div>
      </div>
      <div class="video">
        <video id="video1" class="video-container">
          <source src="./assets/video/1008.mp4" type="video/mp4">
        </video>
      </div>
    </div>
    <div class="bottom">
      <div class="section nengxiao">
        <div class="title">
          <div class="text">能效指标</div>
        </div>
        <div class="content">
          <div class="item">
            <div class="item-name" @click="showDialog()">单位GDP能耗量<em>（tce/万元）</em></div>
            <div class="num">
              <div class="main">{{energyFlowData.gdp}}</div>
              <div class="updown down">{{energyFlowData.gdpRate}}%</div>
              <div class="bi">同比</div>
            </div>
            <div class="bar">
              <div class="bar1" :style="`height: ${(energyFlowData.gdp/(energyFlowData.gdp>energyFlowData.gdplast?energyFlowData.gdp:energyFlowData.gdplast)) * 120}px;
                                        margin-top : ${(1-(energyFlowData.gdp/(energyFlowData.gdp>energyFlowData.gdplast?energyFlowData.gdp:energyFlowData.gdplast))) * 120}px;`"></div>
              <div class="bar2" :style="`height: ${(energyFlowData.gdplast/(energyFlowData.gdplast)) * 120}px;
                                        margin-top : ${(1-(energyFlowData.gdplast/(energyFlowData.gdp>energyFlowData.gdplast?energyFlowData.gdp:energyFlowData.gdplast))) * 120}px;`"></div>
            </div>
            <div class="text">
              <div class="biaogan">
                <div class="num">0.200</div>
                <span>标杆水平</span>
                <div class="sperate"></div>
              </div>
              <div class="text1"><em class="dot"></em>当年完成值</div>
              <div class="text2"><em class="dot"></em>上一年完成值<em class="num">{{energyFlowData.gdplast}}</em></div>
            </div>
          </div>

          <div class="item">
            <div class="item-name" @click="showDialog()">全年能耗总量<em>（万tce）</em></div>
            <div class="num">
              <div class="main">{{energyFlowData.energy}}</div>
              <div class="updown down">{{energyFlowData.energyRate}}%</div>
              <div class="bi">同比</div>
            </div>
            <div class="bar">
              <div class="bar1" :style="`height: ${(energyFlowData.energy/(energyFlowData.energy>energyFlowData.energylast?energyFlowData.energy:energyFlowData.energylast)) * 120}px;
                                        margin-top : ${(1-(energyFlowData.energy/(energyFlowData.energy>energyFlowData.energylast?energyFlowData.energy:energyFlowData.energylast))) * 120}px;`"></div>
              <div class="bar2" :style="`height: ${(energyFlowData.energylast/( energyFlowData.energylast)) * 120}px;
                                        margin-top : ${(1-(energyFlowData.energylast/(energyFlowData.energy>energyFlowData.energylast?energyFlowData.energy:energyFlowData.energylast))) * 120}px;`"></div>
            </div>
            <div class="text">
              <div class="biaogan">
                <div class="num">500</div>
                <span>标杆水平</span>
                <div class="sperate"></div>
              </div>
              <div class="text1"><em class="dot"></em>当年完成值</div>
              <div class="text2"><em class="dot"></em>上一年完成值<em class="num">{{energyFlowData.energylast}}</em></div>
            </div>
          </div>

          <div class="item">
            <div class="item-name" @click="showDialog()">全年碳排总量<em>（万tCO₂e）</em></div>
            <div class="num">
              <div class="main">{{energyFlowData.carbon}}</div>
              <div class="updown down">{{energyFlowData.carbonRate}}%</div>
              <div class="bi">同比</div>
            </div>
            <div class="bar">
              <div class="bar1" :style="`height: ${(energyFlowData.carbon/(energyFlowData.carbon>energyFlowData.carbonlast?energyFlowData.carbon:energyFlowData.carbonlast)) * 120}px;
                                        margin-top : ${(1-(energyFlowData.carbon/(energyFlowData.carbon>energyFlowData.carbonlast?energyFlowData.carbon:energyFlowData.carbonlast))) * 120}px;`"></div>
              <div class="bar2" :style="`height: ${(energyFlowData.carbonlast/( energyFlowData.carbonlast)) * 120}px;
                                        margin-top : ${(1-(energyFlowData.carbonlast/(energyFlowData.carbon>energyFlowData.carbonlast?energyFlowData.carbon:energyFlowData.carbonlast))) * 120}px;`"></div>
            </div>
            <div class="text">
              <div class="biaogan">
                <div class="num">6.5</div>
                <span>标杆水平</span>
                <div class="sperate"></div>
              </div>
              <div class="text1"><em class="dot"></em>当年完成值</div>
              <div class="text2"><em class="dot"></em>上一年完成值<em class="num">{{energyFlowData.carbonlast}}</em></div>
            </div>
          </div>

          <div class="item">
            <div class="item-name" @click="showDialog()">全年节能量<em>（万tce）</em></div>
            <div class="num">
              <div class="main">{{energyFlowData.energySave}}</div>
              <div class="updown down">{{energyFlowData.energySaveRate}}%</div>
              <div class="bi">同比</div>
            </div>
            <div class="bar">
              <div class="bar1" :style="`height: ${(energyFlowData.energySave/(energyFlowData.energySave>energyFlowData.energySave?energyFlowData.energySave:energyFlowData.energySave)) * 120}px;
                                        margin-top : ${(1-(energyFlowData.energySave/(energyFlowData.energySave>energyFlowData.energySave?energyFlowData.energySave:energyFlowData.energySave))) * 120}px;`"></div>
              <div class="bar2" :style="`height: ${(energyFlowData.energySavelast/(energyFlowData.energySave>energyFlowData.energySave?energyFlowData.energySave:energyFlowData.energySave)) * 120}px;
                                        margin-top : ${(1-(energyFlowData.energySavelast/(energyFlowData.energySave>energyFlowData.energySave?energyFlowData.energySave:energyFlowData.energySave))) * 120}px;`"></div>
            </div>
            <div class="text">
              <div class="biaogan">
                <div class="num">30</div>
                <span>标杆水平</span>
                <div class="sperate"></div>
              </div>
              <div class="text1"><em class="dot"></em>当年完成值</div>
              <div class="text2"><em class="dot"></em>上一年完成值<em class="num">{{energyFlowData.energySavelast}}</em></div>
            </div>
          </div>
        </div>
      </div>
      <div class="section nengyuan">
        <div class="title">
          <div class="text">能源消费结构<em>（按能源类型）</em></div>
          <div class="icons">
            <div class="pie" v-bind:class="{ active: pieList==1 }" v-on:click="pieList=1"></div>
            <div class="line"></div>
            <div class="list" v-bind:class="{ active: pieList==2 }" v-on:click="pieList=2"></div>
          </div>
        </div>
        <div class="content" id="nengyuan-chart" style="width: 450px;height: 300px;" v-bind:class="{ active: pieList==1 }" v-on:click="pieList=1"></div>
        <div class="content" id="nengyuan-line" v-bind:class="{ active: pieList==2 }" v-on:click="pieList=2">
          <div class="items">
            <div class="row">
              <div class="item">
                <div class="num1">{{energyFlowData.electric}}<em>MWh</em></div>
                <div class="num2">{{energyFlowData.electricTce}}<em>万tce</em></div>
                <div class="name">电</div>
              </div>
              <div class="item">
                <div class="num1">{{energyFlowData.naturalGas}}<em>亿Nm³</em></div>
                <div class="num2">{{energyFlowData.naturalGasTce}}<em>万tce</em></div>
                <div class="name">天然气</div>
              </div>
              <div class="item">
                <div class="num1">{{energyFlowData.coal}}<em>万吨</em></div>
                <div class="num2">{{energyFlowData.coalTce}}<em>万tce</em></div>
                <div class="name">煤炭及煤制品</div>
              </div>
            </div>
            <div class="row">
              <div class="item">
                <div class="num1">{{energyFlowData.gasoline}}<em>万吨</em></div>
                <div class="num2">{{energyFlowData.gasolineTce}}<em>万tce</em></div>
                <div class="name">汽油</div>
              </div>
              <div class="item">
                <div class="num1">{{energyFlowData.hot}}<em>万GJ</em></div>
                <div class="num2">{{energyFlowData.hotTce}}<em>万tce</em></div>
                <div class="name">热力</div>
              </div>
              <div class="item">
                <div class="num1">{{energyFlowData.oil}}<em>万吨</em></div>
                <div class="num2">{{energyFlowData.oilTce}}<em>万tce</em></div>
                <div class="name">柴油</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="_dialog_con flexDiv" @click="Dialog=false" v-show="Dialog">
      <div class="_dialog_con_img">
        <i class="iconfont icon-close _closeIcon" @click="Dialog=false"></i>
        <img src="./assets/img/dialogImg.png" v-on:click.stop>
      </div>
    </div>
  </div>
</template>

<script>
  import httpServer from "../../../untils/http.js";
  import $moment from 'moment'
  export default {
    name: "quanjing",
    data() {
      return {
        year: 2017,
        pieList: 1,
        energyFlowData : {},
        Dialog:false,
      }
    },
    created() {
    },
    mounted() {
      //自动播放
      var video1 = document.getElementById("video1");
      video1.loop = false;
      video1.autoplay = true;
      video1.muted = true;
      video1.load();

      let years = this.year
      this.getEnergyFlow(years);
      setInterval( () => {
          this.getEnergyFlow(years)
      }, 30000)
    },
    methods: {
      // 获取能流统计值
      getEnergyFlow(val) {
        let _that = this
        this.year = val;
        var dateTime = new Date;
        var _opts = {
          method: "post",
          url: "/suzhou_pro/show/energyFlow",
          year: val || dateTime.getFullYear()

        };
        httpServer(_opts).then(res => {
          if (res.code === '1') {
            this.energyFlowData = res.data;
            let typeTce = [
              {
                key: 'electricTce',
                value: '电',
                color: '#065981'
              },
              {
                key: 'coalTce',
                value: '煤炭及煤制品',
                color: '#1B6A78'
              },
              {
                key: 'gasolineTce',
                value: '汽油',
                color: '#CA9A28'
              },
              {
                key: 'naturalGasTce',
                value: '天然气',
                color: '#77C1D2'
              },
              {
                key: 'hotTce',
                value: '热力',
                color: '#AD642E'
              },
              {
                key: 'oilTce',
                value: '柴油',
                color: '#09878E'
              }
            ];
            let allTypeTce = 0
            let tceData = []
            typeTce.forEach(ele => {
              allTypeTce += res.data[ele.key]
            })
            typeTce.forEach(ele => {
              let tce = {
                value: 0,
                name: '',
                label: {fontSize: 14, fontFamily: "PingFangSC-Regular"},
                itemStyle: {color: "#CA9A28"}
              }
              tce.value = (res.data[ele.key] / allTypeTce * 100).toFixed(2);
              tce.name = ele.value;
              tce.itemStyle.color = ele.color;
              tceData.push(tce)
            })
            this.initNengyuanChart(tceData)
          }
        })
      },
      /**
       * 今日用电负荷
       */
      initNengyuanChart(data) {
        let jinRiYongDianChart = this.$echarts.init(document.getElementById('nengyuan-chart'));
        var option = {
          title: {
            x: 'center'
          },
          legend: {
            show: false
          },
          series: [
            {
              type: 'pie',
              radius: ['50%', '80%'],
              center: ['50%', '50%'],
              label: {
                normal: {
                  formatter: '{b|{b}}\n{per|{d}%}',
                  rich: {
                    b: {
                      color: 'rgba(170,178,200,1)',
                      fontSize: 14,
                      fontFamily: "PingFangSC-Regular"
                    },
                    per: {
                      color: 'rgba(170,178,200,1)',
                      fontSize: 14,
                      fontFamily: "PingFangSC-Regular"
                    }
                  }
                }
              },
              data: data
            }
          ]
        };
        // 使用刚指定的配置项和数据显示图表。
        jinRiYongDianChart.setOption(option);
      },

      showDialog(){
        this.Dialog = true
      }
    }
  }
</script>

<style scoped>
  @import '../../../assets/css/public.css';
  @import 'assets/css/nengliu.css';
  ._dialog_con{
    position: fixed;
    left:0;right:0;
    top:0;
    bottom:0;
    /*background: rgba(0,0,0, .8);*/
    z-index: 999999;
  }
  ._dialog_con_img{width: 80%;position: relative;}
  ._dialog_con img { width: 100%;}

  ._closeIcon.iconfont{position: absolute;right: 20px; top:20px;font-size: 26px; cursor:pointer;}
</style>
