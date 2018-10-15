<template>
  <div v-on:click="bodyClicked($event);" v-on:mouseover="mouseMoved($event)" style="height:100%;overflow-y: auto; overflow-x: hidden;position:relative">
<!--    <div class="bg dian220"></div>
    <div class="bg dian500"></div>
    <div class="bg lengguan"></div>
    <div class="bg reguan"></div>
    <div class="bg dianzhan"></div>
    -->
    <img class="bg lengguan-gif" v-bind:src="lengguanSrc" v-bind:style="lengguanStyle"/>
    <img class="bg reguan-gif" v-bind:src="reguanSrc" v-bind:style="reguanStyle"/>
    <img class="bg dianwang-gif" v-bind:src="dianwangSrc" v-bind:style="dianwangStyle"/>
<!--    <div class="bg lengguan-gif" v-bind:class="{ open: typeGonglengOpen }"></div>
    <div class="bg reguan-gif" v-bind:class="{ open: typeGongreOpen }"></div>
    <div class="bg dianwang-gif" v-bind:class="{ open: typeDianwangOpen }"></div>-->
    <div class="ceshi">
      <div class="main-content">
        <div class="page-name">多能全景监控</div>
        <div class="page-name-dropdown" v-bind:class="{ open: typeChooseOpen }" v-on:click="typeChooseOpen=!typeChooseOpen"></div>
        <div class="type-choose" v-bind:class="{ open: typeChooseOpen }">
          <div class="type-content">
            <div class="type-item">
              <div class="type-name">源</div>
              <div class="sub-types">
                <div class="sub-type" id="ranqiBtn" v-bind:class="{ active: typeRanqiOpen }" v-on:click="typeRanqiOpen=!typeRanqiOpen,typeSelected('ranqidianzhan')">燃气电站
                </div>
                <div class="sub-type" id="guangfuBtn" v-bind:class="{ active: typeGuangfuOpen }" v-on:click="typeGuangfuOpen=!typeGuangfuOpen,typeSelected('guangfu')">光伏
                </div>
              </div>
            </div>
            <div class="type-item">
              <div class="type-name">网</div>
              <div class="sub-types">
                <div class="sub-type" v-bind:class="{ active: typeDianwangOpen }" v-on:click="typeDianwangOpen=!typeDianwangOpen,typeSelected('dianwang')">电网
                </div>
                <div class="sub-type" v-bind:class="{ active: typeGongreOpen }" v-on:click="typeGongreOpen=!typeGongreOpen,typeSelected('gongre')">供热网
                </div>
                <div class="sub-type" v-bind:class="{ active: typeGonglengOpen }" v-on:click="typeGonglengOpen=!typeGonglengOpen,typeSelected('gongleng')">供冷网
                </div>
              </div>
            </div>
            <div class="type-item">
              <div class="type-name">储</div>
              <div class="sub-types">
                <div class="sub-type" id="chunengBtn" v-bind:class="{ active: typeChunengOpen }" v-on:click="typeChunengOpen=!typeChunengOpen,typeSelected('chuneng')">储能
                </div>
              </div>
            </div>
            <div class="type-item">
              <div class="type-name">荷</div>
              <div class="sub-types">
                <div class="sub-type" id="qiyeBtn" v-bind:class="{ active: typeQiyeOpen }" v-on:click="typeQiyeOpen=!typeQiyeOpen,typeSelected('qiye')">企业
                </div>
                <div class="sub-type" id="chongdianzhanBtn" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:click="typeChongdianzhanOpen=!typeChongdianzhanOpen,typeSelected('chongdianzhan')">充电站
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="qiyenenghaopaiming" v-bind:class="{ open: bottomOpen }" v-on:click="qiyenenghaoOpen=!qiyenenghaoOpen,getBottomData(1)">企业能耗排名</div>

        <div class="bottom " v-bind:class="{ open: bottomOpen }" v-on:click="bottomOpen=!bottomOpen">
          <div class="head">
            <div class="item jinri">总量控制<em>(当年累计/年度计划)</em></div>
            <div class="item jiegou">结构优化<em>(当年累计/年度目标)</em></div>
            <div class="item anquan">安全保障<em>(当年累计/年度目标)</em></div>
            <div class="item jieneng">节能环保<em>(当年累计/年度目标)</em></div>
            <div class="item jieru">接入规模<em>(接入数/园区总数)</em></div>
          </div>
          <div class="content">
            <div class="head">
              <div class="item jinri">总量控制<em>(当年累计/年度计划)</em></div>
              <div class="item jiegou">结构优化<em>(当年累计/年度目标)</em></div>
              <div class="item anquan">安全保障<em>(当年累计/年度目标)</em></div>
              <div class="item jieneng">节能环保<em>(当年累计/年度目标)</em></div>
              <div class="item jieru">接入规模<em>(接入数/园区总数)</em></div>
            </div>
            <div class="data-items">
              <div class="data-item jinri">
                <div class="row">
                  <div class="cell">
                    <div class="num">230<em>万tce&nbsp;&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;</em>550<em>万tce</em></div>
                    <div class="name">全社会能源消费总量</div>
                  </div>
                  <div class="cell">
                    <div class="num">100<em>亿kWh&nbsp;&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;</em>120<em>亿kWh</em></div>
                    <div class="name">全社会用电量</div>
                  </div>
                </div>
                <div class="row">
                  <div class="cell _100">
                    <div class="num">13686<em>万m³&nbsp;&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;</em>16000<em>万m³</em></div>
                    <div class="name">全社会用水量</div>
                  </div>
                </div>
              </div>
              <div class="data-item jiegou">
                <div class="row">
                  <div class="cell _100">
                    <div class="num">21<em>%&nbsp;&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;</em>25<em>%</em></div>
                    <div class="name">天然气占一次能源消费比重</div>
                  </div>
                </div>
                <div class="row">
                  <div class="cell _100">
                    <div class="num">94.1<em>%&nbsp;&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;</em>95<em>%</em></div>
                    <div class="name">本地清洁能源装机比重</div>
                  </div>
                </div>
              </div>
              <div class="data-item anquan">
                <div class="row">
                  <div class="cell _100">
                    <div class="num">99.7<em>%&nbsp;&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;</em>99.96<em>%</em></div>
                    <div class="name">中心城区及重点区域供电可靠性</div>
                  </div>
                </div>
              </div>
              <div class="data-item jieneng">
                <div class="row">
                  <div class="cell mid">
                    <div class="num">4<em>%&nbsp;&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;</em>4<em>%</em></div>
                    <div class="name big">天然气产销差率</div>
                  </div>
                </div>
              </div>
              <div class="data-item jieru">
                <div class="row">
                  <div class="cell small">
                    <div class="num">2<em>/2座</em></div>
                    <div class="name">燃气电站</div>
                  </div>
                  <div class="cell small">
                    <div class="num">1<em>/64座</em></div>
                    <div class="name">分布式光伏</div>
                  </div>
                  <div class="cell small">
                    <div class="num">1<em>/2座</em></div>
                    <div class="name">分布式储能</div>
                  </div>
                </div>
                <div class="row">
                  <div class="cell small">
                    <div class="num">1<em>/1座</em></div>
                    <div class="name">水厂</div>
                  </div>
                  <div class="cell small">
                    <div class="num">51<em>/3263家</em></div>
                    <div class="name">用能企业</div>
                  </div>
                  <div class="cell small">
                    <div class="num">10<em>/109个</em></div>
                    <div class="name">充电站</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="qiyenenghaopaiming-modal" v-bind:class="{ open: qiyenenghaoOpen }">
          <div class="title">
            <span class="name">企业综合用能排名</span>
            <span class="dropdown" v-bind:class="{ open: qiyenenghaoDropdownOpen }" v-on:click="qiyenenghaoDropdownOpen=!qiyenenghaoDropdownOpen"><span class="shaixuanTitle">{{shaixuanTitle}}</span><i></i></span>
            <span class="icon-1"></span>
            <span class="icon-2"></span>
            <span class="icon-3"></span>
            <span class="name2">园区节能潜力（已落实节能项目/总体潜力）：<em>{{energyRanking.plan}}tce/{{energyRanking.max}}tce</em></span>
            <span class="close" v-on:click="qiyenenghaoOpen=false,qiyenenghaoDropdownOpen=false"></span>
          </div>
          <div class="content">
            <div class="row">
              <div class="item" v-for="(comp, indexComp) in energyRanking.showingdata.slice(0,5)" :key="indexComp">
                <span class="name">
                  <em>{{comp.index}}.</em>{{ comp.name }}
                </span>
                <div class="num">
                  <span class="no"><em></em>{{ comp.energy }}tce</span>
                  <span class="perct"><em></em>同比：下降{{ comp.rate }}%</span>
                  <span class="no2"><em></em>{{ comp.plan }}tce</span>
                </div>
                <div class="bar-bg"></div>
                <div class="bar-data" v-bind:data-perct="comp.perct"></div>
                <router-link class="icon-4" v-bind:to="comp.downloadFile1" target="_blank" v-if="comp.downloadFile1"></router-link>
                <router-link class="icon-4" v-bind:to="comp.downloadFile2" target="_blank" v-if="comp.downloadFile2"></router-link>
              </div>
            </div>
            <div class="row">
              <div class="item" v-for="(comp, indexComp) in energyRanking.showingdata.slice(5,10)" :key="indexComp">
                <span class="name">
                  <em>{{comp.index}}.</em>{{ comp.name }}
                </span>
                <div class="num">
                  <span class="no"><em></em>{{ comp.energy }}tce</span>
                  <span class="perct"><em></em>同比：下降{{ comp.rate }}%</span>
                  <span class="no2"><em></em>{{ comp.plan }}tce</span>
                </div>
                <div class="bar-bg"></div>
                <div class="bar-data" v-bind:data-perct="comp.perct"></div>
                <router-link class="icon-4" v-bind:to="comp.downloadFile1" target="_blank" v-if="comp.downloadFile1"></router-link>
                <router-link class="icon-4" v-bind:to="comp.downloadFile2" target="_blank" v-if="comp.downloadFile2"></router-link>
              </div>
            </div>
            <div class="row">
              <div class="item" v-for="(comp, indexComp) in energyRanking.showingdata.slice(10,15)" :key="indexComp">
                <span class="name">
                  <em>{{comp.index}}.</em>{{ comp.name }}
                </span>
                <div class="num">
                  <span class="no"><em></em>{{ comp.energy }}tce</span>
                  <span class="perct"><em></em>同比：下降{{ comp.rate }}%</span>
                  <span class="no2"><em></em>{{ comp.plan }}tce</span>
                </div>
                <div class="bar-bg"></div>
                <div class="bar-data" v-bind:data-perct="comp.perct"></div>
                <router-link class="icon-4" v-bind:to="comp.downloadFile1" target="_blank" v-if="comp.downloadFile1"></router-link>
                <router-link class="icon-4" v-bind:to="comp.downloadFile2" target="_blank" v-if="comp.downloadFile2"></router-link>
              </div>
            </div>
          </div>
          <div class="indicate">
            <div class="num">
              <span class="no"><em></em>企业能耗</span>
              <span class="perct"><em></em>企业能耗同比</span>
              <span class="no2"><em></em>企业节能潜力</span>
            </div>
          </div>
          <div class="paging" v-if="energyRanking.totalPages>1">
            <span class="left" v-on:click="prevPage()"></span>
            <span class="page"
                  v-for="(pageNum, index) in energyRanking.currentPageNums"
                  :key="index"
                  v-on:click="changePage(pageNum)"
                  v-bind:class="{active:pageNum==energyRanking.currentPage}">{{pageNum}}</span>
            <span class="right" v-on:click="nextPage()"></span>
          </div>
        </div>

        <div class="hangyeshaixuan-popup" v-bind:class="{ open: qiyenenghaoDropdownOpen&&qiyenenghaoOpen }">
          <ul>
            <li v-bind:class="{ active: energyRanking.industry==0}" v-on:click="changeIndustry(0),shaixuanTitle='行业筛选'">全部</li>
            <li v-bind:class="{ active: energyRanking.industry==1}" v-on:click="changeIndustry(1),shaixuanTitle='制造业'">制造业</li>
            <li v-bind:class="{ active: energyRanking.industry==2}" v-on:click="changeIndustry(2),shaixuanTitle='电力、燃气及水的生产和供应业'">电力、燃气及水的生产和供应业</li>
            <li v-bind:class="{ active: energyRanking.industry==3}" v-on:click="changeIndustry(3),shaixuanTitle='批发和零售业'">批发和零售业</li>
            <li v-bind:class="{ active: energyRanking.industry==4}" v-on:click="changeIndustry(4),shaixuanTitle='信息传输、计算机服务和软件业'">信息传输、计算机服务和软件业</li>
            <li v-bind:class="{ active: energyRanking.industry==5}" v-on:click="changeIndustry(5),shaixuanTitle='住宿和餐饮业'">住宿和餐饮业</li>
            <li v-bind:class="{ active: energyRanking.industry==6}" v-on:click="changeIndustry(6),shaixuanTitle='科学研究、技术服务和地质勘查业'">科学研究、技术服务和地质勘查业</li>
            <li v-bind:class="{ active: energyRanking.industry==7}" v-on:click="changeIndustry(7),shaixuanTitle='租赁和商务服务业'">租赁和商务服务业</li>
            <li v-bind:class="{ active: energyRanking.industry==8}" v-on:click="changeIndustry(8),shaixuanTitle='金融业'">金融业</li>
            <li v-bind:class="{ active: energyRanking.industry==9}" v-on:click="changeIndustry(9),shaixuanTitle='建筑业'">建筑业</li>
            <li v-bind:class="{ active: energyRanking.industry==10}" v-on:click="changeIndustry(10),shaixuanTitle='房地产业'">房地产业</li>
            <li v-bind:class="{ active: energyRanking.industry==11}" v-on:click="changeIndustry(11),shaixuanTitle='教育'">教育</li>
            <li v-bind:class="{ active: energyRanking.industry==12}" v-on:click="changeIndustry(12),shaixuanTitle='文化、体育和娱乐业'">文化、体育和娱乐业</li>
            <li v-bind:class="{ active: energyRanking.industry==13}" v-on:click="changeIndustry(13),shaixuanTitle='交通运输、仓储和邮政业'">交通运输、仓储和邮政业</li>
            <li v-bind:class="{ active: energyRanking.industry==14}" v-on:click="changeIndustry(14),shaixuanTitle='公共管理和社会组织'">公共管理和社会组织</li>
            <li v-bind:class="{ active: energyRanking.industry==15}" v-on:click="changeIndustry(15),shaixuanTitle='卫生、社会保障和社会福利业'">卫生、社会保障和社会福利业</li>
            <li v-bind:class="{ active: energyRanking.industry==16}" v-on:click="changeIndustry(16),shaixuanTitle='居民服务和其他服务业'">居民服务和其他服务业</li>
            <li v-bind:class="{ active: energyRanking.industry==17}" v-on:click="changeIndustry(17),shaixuanTitle='其他'">其他</li>
          </ul>
        </div>

        <div class="modal qiye" v-bind:class="{ open: typeQiyeOpen&&typeQiyeSelected }">
          <div class="dot"></div>
          <div class="title">{{ qiyeData.name }}</div>
          <span class="close" v-on:click="typeQiyeSelected=false"></span>
          <div class="content">
            <div class="items">
              <div class="row">
                <div class="tab">
                  <div class="tab-item active tab-item1" v-on:click="tabItemClicked($event,1)">电</div>
                  <div class="tab-item tab-item2" v-on:click="tabItemClicked($event,2)">热</div>
                  <div class="tab-item tab-item3" v-on:click="tabItemClicked($event,3)">气</div>
                  <div class="tab-item tab-item4" v-on:click="tabItemClicked($event,4)">水</div>
                </div>
              </div>
              <div class="row tab-content tab-content1">
                <div class="item">
                  <div class="num">{{ qiyeData.capacity }}<em>kVA</em></div>
                  <div class="name">容量</div>
                </div>
                <div class="item">
                  <div class="num">{{ qiyeData.usePowerSum }}<em>kWh</em></div>
                  <div class="name">本月累计用电量</div>
                </div>
              </div>
              <div class="row tab-content tab-content1">
                <div class="item">
                  <div class="sub-title">最近30天日用电量曲线</div>
                </div>
              </div>
              <div class="row tab-content tab-content2 hide">
                <div class="item">
                  <div class="num">{{ qiyeData.capacity }}<em>kVA</em></div>
                  <div class="name">本月耗热（MJ）量</div>
                </div>
              </div>
              <div class="row tab-content tab-content2 hide">
                <div class="item">
                  <div class="sub-title">最近三十天耗热量</div>
                </div>
              </div>
              <div class="row tab-content tab-content3 hide">
                <div class="item">
                  <div class="num">{{ qiyeData.capacity }}<em>kVA</em></div>
                  <div class="name">本月耗气（立方米）量</div>
                </div>
              </div>
              <div class="row tab-content tab-content3 hide">
                <div class="item">
                  <div class="sub-title">最近三十天耗气量</div>
                </div>
              </div>
              <div class="row tab-content tab-content4 hide">
                <div class="item">
                  <div class="num">{{ qiyeData.capacity }}<em>kVA</em></div>
                  <div class="name">本月耗水（立方米）量</div>
                </div>
              </div>
              <div class="row tab-content tab-content4 hide">
                <div class="item">
                  <div class="sub-title">最近三十天耗水量</div>
                </div>
              </div>
              <div class="row tab-content tab-content1">
                <div class="chart" id="chart-qiye"></div>
              </div>
              <div class="row tab-content tab-content2 tab-content3 tab-content4 hide">
                <div class="chart" id="chart-qiye2"></div>
              </div>
            </div>
          </div>
        </div>

        <div class="modal chuneng" v-bind:class="{ open: typeChunengOpen&&typeChunengSelected}">
          <div class="dot"></div>
          <div class="title">{{ chunengData.name }}</div>
          <span class="close" v-on:click="typeChunengSelected=false"></span>
          <div class="content">
            <div class="items">
              <div class="row">
                <div class="item">
                  <div class="num">{{ chunengData.capacity }}<em>kWh</em></div>
                  <div class="name">电池容量</div>
                </div>
                <div class="item">
                  <div class="num">{{ chunengData.batteryType }}</div>
                  <div class="name">运行策略</div>
                </div>
              </div>
              <div class="row">
                <div class="item">
                  <div class="num">{{ chunengData.jinriChong }}<em>kWh</em></div>
                  <div class="name">今日充电电量</div>
                </div>
                <div class="item">
                  <div class="num">{{ chunengData.jinriFang }}<em>kWh</em></div>
                  <div class="name">今日放电电量</div>
                </div>
              </div>
              <div class="row">
                <div class="item">
                  <div class="num">{{ chunengData.chargeSum }}<em>kWh</em></div>
                  <div class="name">累计充电电量</div>
                </div>
                <div class="item">
                  <div class="num">{{ chunengData.dischargeSum }}<em>kWh</em></div>
                  <div class="name">累计放电电量</div>
                </div>
              </div>
              <div class="row">
                <div class="item big">
                  <div class="sub-title">今日储能功率曲线</div>
                </div>
              </div>
              <div class="row">
                <div class="chart" id="chart-chuneng"></div>
              </div>
            </div>
          </div>
        </div>

        <div class="modal chongdian" v-bind:class="{ open: typeChongdianzhanOpen&&typeChongdianzhanSelected }">
          <div class="dot"></div>
          <div class="title">{{ chongdianzhanData.name }}</div>
          <span class="close" v-on:click="typeChongdianzhanSelected=false"></span>
          <div class="content">
            <div class="items">
              <div class="row">
                <div class="item">
                  <div class="num">{{ chongdianzhanData.quickCount }}<em>个</em></div>
                  <div class="name">充电桩数量</div>
                </div>
                <div class="item">
                  <div class="num">{{ chongdianzhanData.quickPower }}<em>kW</em></div>
                  <div class="name">额定总功率</div>
                </div>
              </div>
              <div class="row chongdianzhaung-row">
                <div class="chongdianzhaung" v-for="(count,index) in parseInt(chongdianzhanData.quickCount)" :key="index"></div>
              </div>
            </div>
          </div>
        </div>

        <div class="modal guangfu" v-bind:class="{ open: typeGuangfuOpen&&typeGuangfuSelected }">
          <div class="dot"></div>
          <div class="title">{{ guangfuData.name }}</div>
          <span class="close" v-on:click="typeGuangfuSelected=false"></span>
          <div class="content">
            <div class="items">
              <div class="row">
                <div class="item">
                  <div class="num">{{ guangfuData.capacity }}<em>kWp</em></div>
                  <div class="name">容量</div>
                </div>
                <div class="item">
                  <div class="num">{{ guangfuData.startRunDate }}</div>
                  <div class="name">投运日期</div>
                </div>
              </div>
              <div class="row">
                <div class="item">
                  <div class="num">{{ guangfuData.jinri}}<em>kWh</em></div>
                  <div class="name">今日发电量</div>
                </div>
                <div class="item">
                  <div class="num">{{ guangfuData.leiji}}<em>kWh</em></div>
                  <div class="name">累计发电量</div>
                </div>
              </div>
              <div class="row">
                <div class="item">
                  <div class="sub-title">今日发电曲线</div>
                </div>
              </div>
              <div class="row">
                <div class="chart" id="chart-guangfu"></div>
              </div>
            </div>
          </div>
        </div>

        <div class="modal randiqianzhan" v-bind:class="{ open: typeRanqiOpen&&typeRanqiSelected }">
          <div class="dot"></div>
          <div class="title">{{ randianData.name }}</div>
          <span class="close" v-on:click="typeRanqiSelected=false"></span>
          <div class="content">
            <div class="items">
              <div class="row">
                <div class="item">
                  <div class="num">{{ randianData.capacity }}<em>MW</em></div>
                  <div class="name">容量</div>
                </div>
                <div class="item">
                  <div class="num">{{ randianData.startRunDate }}<em>年</em></div>
                  <div class="name">投运年份</div>
                </div>
              </div>
              <div class="row">
                <div class="item">
                  <div class="num">{{ randianData.providePowerSum }}<em>kWh</em></div>
                  <div class="name">上月累计发电量</div>
                </div>
                <div class="item">
                  <div class="num">{{ randianData.provideHotSum }}<em>百万千焦</em></div>
                  <div class="name">上月累计供热量</div>
                </div>
              </div>
              <div class="row">
                <div class="item">
                  <div class="num">&nbsp;</div>
                  <div class="name">&nbsp;</div>
                </div>
              </div>
              <div class="row">
                <div class="item big">
                  <div class="sub-title">今年各月的发电曲线/今年各月的供热量曲线</div>
                </div>
              </div>
              <div class="row">
                <div class="chart" id="chart-randiqianzhan"></div>
              </div>
            </div>
          </div>
        </div>

        <div class="points">
          <div class="ranqidianzhan ranqidianzhan1" v-bind:class="{ active: typeRanqiOpen }" v-on:mouseover="showName($event, 'ranqidianzhan', 'DWRD')" v-on:click="pointClicked('ranqidianzhan', 'DWRD')"></div>
          <div class="ranqidianzhan ranqidianzhan2" v-bind:class="{ active: typeRanqiOpen }" v-on:mouseover="showName($event, 'ranqidianzhan', 'LTRD')" v-on:click="pointClicked('ranqidianzhan', 'LTRD')"></div>
          <div class="guangfu guangfu1" v-bind:class="{ active: typeGuangfuOpen }" v-on:mouseover="showName($event, 'guangfu', 'site_00000485')" v-on:click="pointClicked('guangfu', 'site_00000485')"></div>
          <div class="chuneng chuneng1" v-bind:class="{ active: typeChunengOpen }" v-on:mouseover="showName($event, 'chuneng', 'site_00000501')" v-on:click="pointClicked('chuneng', 'site_00000501')"></div>
          <div class="chongdianzhan chongdianzhan1" v-bind:class="{ active: typeChongdianzhanOpen }"></div>
          <div class="chongdianzhan chongdianzhan2" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:mouseover="showName($event, 'chongdianzhan', '1046')" v-on:click="pointClicked('chongdianzhan', '1046')"></div>
          <div class="chongdianzhan chongdianzhan3" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:mouseover="showName($event, 'chongdianzhan', '176')" v-on:click="pointClicked('chongdianzhan', '176')"></div>
          <div class="chongdianzhan chongdianzhan4" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:mouseover="showName($event, 'chongdianzhan', '3312')" v-on:click="pointClicked('chongdianzhan', '3312')"></div>
          <div class="chongdianzhan chongdianzhan5" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:mouseover="showName($event, 'chongdianzhan', 'SZYS-LLLL-0512-0012')" v-on:click="pointClicked('chongdianzhan', 'SZYS-LLLL-0512-0012')"></div>
          <div class="chongdianzhan chongdianzhan6" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:mouseover="showName($event, 'chongdianzhan', '3205060002')" v-on:click="pointClicked('chongdianzhan', '3205060002')"></div>
          <div class="chongdianzhan chongdianzhan7" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:mouseover="showName($event, 'chongdianzhan', '3205060061')" v-on:click="pointClicked('chongdianzhan', '3205060061')"></div>
          <div class="chongdianzhan chongdianzhan8" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:mouseover="showName($event, 'chongdianzhan', '202')" v-on:click="pointClicked('chongdianzhan', '202')"></div>
          <div class="chongdianzhan chongdianzhan9" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:mouseover="showName($event, 'chongdianzhan', 'SZYS-SZHH-0512-0001')" v-on:click="pointClicked('chongdianzhan', 'SZYS-SZHH-0512-0001')"></div>
          <div class="chongdianzhan chongdianzhan10" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:mouseover="showName($event, 'chongdianzhan', 'SZYS-LLZX-0512-0004')" v-on:click="pointClicked('chongdianzhan', 'SZYS-LLZX-0512-0004')"></div>
          <div class="chongdianzhan chongdianzhan11" v-bind:class="{ active: typeChongdianzhanOpen }" v-on:mouseover="showName($event, 'chongdianzhan', '11961')" v-on:click="pointClicked('chongdianzhan', '11961')"></div>
          <div class="qiye qiye1" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'GBDS')" v-on:click="pointClicked('qiye', 'GBDS')"></div>
          <div class="qiye qiye2" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'QNZY')" v-on:click="pointClicked('qiye', 'QNZY')"></div>
          <div class="qiye qiye3" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'RYX')" v-on:click="pointClicked('qiye', 'RYX')"></div>
          <div class="qiye qiye4" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'LFGC')" v-on:click="pointClicked('qiye', 'LFGC')"></div>
          <div class="qiye qiye5" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'LDKJ')" v-on:click="pointClicked('qiye', 'LDKJ')"></div>
          <div class="qiye qiye6" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'LLZX')" v-on:click="pointClicked('qiye', 'LLZX')"></div>
          <div class="qiye qiye7" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'KDZY')" v-on:click="pointClicked('qiye', 'KDZY')"></div>
          <div class="qiye qiye8" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'TFXS')" v-on:click="pointClicked('qiye', 'TFXS')"></div>
          <div class="qiye qiye9" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'JJH')" v-on:click="pointClicked('qiye', 'JJH')"></div>
          <div class="qiye qiye10" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'RSBDT')" v-on:click="pointClicked('qiye', 'RSBDT')"></div>
          <div class="qiye qiye11" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'AMSHJ')" v-on:click="pointClicked('qiye', 'AMSHJ')"></div>
          <div class="qiye qiye12" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'HJKJ')" v-on:click="pointClicked('qiye', 'HJKJ')"></div>
          <div class="qiye qiye13" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'SXDZ')" v-on:click="pointClicked('qiye', 'SXDZ')"></div>
          <div class="qiye qiye14" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'SXYJ')" v-on:click="pointClicked('qiye', 'SXYJ')"></div>
          <div class="qiye qiye15" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'XXZ')" v-on:click="pointClicked('qiye', 'XXZ')"></div>
          <div class="qiye qiye16" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'XPKJ')" v-on:click="pointClicked('qiye', 'XPKJ')"></div>
          <div class="qiye qiye17" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'BSGGT')" v-on:click="pointClicked('qiye', 'BSGGT')"></div>
          <div class="qiye qiye18" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'XNJG')" v-on:click="pointClicked('qiye', 'XNJG')"></div>
          <div class="qiye qiye19" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'HFYZY')" v-on:click="pointClicked('qiye', 'HFYZY')"></div>
          <div class="qiye qiye20" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'QCKJ')" v-on:click="pointClicked('qiye', 'QCKJ')"></div>
          <div class="qiye qiye21" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'BXOQT')" v-on:click="pointClicked('qiye', 'BXOQT')"></div>
          <div class="qiye qiye22" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'SPJM')" v-on:click="pointClicked('qiye', 'SPJM')"></div>
          <div class="qiye qiye23" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'DJJD')" v-on:click="pointClicked('qiye', 'DJJD')"></div>
          <div class="qiye qiye24" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'BSQC')" v-on:click="pointClicked('qiye', 'BSQC')"></div>
          <div class="qiye qiye25" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'HSYY')" v-on:click="pointClicked('qiye', 'HSYY')"></div>
          <div class="qiye qiye26" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'PJWFB')" v-on:click="pointClicked('qiye', 'PJWFB')"></div>
          <div class="qiye qiye27" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'JLKJ')" v-on:click="pointClicked('qiye', 'JLKJ')"></div>
          <div class="qiye qiye28" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'MKWE')" v-on:click="pointClicked('qiye', 'MKWE')"></div>
          <div class="qiye qiye29" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'YCSP')" v-on:click="pointClicked('qiye', 'YCSP')"></div>
          <div class="qiye qiye30" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'QSQC')" v-on:click="pointClicked('qiye', 'QSQC')"></div>
          <div class="qiye qiye31" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'TKDZ')" v-on:click="pointClicked('qiye', 'TKDZ')"></div>
          <div class="qiye qiye32" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'JPTGS')" v-on:click="pointClicked('qiye', 'JPTGS')"></div>
          <div class="qiye qiye33" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'ZXDZ')" v-on:click="pointClicked('qiye', 'ZXDZ')"></div>
          <div class="qiye qiye34" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'QDWY')" v-on:click="pointClicked('qiye', 'QDWY')"></div>
          <div class="qiye qiye35" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'DYJM')" v-on:click="pointClicked('qiye', 'DYJM')"></div>
          <div class="qiye qiye36" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'WTJP')" v-on:click="pointClicked('qiye', 'WTJP')"></div>
          <div class="qiye qiye37" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'WTCY')" v-on:click="pointClicked('qiye', 'WTCY')"></div>
          <div class="qiye qiye38" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'ULMH')" v-on:click="pointClicked('qiye', 'ULMH')"></div>
          <div class="qiye qiye39" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'THCJ')" v-on:click="pointClicked('qiye', 'THCJ')"></div>
          <div class="qiye qiye40" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'GKZH')" v-on:click="pointClicked('qiye', 'GKZH')"></div>
          <div class="qiye qiye41" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'ZGFS')" v-on:click="pointClicked('qiye', 'ZGFS')"></div>
          <div class="qiye qiye42" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'WBZY')" v-on:click="pointClicked('qiye', 'WBZY')"></div>
          <div class="qiye qiye43" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'XDSW')" v-on:click="pointClicked('qiye', 'XDSW')"></div>
          <div class="qiye qiye44" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'NMCY')" v-on:click="pointClicked('qiye', 'NMCY')"></div>
          <div class="qiye qiye45" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'YRZC')" v-on:click="pointClicked('qiye', 'YRZC')"></div>
          <div class="qiye qiye46" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'YDFU')" v-on:click="pointClicked('qiye', 'YDFU')"></div>
          <div class="qiye qiye47" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'XXGY')" v-on:click="pointClicked('qiye', 'XXGY')"></div>
          <div class="qiye qiye48" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'ZHSJ')" v-on:click="pointClicked('qiye', 'ZHSJ')"></div>
          <div class="qiye qiye49" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'BSDKJ')" v-on:click="pointClicked('qiye', 'BSDKJ')"></div>
          <div class="qiye qiye50" v-bind:class="{ active: typeQiyeOpen }" v-on:mouseover="showName($event, 'qiye', 'SZDS')" v-on:click="pointClicked('qiye', 'SZDS')"></div>
        </div>

        <div class="north"></div>

        <div class="modal qiye2" v-bind:class="{ open: typePointNameTip }">
          <div class="dot"></div>
          <div class="title">{{ qiyeData.name }}</div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
  import httpServer from "../../../untils/http.js";

  export default {
    name: "quanjing",
    data() {
      return {
        lengguanSrcList: [
          "/static/img/quanjing/lengguan/lengguan-1920-1080_0.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_1.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_2.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_3.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_4.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_5.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_6.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_7.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_8.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_9.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_10.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_11.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_12.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_13.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_14.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_15.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_16.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_17.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_18.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_19.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_20.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_21.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_22.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_23.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_24.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_25.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_26.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_27.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_28.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_29.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_30.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_31.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_32.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_33.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_34.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_35.png",
          "/static/img/quanjing/lengguan/lengguan-1920-1080_36.png"
        ],
        reguanSrcList: [
          "/static/img/quanjing/reguan/reguan-1920-1080_0.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_1.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_2.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_3.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_4.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_5.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_6.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_7.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_8.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_9.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_10.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_11.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_12.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_13.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_14.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_15.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_16.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_17.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_18.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_19.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_20.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_21.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_22.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_23.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_24.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_25.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_26.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_27.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_28.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_29.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_30.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_31.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_32.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_33.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_34.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_35.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_36.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_37.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_38.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_39.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_40.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_41.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_42.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_43.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_44.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_45.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_46.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_47.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_48.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_49.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_50.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_51.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_52.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_53.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_54.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_55.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_56.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_57.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_58.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_59.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_60.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_61.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_62.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_63.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_64.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_65.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_66.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_67.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_68.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_69.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_70.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_71.png",
          "/static/img/quanjing/reguan/reguan-1920-1080_72.png",
        ],
        dianwangSrcList: [
          "/static/img/quanjing/dianwang/dianwang_1920-1080_0.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_1.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_2.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_3.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_4.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_5.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_6.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_7.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_8.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_9.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_10.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_11.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_12.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_13.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_14.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_15.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_16.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_17.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_18.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_19.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_20.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_21.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_22.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_23.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_24.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_25.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_26.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_27.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_28.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_29.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_30.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_31.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_32.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_33.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_34.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_35.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_36.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_37.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_38.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_39.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_40.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_41.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_42.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_43.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_44.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_45.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_46.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_47.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_48.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_49.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_50.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_51.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_52.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_53.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_54.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_55.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_56.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_57.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_58.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_59.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_60.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_61.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_62.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_63.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_64.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_65.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_66.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_67.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_68.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_69.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_70.png",
          "/static/img/quanjing/dianwang/dianwang_1920-1080_71.png",
        ],
        lengguanSrc: "/static/img/quanjing/lengguan/lengguan-1920-1080_0.png",
        reguanSrc: "/static/img/quanjing/reguan/reguan-1920-1080_0.png",
        dianwangSrc: "/static/img/quanjing/dianwang/dianwang_1920-1080_0.png",
        lengguanStyle: "display:block",
        reguanStyle: "display:block",
        dianwangStyle: "display:block",
        typeChooseOpen: true,
        typeRanqiOpen: true,
        typeGuangfuOpen: true,
        typeDianwangOpen: true,
        typeGongreOpen: true,
        typeGonglengOpen: true,
        typeDianwangInterval: true,
        typeGongreInterval: true,
        typeGonglengInterval: true,
        typeDianwangIntervalIndex: 0,
        typeGongreIntervalIndex: 0,
        typeGonglengIntervalIndex: 0,
        typeChunengOpen: true,
        typeQiyeOpen: true,
        typePointNameTip: false,
        typeRanqiSelected: false,
        typeGuangfuSelected: false,
        typeChunengSelected: false,
        typeChongdianzhanSelected: false,
        typeQiyeSelected: false,
        typeChongdianzhanOpen: true,
        bottomOpen: false,
        qiyenenghaoOpen: false,//企业弹窗打开
        qiyenenghaoDropdownOpen: false,//企业弹窗选择行业弹窗
        shaixuanTitle: "制造业",
        pointArr: [],
        monitorData: {
          electric: 0,//电能耗
          cold: 0,//冷能耗
          hot: 0,//热能耗
          clean: 0,//清洁能源发电量
          gas: 0,//燃机发电量
          photovoltaic: 0,//光伏发电量
          charge: 0,//储能充电
          discharge: 0,//储能放电
          companyCount: 0,//用能企业数量
          gasCount: 0,//燃气电站数量
          photovoltaicCount: 0,//分布光伏数量
          chargeCount: 0,//分布储能数量
          length: 0,//冷热网长度
          transCount: 0,//变电站数量
          companyCountSum: 0,
          gasCountSum: 0,
          photovoltaicCountSum: 0,
          transCountSum: 0,
          chargeCountSum: 0,
          photovoltaicPlan: 0,//光伏装机已规划）
          photovoltaicUse: 0,//光伏装机已接入
          chargePlan: 2000,//储能装机已接入装机
          chargeUse: 106,//储能装机已接入
        },
        energyRanking: {
          industry: 1,
          pageNum: 0,
          totalPages: 1,
          currentPage: 1,
          currentPageNums: [1, 2, 3, 4, 5],
          showingdata: []
        },
        chongdianzhanData: {
          name: "",//名称
          quickCount: 0,//充电桩数量
          quickPower: 0//额定总功率
        },
        qiyeData: {
          capacity: 0,//容量
          name: "",//企业名称
          usePowerSum: 0,//用电量
          resultList_YDL: []//最近30天日用电量数据
        },
        randianData: {
          capacity: 0,//容量
          name: "",//名称
          provideHotSum: 0,//累计供热量
          providePowerSum: 0,//累计发电量
          startRunDate: "",//投运年份
          resultList_FDL: [],//各月发电量
          resultList_GRL: []//各月供热量
        },
        guangfuData: {
          capacity: 0,//容量
          name: "",//名称
          startRunDate: "",//投运日期
          jinri: 0,
          leiji: 0,
          resultList_PV: []//发电数据
        },
        chunengData: {
          capacity: 0,//容量
          chargeSum: 0,//充电量
          dischargeSum: 0,//放电量
          jinriChong: 0,
          jinriFang: 0,
          name: "",//名称
          batteryType: "",//运行策略
          dailyChargeList: [],//今日充电量数据
          dailyDischargeList: []//今日放电量数据
        },
        hours: ['', '', '', '', '', '', '', '', '', '', '', '1',
          '', '', '', '', '', '', '', '', '', '', '', '2',
          '', '', '', '', '', '', '', '', '', '', '', '3',
          '', '', '', '', '', '', '', '', '', '', '', '4',
          '', '', '', '', '', '', '', '', '', '', '', '5',
          '', '', '', '', '', '', '', '', '', '', '', '6',
          '', '', '', '', '', '', '', '', '', '', '', '7',
          '', '', '', '', '', '', '', '', '', '', '', '8',
          '', '', '', '', '', '', '', '', '', '', '', '9',
          '', '', '', '', '', '', '', '', '', '', '', '10',
          '', '', '', '', '', '', '', '', '', '', '', '11',
          '', '', '', '', '', '', '', '', '', '', '', '12',
          '', '', '', '', '', '', '', '', '', '', '', '13',
          '', '', '', '', '', '', '', '', '', '', '', '14',
          '', '', '', '', '', '', '', '', '', '', '', '15',
          '', '', '', '', '', '', '', '', '', '', '', '16',
          '', '', '', '', '', '', '', '', '', '', '', '17',
          '', '', '', '', '', '', '', '', '', '', '', '18',
          '', '', '', '', '', '', '', '', '', '', '', '19',
          '', '', '', '', '', '', '', '', '', '', '', '20',
          '', '', '', '', '', '', '', '', '', '', '', '21',
          '', '', '', '', '', '', '', '', '', '', '', '22',
          '', '', '', '', '', '', '', '', '', '', '', '23',
          '', '', '', '', '', '', '', '', '', '', '', '24'],
        daysInMonth: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10',
          '11', '12', '13', '14', '15', '16', '17', '18', '19', '20',
          '21', '22', '23', '24', '25', '26', '27', '28', '29', '30'],
        months: ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12'],
      }
    },
    created() {
      this.lengguanSrc = this.lengguanSrcList[0];
      this.reguanSrc = this.reguanSrcList[0];
      this.dianwangSrc = this.dianwangSrcList[0];
    },
    mounted() {
      this.get_openMonitor();
      this.changePicSrc("dianwang");
      this.changePicSrc("gongre");
      this.changePicSrc("gongleng");
    },
    methods: {
      pointClicked(type, siteId) {
        if (this.qiyenenghaoOpen == true)
          return;
        if (type === "ranqidianzhan") {//选择热电站的点
          this.typeRanqiSelected = true;
          this.typeGuangfuSelected = false;
          this.typeChunengSelected = false;
          this.typeChongdianzhanSelected = false;
          this.typeQiyeSelected = false;
          var _opts = {
            method: "post",
            url: "/suzhou_pro/show/siteCurve",
            timestamp:"1",
            siteId:siteId,
            pointArr:"GRL,FDL",
            type:2
          };
          //发送post请求
          httpServer(_opts).then((res) => {
            console.log(res);
            this.randianData = res.data;
            if (this.randianData.providePowerSum)
              this.randianData.providePowerSum = parseFloat(this.randianData.providePowerSum).toFixed(2);
            var _data1 = [];
            var _data2 = [];
            var _yMax1 = 0;
            var _yMax2 = 0;
            for (var i = 0; i < res.data["resultList_FDL"].length; i++) {
              var _dt = new Date(res.data["resultList_FDL"][i].timestamp + "-01");
              var _m = _dt.getMonth();
              _data1[_m] = res.data["resultList_FDL"][i].value;
              if (res.data["resultList_FDL"][i].value >= _yMax1)
                _yMax1 = res.data["resultList_FDL"][i].value
            }
            for (var i = 0; i < res.data["resultList_GRL"].length; i++) {
              var _dt = new Date(res.data["resultList_FDL"][i].timestamp + "-01");
              var _m = _dt.getMonth();
              _data2[_m] = res.data["resultList_GRL"][i].value;
              if (res.data["resultList_GRL"][i].value >= _yMax2)
                _yMax2 = res.data["resultList_GRL"][i].value
            }
            this.initModalChart("chart-randiqianzhan", this.months, {name: ["发电量", "供热量"], max: [_yMax1, _yMax2]}, _data1, _data2, '{b0}月发电量 : {c0} <br/>{b1}月供热量 : {c1}');
          }, (error) => {
            console.log(error);
          })
        } else if (type === "guangfu") {//选择光伏的点
          this.typeRanqiSelected = false;
          this.typeGuangfuSelected = true;
          this.typeChunengSelected = false;
          this.typeChongdianzhanSelected = false;
          this.typeQiyeSelected = false;
          var _opts = {
            method: "post",
            url: "/suzhou_pro/show/siteCurve",
            timestamp:"1",
            siteId:siteId,
            pointArr:"PV.EnergyDay",
            type:1
          };
          //发送post请求
          httpServer(_opts).then((res) => {
            console.log(res);
            this.guangfuData = res.data;
            if (res.data["PV.EnergyDay_value"])
              this.guangfuData.jinri = parseFloat(res.data["PV.EnergyDay_value"]).toFixed(2);
            else this.guangfuData.jinri = 0
            if (res.data["PV.EnergyYear_value"])
              this.guangfuData.leiji = parseFloat(res.data["PV.EnergyYear_value"]).toFixed(2);
            else this.guangfuData.leiji = 0
            var _data = [];
            var _yMax = 0;
            for (var i = 0; i < res.data["resultList_PV.EnergyDay"].length; i++) {
              _data[i] = res.data["resultList_PV.EnergyDay"][i].value;
              if (res.data["resultList_PV.EnergyDay"][i].value > _yMax)
                _yMax = res.data["resultList_PV.EnergyDay"][i].value
            }
            this.initModalChart("chart-guangfu", ['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24'], {
              name: ["发电量", ""],
              max: [_yMax, 0]
            }, _data, null, '{b}时 : {c}');
          }, (error) => {
            console.log(error);
          })
        } else if (type === "chuneng") {//选择储能的点
          this.typeRanqiSelected = false;
          this.typeGuangfuSelected = false;
          this.typeChunengSelected = true;
          this.typeChongdianzhanSelected = false;
          this.typeQiyeSelected = false;
          var _opts = {
            method: "post",
            url: "/suzhou_pro/show/siteCurve",
            timestamp:"1",
            siteId:siteId,
            pointArr:"Storage.Power",
            type:4
          };
          //发送post请求
          httpServer(_opts).then((res) => {
            console.log(res);
            this.chunengData = res.data;
            // Storage.DailyCharge_value: "885.0000"
            // Storage.DailyDischarge_value: "474.0000"
            // Storage.TotalCharge_value: "208029.0000"
            // Storage.TotalCharge_value: "154017.0000"
            if (res.data["Storage.DailyCharge_value"])
              this.chunengData.jinriChong = parseFloat(res.data["Storage.DailyCharge_value"]).toFixed(2);
            else
              this.chunengData.jinriChong = 0;
            if (res.data["Storage.DailyDischarge_value"])
              this.chunengData.jinriFang = parseFloat(res.data["Storage.DailyDischarge_value"]).toFixed(2);
            else
              this.chunengData.jinriFang = 0;
            if (res.data["Storage.TotalCharge_value"])
              this.chunengData.chargeSum = parseFloat(res.data["Storage.TotalCharge_value"]).toFixed(2);
            else
              this.chunengData.chargeSum = 0;
            if (res.data["Storage.TotalDischarge_value"])
              this.chunengData.dischargeSum = parseFloat(res.data["Storage.TotalDischarge_value"]).toFixed(2);
            else
              this.chunengData.dischargeSum = 0;
            var _data1 = [];
            var _yMax1 = 0;
            for (var i = 0; i < 288; i++) {
              _data1.push(0);
            }
            for (var i = 0; i < res.data["resultList_Storage.Power"].length; i++) {
              var _dt = new Date(res.data["resultList_Storage.Power"][i].timestamp);
              var _idx = _dt.getHours() * 12 + _dt.getMinutes() / 5;
              _data1[_idx - 1] = res.data["resultList_Storage.Power"][i].value;
              if (res.data["resultList_Storage.Power"][i].value >= _yMax1)
                _yMax1 = res.data["resultList_Storage.Power"][i].value
            }
            this.initModalChart("chart-chuneng", this.hours, {name: ["充电"], max: [_yMax1]}, _data1, null, '{b}时 : {c}');
          }, (error) => {
            console.log(error);
          })
        } else if (type === "chongdianzhan") {//选择充电站的点
          this.typeRanqiSelected = false;
          this.typeGuangfuSelected = false;
          this.typeChunengSelected = false;
          this.typeChongdianzhanSelected = true;
          this.typeQiyeSelected = false;
          var _opts = {
            method: "post",
            url: "/suzhou_pro/show/siteCurve",
            timestamp:"1",
            siteId:siteId,
            pointArr:"YDL",
            type:5
          };
          //发送post请求
          httpServer(_opts).then((res) => {
            console.log(res);
            this.chongdianzhanData = res.data;
          }, (error) => {
            console.log(error);
          })
        } else if (type === "qiye") {//选择企业的点
          this.typeRanqiSelected = false;
          this.typeGuangfuSelected = false;
          this.typeChunengSelected = false;
          this.typeChongdianzhanSelected = false;
          this.typeQiyeSelected = true;
          this.typePointNameTip = false;
          var _opts = {
            method: "post",
            url: "/suzhou_pro/show/siteCurve",
            timestamp:"1",
            siteId:siteId,
            pointArr:"YDL",
            type:3
          };
          //发送post请求
          httpServer(_opts).then((res) => {
            console.log(res);
            this.qiyeData = res.data;
            var _data = [];
            var _yMax1 = 0;
            for (var i = 0; i < res.data["resultList_YDL"].length; i++) {
              var _dt = new Date(res.data["resultList_YDL"][i].timestamp);
              _data[_dt.getDate() - 1] = res.data["resultList_YDL"][i].value;
              if (res.data["resultList_YDL"][i].value >= _yMax1)
                _yMax1 = res.data["resultList_YDL"][i].value
            }
            var _xAxisData = [30];
            var ts = new Date().getTime();
            for (var i = 0; i < 30; i++) {
              _xAxisData[29 - i] = new Date(ts).getDate();
              ts = ts - 86400000;
            }
            this.initModalChart("chart-qiye", _xAxisData, {name: ["用电量", ""], max: [_yMax1, 0]}, _data);
          }, (error) => {
            console.log(error);
          })
        } else if (type === "none") {//啥也没选
          this.typeRanqiSelected = false;
          this.typeGuangfuSelected = false;
          this.typeChunengSelected = false;
          this.typeChongdianzhanSelected = false;
          this.typeQiyeSelected = false;
        }
      },
      showName(event, type, siteId) {
        if (this.qiyenenghaoOpen == true)
          return;
        this.typePointNameTip = true;
        $(".modal.qiye2").css({
          left: event.pageX > 1440 ? "1400px" : (event.pageX - 50 + "px"),
          top: event.pageY > 60 ? (event.pageY - 50 + "px") : "10px"
        });
        if (type === "ranqidianzhan") {//选择热电站的点
          var _opts = {
            method: "post",
            url: "/suzhou_pro/show/siteCurve",
            timestamp: "1",
            siteId: siteId,
            pointArr: "GRL,FDL",
            type: 2
          };
          //发送post请求
          httpServer(_opts).then((res) => {
            console.log(res);
            this.qiyeData = res.data;
          }, (error) => {
            console.log(error);
          })
        } else if (type === "guangfu") {//选择光伏的点
          var _opts = {
            method: "post",
            url: "/suzhou_pro/show/siteCurve",
            timestamp: "1",
            siteId: siteId,
            pointArr: "PV.EnergyDay",
            type: 1
          };
          //发送post请求
          httpServer(_opts).then((res) => {
            console.log(res);
            this.qiyeData = res.data;
          }, (error) => {
            console.log(error);
          })
        } else if (type === "chuneng") {//选择储能的点
          var _opts = {
            method: "post",
            url: "/suzhou_pro/show/siteCurve",
            timestamp: "1",
            siteId: siteId,
            pointArr: "Storage.Power",
            type: 4
          };
          //发送post请求
          httpServer(_opts).then((res) => {
            console.log(res);
            this.qiyeData = res.data;
          }, (error) => {
            console.log(error);
          })
        } else if (type === "chongdianzhan") {//选择充电站的点
          var _opts = {
            method: "post",
            url: "/suzhou_pro/show/siteCurve",
            timestamp: "1",
            siteId: siteId,
            pointArr: "YDL",
            type: 5
          };
          //发送post请求
          httpServer(_opts).then((res) => {
            console.log(res);
            this.qiyeData = res.data;
          }, (error) => {
            console.log(error);
          })
        } else if (type === "qiye") {//选择企业的点
          var _opts = {
            method: "post",
            url: "/suzhou_pro/show/siteCurve",
            timestamp: "1",
            siteId: siteId,
            pointArr: "YDL",
            type: 3
          };
          //发送post请求
          httpServer(_opts).then((res) => {
            console.log(res);
            this.qiyeData = res.data;
          }, (error) => {
            console.log(error);
          })
        }
      },
      typeSelected(type) {
        if (type === "ranqidianzhan" && !this.typeRanqiOpen) {
          this.typeRanqiSelected = false;
        } else if (type === "guangfu" && !this.typeGuangfuOpen) {
          this.typeGuangfuSelected = false;
        } else if (type === "chuneng" && !this.typeChunengOpen) {
          this.typeChunengSelected = false;
        } else if (type === "chongdianzhan" && !this.typeChongdianzhanOpen) {
          this.typeChongdianzhanSelected = false;
        } else if (type === "qiye" && !this.typeQiyeOpen) {
          this.typeQiyeSelected = false;
        } else if (type === "dianwang") {
          if (!this.typeDianwangOpen) {
            clearInterval(this.typeDianwangInterval);
            this.typeDianwangIntervalIndex = 0;
            this.dianwangSrc = this.dianwangSrcList[0];
            this.dianwangStyle= "display:none";
          } else {
            this.changePicSrc(type)
            this.dianwangStyle= "display:block";
          }
        } else if (type === "gongre") {
          if (!this.typeGongreOpen) {
            clearInterval(this.typeGongreInterval);
            this.typeGongreIntervalIndex = 0;
            this.reguanSrc = this.reguanSrcList[0];
            this.reguanStyle= "display:none";
          } else {
            this.changePicSrc(type)
            this.reguanStyle= "display:block";
          }
        } else if (type === "gongleng") {
          if (!this.typeGonglengOpen) {
            clearInterval(this.typeGonglengInterval);
            this.typeGonglengIntervalIndex = 0;
            this.lengguanSrc = this.lengguanSrcList[0];
            this.lengguanStyle= "display:none";
          } else {
            this.changePicSrc(type)
            this.lengguanStyle= "display:block";
          }
        }
      },
      /**
       * 切换背景图
       */
      changePicSrc(type) {
        if (type === "dianwang") {
          let that = this;
          that.typeDianwangInterval = setInterval(function () {
            that.typeDianwangIntervalIndex++;
            that.dianwangSrc = that.dianwangSrcList[that.typeDianwangIntervalIndex];
            if (that.typeDianwangIntervalIndex > 70) {
              that.typeDianwangIntervalIndex = 0;
            }
          }, 60);
        } else if (type === "gongre") {
          let that = this;
          that.typeGongreInterval = setInterval(function () {
            that.typeGongreIntervalIndex++;
            that.reguanSrc = that.reguanSrcList[that.typeGongreIntervalIndex];
            if (that.typeGongreIntervalIndex > 70) {
              that.typeGongreIntervalIndex = 0;
            }
          }, 60);
        } else if (type === "gongleng") {
          let that = this;
          that.typeGonglengInterval = setInterval(function () {
            that.typeGonglengIntervalIndex++;
            that.lengguanSrc = that.lengguanSrcList[that.typeGonglengIntervalIndex];
            if (that.typeGonglengIntervalIndex > 35) {
              that.typeGonglengIntervalIndex = 0;
            }
          }, 60);
        }
      },
      getBottomData(_page, _industry) {
        this.get_energyRanking(_page, _industry);
        this.typeRanqiSelected = false;
        this.typeGuangfuSelected = false;
        this.typeChunengSelected = false;
        this.typeChongdianzhanSelected = false;
        this.typeQiyeSelected = false;
      },
      /**
       */
      changeIndustry(_industry) {
        this.energyRanking.industry = _industry;
        this.qiyenenghaoDropdownOpen = false;
        this.energyRanking.totalPages = 1;
        this.energyRanking.currentPage = 1;
        this.get_energyRanking(1, _industry);
      },
      prevPage() {
        if (this.energyRanking.currentPage > 1)
          this.energyRanking.currentPage--;
        this.get_energyRanking(this.energyRanking.currentPage, this.energyRanking.industry);
      },
      nextPage() {
        if (this.energyRanking.currentPage < this.energyRanking.totalPages)
          this.energyRanking.currentPage++;
        this.get_energyRanking(this.energyRanking.currentPage, this.energyRanking.industry);
      },
      changePage(pageNum) {
        this.energyRanking.currentPage = pageNum;
        this.get_energyRanking(pageNum, this.energyRanking.industry);
      },
      /**
       * 一、  多功能全景监控展开接口
       */
      get_openMonitor() {
        //发送get请求
        httpServer({
          method: "post",
          url: "/suzhou_pro/show/openMonitor",
        }).then((res) => {
          console.log(res);
          this.monitorData = res.data;
        }, (error) => {
          console.log(error);
        })
      },
      /**
       * 二、  企业能耗排名接口
       */
      get_energyRanking(_page, _industry) {
        var _opts = {
          method: "post",
          url: "/suzhou_pro/show/energyRanking",
          page: _page,
          pageSize: 15
        };
        if (typeof _industry != 'undefined' && _industry > 0)
          _opts.industry = _industry;
        let that = this;
        //发送get请求
        httpServer(_opts).then((res) => {
          console.log(res);
          var _max = res.data.max;
          that.energyRanking.max = Number(res.data.max).toFixed(2);
          that.energyRanking.plan = res.data.plan.toFixed(2);
          that.energyRanking.totalPages = res.data.list.pages;
          that.energyRanking.showingdata = res.data.list.list;
          for (var i = 0; i < that.energyRanking.showingdata.length; i++) {
            that.energyRanking.showingdata[i].index = (that.energyRanking.currentPage == 1 ? 0 : (that.energyRanking.currentPage - 1) * 21) + (i + 1);
            that.energyRanking.showingdata[i].perct = parseFloat(that.energyRanking.showingdata[i].energy / _max).toFixed(4);
          }
          //重新计算页码
          if (res.data.list.pages < 5) {
            var list = [];
            for (var i = 1; i <= res.data.list.pages; i++) {
              list.push(i);
            }
            that.energyRanking.currentPageNums = list;
          } else {
            if (res.data.list.pageNum <= 3)
              that.energyRanking.currentPageNums = [1, 2, 3, 4, 5];
            else if (res.data.list.pageNum < res.data.list.pages - 2)
              that.energyRanking.currentPageNums = [res.data.list.pageNum - 2, res.data.list.pageNum - 1, res.data.list.pageNum, res.data.list.pageNum + 1, res.data.list.pageNum + 2];
            else
              that.energyRanking.currentPageNums = [res.data.list.pages - 4, res.data.list.pages - 3, res.data.list.pages - 2, res.data.list.pages - 1, res.data.list.pages];
          }
          setTimeout(function () {
            that.reClacDataItemLength();//计算条形图百分比
          }, 1000);
        }, (error) => {
          console.log(error);
        })
      },

      initModalChart(_id, _xAxisData, _yAxis, _data1, _data2, _formatter2) {
        let chart = this.$echarts.init(document.getElementById(_id));
        var _formatter = _data2 ? '{b0}日 : {c0} <br/>{b1}日 : {c1}' : '{b}日 : {c}';
        if (_formatter && _formatter2)
          _formatter = _formatter2;
        var option = {
          tooltip: {
            trigger: 'axis',
            formatter: _formatter
          },
          xAxis: {
            type: 'category',
            data: _xAxisData,
            axisLabel: {
              interval: 0,
              color: "#839191",
              align: "center",
              fontSize: 8
            },
            axisTick: {
              show: false
            }
          },
          yAxis: [{
            name: _yAxis.name[0],
            max: _yAxis.max[0],
            nameTextStyle: {
              color: "#839191",
              fontSize: 12
            },
            axisLabel: {
              color: "#839191",
              fontSize: 8
            },
            axisTick: {
              show: false
            },
            splitLine: {
              show: false
            }
          }],
          series: [{
            data: _data1,
            name: _yAxis.name[0],
            type: 'line',
            symbolSize: 0,
            lineStyle: {
              color: "#5EF4FF",
              width: 2
            }
          }]
        };

        if (_data2){
          option.yAxis.push({
            name: _yAxis.name[1],
            max: _yAxis.max[1],
            nameTextStyle: {
              color: "#839191",
              fontSize: 12
            },
            axisLabel: {
              color: "#839191",
              fontSize: 8
            },
            axisTick: {
              show: false
            },
            splitLine: {
              show: false
            },
          });
          option.series.push({
            name: _yAxis.name[1],
            data: _data2,
            type: 'line',
            yAxisIndex: 1,
            symbolSize: 0,
            lineStyle: {
              color: "#E9AC21",
              width: 2
            }
          });
        }
        console.log(JSON.stringify(option))
        // 使用刚指定的配置项和数据显示图表。
        chart.setOption(option);
      },

      bodyClicked(e) {
        console.log(e);
        //企业能耗排名按钮
        if (this.qiyenenghaoOpen == true) {
          var within = false;
          $.each($(e.target).parents(), function (idx, obj) {
            if ($(obj).hasClass("qiyenenghaopaiming-modal")) {
              within = true;
              return false;
            }
          });
          if (within || $(e.target).hasClass("qiyenenghaopaiming")) {//底部打开
            return;
          } else if (e.pageX < 196 || e.pageX > 196 + 1528 || e.pageY < 157 || e.pageY > 766 + 157) { // 企业能耗排名 width: 1528px; height: 766px; left: 196px; top: 157px;
            this.qiyenenghaoOpen = false;
          }
        }

        if (this.qiyenenghaoDropdownOpen == true) {
          //行业筛选按钮  805 20    80 20
          if ($(e.target).hasClass("dropdown") || $(e.target).parent().hasClass("dropdown")) {
            return;
          }
          // width: 321px; height: 576px; left: 790px; top: 215px;
          else if (e.pageX < 790 || e.pageX > 790 + 321 || e.pageY < 215 || e.pageY > 576 + 215)
            this.qiyenenghaoDropdownOpen = false;
        }

        //width: 480; height: 426; left: 678; top: 223;
        if (this.typeQiyeSelected == true) {
          if (e.target.className.indexOf("qiye") >= 0)
            return
          if (e.pageX < 678 || e.pageX > 678 + 480 || e.pageY < 223 || e.pageY > 426 + 223)
            this.typeQiyeSelected = false;
        }

        //width: 480; height: 392; left: 720; top: 304;
        if (this.typeGuangfuSelected == true) {
          if (e.target.className.indexOf("guangfu") >= 0)
            return
          if (e.pageX < 720 || e.pageX > 720 + 480 || e.pageY < 304 || e.pageY > 392 + 304)
            this.typeGuangfuSelected = false;
        }

        //width: 480; height: 488; left: 720; top: 256;
        if (this.typeChunengSelected == true) {
          if (e.target.className.indexOf("chuneng") >= 0)
            return
          if (e.pageX < 720 || e.pageX > 720 + 480 || e.pageY < 256 || e.pageY > 488 + 256)
            this.typeChunengSelected= false;
        }

        //width: 384; height: 192; left: 768; top: 404;
        if (this.typeChongdianzhanSelected == true) {
          if (e.target.className.indexOf("chongdianzhan") >= 0)
            return
          if (e.pageX < 768 || e.pageX > 768 + 384 || e.pageY < 404 || e.pageY > 192 + 404)
            this.typeChongdianzhanSelected = false;
        }

        // width: 480;  height: 490; left: 720; top: 255;
        if (this.typeRanqiSelected == true) {
          if (e.target.className.indexOf("ranqidianzhan") >= 0)
            return
          if (e.pageX < 720 || e.pageX > 720 + 480 || e.pageY < 255 || e.pageY > 490 + 255)
            this.typeRanqiSelected = false;
        }
      },

      mouseMoved(e) {
        if (this.typePointNameTip == true && $(e.target).parent().hasClass("points")) {
          return;
        }
        this.typePointNameTip = false
      },

      /**
       * 计算条形图百分比
       */
      reClacDataItemLength() {
        $.each($(".qiyenenghaopaiming-modal .content .row .item .bar-data"), function () {
          var attrs = $(this)[0].attributes;
          for (var i = 0; i < attrs.length; i++) {
            if (attrs[i].nodeName === "data-perct") {
              var _w = parseFloat(attrs[i].value).toFixed(2) * 300;
              $(this).css("width", _w + "px");
              break;
            }
          }
        })
      },

      tabItemClicked(event, tabIndex) {
        //tab-content
        $(event.target).addClass("active").siblings().removeClass("active");
        $(".modal.qiye").find(".tab-content").addClass("hide");
        $(".modal.qiye").find(".tab-content" + tabIndex).removeClass("hide");

        var _xAxisData = [30];
        var _data = [];
        var _yMax1 = 0;
        for (var i = 0; i < 30; i++) {
          _data[i] = parseFloat(Math.random() * 100).toFixed(2);
          if (_data[i] >= _yMax1)
            _yMax1 = _data[i]
        }
        var ts = new Date().getTime();
        for (var i = 0; i < 30; i++) {
          _xAxisData[29 - i] = new Date(ts).getDate();
          ts = ts - 86400000;
        }
        var type = "";
        switch (tabIndex) {
          case 2:
            type = "热";
            break;
          case 3:
            type = "气";
            break;
          case 4:
            type = "水";
            break;
        }
        this.initModalChart("chart-qiye2", _xAxisData, {name: ["用" + type + "量", ""], max: [_yMax1, 0]}, _data);
      }

      //end of methods
    }
  }
</script>

<style scoped>
  @import '../../../assets/css/public.css';
  @import 'assets/css/quanjing.css';
</style>
