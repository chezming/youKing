<template>
    <div class="main_content">
      <div v-if="isDetail" class="detailMain">
        <div class="backFund" @click="backFund">&lt;返回</div>
        <div class="detail_mes">
          <div class="detail_name">{{detail.name}}</div>
          <div class="detail_code">&nbsp;{{detail.code}}</div>
          <div style="clear: both"></div>
        </div>
        <div class="detail_blocks">
          <div class="detail_left">
            <div class="detail_lt">
              <div id="detailChart1" :style="{width: '90%', height: '300px'}"></div>
            </div>
            <div class="detail_lb">
              <div class="comment">
                <div class="comment_title">评论区</div>
                <div class="comment_con">
                  <div class="comment_li" v-for="(item,i) in comments">
                    <div class="comment_id"><p>{{item.userId}}</p><img class="confirm" src="../../static/news_img/v.png" alt=""></div>
                    <div class="comment_time">{{item.time | formatDate}}</div>
                    <div class="comment_mes">{{item.commentContent}}</div>
                    <div style="clear: both"></div>
                  </div>
                </div>
                <el-input type="textarea" class="textarea" :autosize="{ minRows: 2, maxRows: 2}" placeholder="请输入内容" v-model="textarea"></el-input>
                <div class="submit_bt"><el-button plain class="sbt" @click="subComment">提交</el-button></div>
              </div>
              <div class="center">
                <div class="center_top">
                  <div class="center_t1">
                    <div class="ct1">
                      <div class="ct1_t">总价值</div>
                      <div class="red">￥{{totalValue}}</div>
                      <div class="ct1_t">日收益均值</div>
                      <div class="ct1_c">￥{{DetailFund.mean}}</div>
                    </div>
                  </div>
                  <div class="center_t2">
                    <div id="detailChart2" :style="{width: '90%', height: '90%'}"></div>
                  </div>
                </div>
                <div class="center_bottom"></div>
              </div>
            </div>
          </div>
          <div class="detail_right">
            <div class="detail_ul">
              <div class="detail_tip">
                <div class="detail_tiptip">基金管理者</div>
                <div class="detail_tiptip">基金托管人</div>
                <div class="detail_tiptip">运作模式</div>
                <div class="detail_tiptip">投资类型</div>
                <div class="detail_tiptip">开始时间</div>
                <div class="detail_tiptip">短期beta</div>
                <div class="detail_tiptip">长期beta</div>
                <div class="detail_tiptip">资本规模</div>
                <div class="detail_tiptip">成立时长</div>
              </div>
              <div class="detail_data">
                <div class="detail_dt">{{detail.advisor}}</div>
                <div class="detail_dt">{{detail.trustee}}</div>
                <div class="detail_dt">{{detail.operateMode}}</div>
                <div class="detail_dt">{{detail.underlyingAssetType}}</div>
                <div class="detail_dt">{{detail.startDate|formatDate}}</div>
                <div class="detail_dt">{{DetailFund.shortbeta}}</div>
                <div class="detail_dt">{{DetailFund.longbeta}}</div>
                <div class="detail_dt">{{DetailFund.capscale}}</div>
                <div class="detail_dt">{{DetailFund.existtime}}</div>
              </div>
            </div>
            <div class="stock_block"></div>
          </div>
        </div>
      </div>
      <div class="news_left"v-if="!isDetail">
        <div class="news_div">
          <div class="news_list_title">自选基金</div>
          <ul class="fund_ul">
            <div class="fund_contain fd_con1" v-for="(item,i) in conFund" @click="getFundDetail(item)">
              <div class="fund_mes">
                <div class="fund_code">{{item.code}}</div>
                <div class="fund_name">{{item.name}}</div>
                <div class="fund_advisor">{{item.advisor}}</div>
                <div class="fund_type">{{item.underlyingAssetType}}</div>
<!--                <div class="collect_button">+&nbsp;收藏</div>-->
                <div class="cancell_button">取消收藏</div>
              </div>
            </div>
          </ul>
        </div>
      </div>
      <div class="news_right"v-if="!isDetail">
        <div class="news_main">
          <div class="news_main_title"><p class="t1">推荐基金</p><p class="t2">Recommend</p><div style="clear: both"></div></div>
          <div class="fund_recom">
            <div class="fund_contain fd_con3" v-for="(item,i) in RsFund" @click="getFundDetail(item)">
              <div class="fund_mes">
                <div class="fund_code">{{item.code}}</div>
                <div class="fund_name">{{item.name}}</div>
                <div class="fund_advisor">{{item.advisor}}</div>
                <div class="fund_type">{{item.underlyingAssetType}}</div>
                <div class="collect_button">+&nbsp;收藏</div>
<!--                <div class="cancell_button">取消收藏</div>-->
              </div>
            </div>
          </div>
          <div class="news_main_title"><p class="t1">全部基金</p><p class="t2">All</p><div style="clear: both"></div></div>
          <div class="fund_recom2">
            <div class="fund_contain fd_con3" v-for="(item,i) in allFund" @click="getFundDetail(item)">
              <div class="fund_mes">
                <div class="fund_code">{{item.code}}</div>
                <div class="fund_name">{{item.name}}</div>
                <div class="fund_advisor">{{item.advisor}}</div>
                <div class="fund_type">{{item.underlyingAssetType}}</div>
                <div class="collect_button">+&nbsp;收藏</div>
                <!--                <div class="cancell_button">取消收藏</div>-->
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import {formatDate} from "../../static/date";

    export default {
        name: "fund",
        props:{
            userid:{
                type:Object,
                default:null,
            }
        },
        filters:{
            formatDate(time) {
                let date = new Date(time);
                console.log(new Date(time));
                return formatDate(date, 'yyyy-MM-dd hh:mm');
            },
        },
        data() {
            return {
                msg: "Hello Vue.js",
                allFund: '',
                RsFund: '',
                conFund: '',
                DetailFund: '',
                isDetail: false,
                link: 'http://localhost:8181',
                detail: '',
                textarea: '',
                totalValue: '',
                stylePie:
                    [{
                        name: '985院校',
                        value: 1
                    },{
                        name: '211院校',
                        value: 1
                    },{
                        name: '普通院校',
                        value: 1
                    }
                    ],
                Chart1:[[]],
                Pie1:[
                    {
                        name: '资产价值',
                        value: 0
                    },
                    {
                        name: '股票价值',
                        value: 0
                    },
                    {
                        name: '债券价值',
                        value: 0
                    },{
                        name: '贵金属价值',
                        value: 0
                    },{
                        name: '衍生品价值',
                        value: 0
                    },{
                        name: '回购价值',
                        value: 0
                    },{
                        name: '存款价值',
                        value: 0
                    },{
                        name: '其他价值',
                        value: 0
                    },
                ],
                comments: [],
                sendComment:{
                    code: '',
                    newsOrFund: 1,
                    commentContent: '',
                    userId: '',
                    time: ''
                },
            }
        },
        components: {
            //someComponent
        },
        created() {
            this.getAllFund();
            this.getRsFund();
        },
        mounted(){
            // this.drawLeft();
        },
        methods: {
            getAllFund(){
                axios.get(this.link+'/fund_basis/findAll').then(res=>{
                    this.allFund = res.data;
                    console.log(res);
                })
            },
            getRsFund(){
                axios.get(this.link+'/fund_basis/findRs/'+this.userid).then(res=>{
                    this.RsFund = res.data;
                    console.log(res);
                })
                axios.get(this.link+'/fund_basis/findCF/'+this.userid).then(res=>{
                    this.conFund = res.data;
                    console.log(res);
                })
            },
            getFundDetail(item){
                this.isDetail = true;
                this.detail = item;
                axios.get(this.link+'/fund_feature/findAll/'+item.code).then(res=>{
                    this.DetailFund = res.data;
                    console.log(res);
                    this.drawLeft(item.code);
                    this.drawCenter(item.code);
                    this.getComment('000004')
                })
            },
            subComment(){
                if(this.textarea !== ''){
                    this.sendComment.code = this.detail.code;
                    this.sendComment.commentContent = this.textarea;
                    this.sendComment.userId = this.userid;
                    this.sendComment.time = new Date();
                    axios.post(this.link+'/comment_basis/save',this.sendComment).then(res=>{
                        this.textarea = '';
                        this.getComment(this.sendComment.code);
                        alert("发表成功");
                    })
                }else {
                    alert("评论不能为空！")
                }
            },
            backFund(){
                this.isDetail =false;
            },
            drawLeft(code){
                axios.get(this.link+'/fund_net_value/findLineData/'+code).then(res=>{
                    for(let i=0;i<res.data.length;i++){
                        this.Chart1[i] = [];
                        this.Chart1[i][0] = res.data[i].date;
                        this.Chart1[i][1] = res.data[i].refactorNetValue;
                    }
                    console.log(res.data);
                    console.log(this.Chart1);
                    let detailChart1 = this.$echarts.init(document.getElementById('detailChart1'))
                    // console.log(11111)
                    detailChart1.setOption({
                        title: {
                            text: '基金走势图'
                        },
                        tooltip: {
                            trigger: 'axis'
                        },
                        legend: {
                            data: ['']
                        },
                        dataZoom: [
                            {
                                show: true,
                                realtime: true,
                                start: 60,
                                end: 70,
                            },
                            {
                                type: 'inside',
                                realtime: true,
                                start: 30,
                                end: 70,
                            }
                        ],
                        grid: {
                            left: '3%',
                            right: '4%',
                            bottom: '3%',
                            containLabel: true
                        },
                        toolbox: {
                            feature: {
                                saveAsImage: {}
                            }
                        },
                        xAxis: {
                            type: 'time',
                            boundaryGap: false,
                        },
                        yAxis: {
                            type: 'value',splitLine: {
                                show: false
                            },
                            scale:true,/*按比例显示*/
                        },
                        series: [
                            {
                                name: '价格',
                                type: 'line',
                                stack: '总量',
                                data: this.Chart1
                            },
                        ]
                    });
                })

            },
            drawCenter(code){
                axios.get(this.link+'/fund_port_all/findPieData/'+code).then(res=>{
                    this.Pie1[0].value = res.data.equityValue;
                    this.Pie1[1].value = res.data.stockValue;
                    this.Pie1[2].value = res.data.fixedIncomeValue;
                    this.Pie1[3].value = res.data.preciousMetalValue;
                    this.Pie1[4].value = res.data.derivativeValue;
                    this.Pie1[5].value = res.data.buyingBackValue;
                    this.Pie1[6].value = res.data.depositValue;
                    this.Pie1[7].value = res.data.othersValue;
                    this.totalValue = res.data.totalAsset;
                    console.log(res)
                let detailChart2 = this.$echarts.init(document.getElementById('detailChart2'))
                // console.log(11111)
                detailChart2.setOption({
                    title: {
                        text: '投资比例图',
                        // subtext: '纯属虚构',
                        // left: 'left'
                    },
                    tooltip: {
                        trigger: 'item',
                        formatter: '{b} :￥ {c} ({d}%)'
                    },
                    legend: {
                        type: 'scroll',
                        orient: 'vertical',
                        right: 10,
                        top: 20,
                        bottom: 20,
                        // data: this.styleLists,

                    },
                    series: [
                        {
                            name: '去向',
                            type: 'pie',
                            radius: '55%',
                            center: ['40%', '50%'],
                            data: this.Pie1,
                            emphasis: {
                                itemStyle: {
                                    shadowBlur: 10,
                                    shadowOffsetX: 0,
                                    shadowColor: 'rgba(0, 0, 0, 0.5)'
                                }
                            },
                            label: {
                                normal: {
                                    position: 'inner',
                                    show: false,
                                }
                            },
                        }
                    ]
                })
                })
            },
            getComment(code){
                axios.get(this.link+'/comment_basis/findByCode/'+code).then(res=>{
                    this.comments = res.data;
                    console.log(111)
                    console.log(res);
                })
            },

        },

    }
</script>

<style>
  .main_content{
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .news_left{
    width: 22%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .news_right{
    width: 78%;
    height: 100%;
    background-color: white;
    border-top-left-radius: 30px;
    border-bottom-left-radius: 30px;
    box-shadow: rgba(0,0,0,0.01) -5px 0px 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .news_list_title{
    font-size: 24px;
    /*font-weight: 600;*/
    color: #2A2E31;
    margin-left: 12%;
    font-family: 方正粗黑宋简体;
  }
  .news_div{
    height: 90%;
    width: 100%;
  }
  .news_main{
    width: 86%;
    height: 80%;
  }
  .news_main_title .t1{
    font-family: 方正粗黑宋简体;
    font-size: 46px;
    float: left;
  }
  .news_main_title .t2{
    font-family: 方正粗黑宋简体;
    font-size: 30px;
    float: left;
    padding: 16px 10px;
    color: #6d767d;
  }
  .frontP{
    font-family: 方正粗黑宋简体;
    font-size: 14px;
    color: #6d767d;
    cursor: pointer;
    float: right;
    margin-right: 20px;
    margin-top: 5px;
  }
  .frontP:hover{
    color: #2A2E31;
  }
  .nextP{
    font-family: 方正粗黑宋简体;
    font-size: 14px;
    color: #6d767d;
    cursor: pointer;
    float: right;
    margin-top: 5px;
  }
  .nextP:hover{
    color: #2A2E31;
  }
  .fund_ul{
    width: 100%;
    height: 90%;
    margin-top: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    overflow-y: scroll;
  }
  .fund_ul::-webkit-scrollbar{
    width:6px;
    height:10px;
    /**/
  }
  .fund_ul::-webkit-scrollbar-track{
    background: rgb(239, 239, 239);
    border-radius:2px;
  }
  .fund_ul::-webkit-scrollbar-thumb{
    background: #6D767D!important;
    border-radius:10px!important;
  }
  .fund_ul::-webkit-scrollbar-thumb:hover{
    background: #333;
  }
  .fund_ul::-webkit-scrollbar-corner{
    background: #179a16;
  }
  .fund_contain{
    width: 200px;
    border-radius: 15px;
    border: #a1a8ad solid 1px;
    cursor: pointer;
    background-color: white;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .fd_con1{
    height: 19%;
  }
  .fd_con2{
    height: 100%;
  }
  .fd_con3{
    margin-top: 10px;
    height: 140px;
  }
  .fund_mes{
    width: 90%;
    height: 80%;
    position: relative;
  }
  .fund_code{
    font-family: "Microsoft YaHei UI";
    font-size: 24px;
    color: #2a2e31;
  }
  .fund_name{
    font-family: "Microsoft YaHei UI";
    font-size: 16px;
    color: #2a2e31;
  }
  .fund_advisor{
    font-family: "Microsoft YaHei UI";
    font-size: 12px;
    color: #2a2e31;
  }
  .fund_type{
    font-family: "Microsoft YaHei UI";
    font-size: 12px;
    color: #2a2e31;
    position: absolute;
    bottom: 0px;
    left: 0px;
    margin-top: 12px;
  }
  .collect_button{
    width: 36%;
    height: 26px;
    border-radius: 5px;
    background-color: #FF3441;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    bottom: 0px;
    right: 0px;
  }
  .cancell_button{
    width: 36%;
    height: 26px;
    border-radius: 5px;
    background-color: #a1a8ad;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    bottom: 0px;
    right: 0px;
  }
  .fund_recom{
    width: 100%;
    height: 25%;
    overflow-y: scroll;
    /*background-color: blue;*/
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    flex-wrap: wrap;
  }
  .fund_recom2{
    width: 100%;
    height: 50%;
    /*background-color: blue;*/
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    overflow-y: scroll;
  }
  .backFund{
    cursor: pointer;
  }
  .detailMain{
    width: 90%;
    height: 90%;
  }
  .detail_mes{
    width: 100%;
  }
  .detail_mes div{
    font-family: "Microsoft YaHei UI";
    color: #2a2e31;
    font-size: 16px;
  }
  .detail_name{
    font-family: 方正粗黑宋简体!important;
    float: left;
    font-size: 26px!important;
  }
  .detail_code{
    font-family: 方正粗黑宋简体!important;
    font-size: 26px!important;
  }
  .detail_blocks{
    width: 100%;
    height: 90%;
    display: flex;
    justify-content: space-between;
  }
  .detail_left{
    width: 68%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .detail_right{
    width: 30%;
    height: 100%;
    border-radius: 20px;
    background-color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .detail_tip{
    width: 150px;
  }
  .detail_data{
    width: 100%;
    overflow-x: scroll;
  }
  ::-webkit-scrollbar{
    width:5px;
    height:5px;
  }
  ::-webkit-scrollbar-track{
    background: rgb(239, 239, 239);
    border-radius:2px;
  }
  ::-webkit-scrollbar-thumb{
    background: #6D767D!important;
    border-radius:10px!important;
  }
  ::-webkit-scrollbar-thumb:hover{
    background: #333;
  }
  ::-webkit-scrollbar-corner{
    background: #179a16;
  }
  .detail_tiptip{
    font-family: 方正粗黑宋简体;
    line-height: 26px;
    font-size: 16px;
  }
  .detail_dt{
    font-family: "Microsoft YaHei UI";
    line-height: 26px;
    font-size: 16px;
    width: 100%;
    /*overflow-x: scroll;*/
    word-break:keep-all; /* 不换行 */
    white-space:nowrap; /* 不换行 */
  }
  .detail_ul{
    width: 80%;
    height: 40%;
    display: flex;
    justify-content: space-between;
  }
  .detail_lt{
    width: 100%;
    height: 50%;
    background-color: white;
    border-radius: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
  }
  .detail_lb{
    width: 100%;
    height: 47%;
    display: flex;
    justify-content: space-between;
  }
  .comment{
    width: 40%;
    height: 100%;
    background-color: white;
    border-radius: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .comment_li{
    margin-top: 10px;
  }
  .comment_title{
    font-family: 方正粗黑宋简体;
    line-height: 26px;
    font-size: 18px;
    width: 90%;
  }
  .comment_id p{
    font-family: 方正粗黑宋简体;
    font-size: 16px;
    float: left;
  }
  .comment_time,.comment_mes{
    font-family: "Microsoft YaHei UI";
    font-size: 12px;
    line-height: 16px;
    width: 100%;
    float: left;
  }
  .comment_mes{
    margin-top: 5px;
  }
  .confirm{
    width: 12px;
  }
  .comment_id{
    display: flex;
    align-items: center;
  }
  .center{
    width: 58%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .center_top{
    width: 100%;
    height: 46%;
    display: flex;
    justify-content: space-between;
  }
  .center_bottom{
    width: 100%;
    height: 50%;
    background-color: white;
    border-radius: 20px;
  }
  .center_t1{
    width: 30%;
    height: 100%;
    background-color: white;
    border-radius: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .center_t2{
    width: 68%;
    height: 100%;
    background-color: white;
    border-radius: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .comment_con{
    width: 86%;
    height: 60%;
    overflow-y: scroll;
  }
  .ct1{
    width: 90%;
    height: 80%;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  .ct1_t{
    font-family: 方正粗黑宋简体;
    font-size: 16px;
  }
  .red{
    font-family: 方正粗黑宋简体;
    font-size: 20px;
    color: #EA1F35;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    line-height: 28px;
  }
  .ct1_c{
    font-family: 方正粗黑宋简体;
    font-size: 20px;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    line-height: 28px;
  }
  .textarea{
    width: 86%;
  }
  .submit_bt{
    width: 86%;
  }
  .sbt{
    float: right;
    text-align: center;
    padding: 5px 10px;
  }
  .stock_block{
    height: 40%;
    width: 80%;
  }
</style>
