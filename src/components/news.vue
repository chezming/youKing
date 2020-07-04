<template>
    <div class="main_content">
      <div class="topic" v-if="picktopic === 10">
        <div class="topic_title">新闻十大话题</div>
        <div class="topic_eng">main&nbsp;topics&nbsp;for&nbsp;news</div>
        <div class="topic_pics">
          <div class="t_pic" v-for="i in 10">
            <img class="t_img" v-bind:src="picsrc[i-1]"></img>
            <el-button type="info" @click="entertopic(i-1)">进入话题</el-button>
          </div>
        </div>
      </div>
      <div class="news_left" v-if="picktopic !== 10">
        <div class="news_div">
          <div class="backtopic" @click="backtopic()">&lt;back</div>
          <div class="news_list_title">NEWS</div>
          <ul class="news_ul">
            <li @click="changeNews(i+1)" v-for="(item,i) in news" :class="{active_new:(choose_news-1) === i}"><div class="news_li_con"><div class="news_li_t">{{item.title}}</div><div class="news_li_sub">{{item.content}}</div></div></li>
          </ul>
          <div class="nextP" v-if="currentpage <= total" @click="next">next&gt;</div>
          <div class="frontP" v-if="currentpage!==1" @click="front">&lt;front</div>
        </div>
      </div>
      <div class="news_right" v-if="picktopic !== 10">
        <div class="news_main">
          <div class="news_main_title" v-if="choose_news===0"><p class="t1">Main</p><p class="t2">News</p><div style="clear: both"></div></div>
          <div class="news_main_pic" v-if="choose_news===0">
            <div class="pic_top">
              <div class="pic_tl"></div>
              <div class="pic_tr">
                <div class="pic_trt"></div>
                <div class="pic_trb"></div>
              </div>
            </div>
            <div class="pic_bottom">
              <div class="pic_bl"></div>
              <div class="pic_br"></div>
            </div>
          </div>
          <div class="back" @click="back" v-if="choose_news!==0">&lt;返回</div>
          <div class="news_con_titlte" v-if="choose_news!==0">{{news[choose_news-1].title}}</div>
          <div class="news_mes" v-if="choose_news!==0"><div class="news_sor">{{news[choose_news-1].source}}</div><div class="labels"><div class="news_labels" v-for="(item,i) in labels">{{item}}</div><div style="clear: both"></div></div><div style="clear: both"></div><div class="news_time">{{news[choose_news-1].time}}</div></div>
          <div class="news_content" v-if="choose_news!==0">{{news[choose_news-1].content}}</div>
        </div>
      </div>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: "news",
        data() {
            return {
                news:[{
                    title: '',
                    source: '',
                    time: '',
                    content: '',
                    url: '',
                },{
                    title: '',
                    source: '',
                    time: '',
                    content: '',
                    url: '',
                },
                    {
                        title: '',
                        source: '',
                        time: '',
                        content: '',
                        url: '',
                    },
                    {
                        title: '',
                        source: '',
                        time: '',
                        content: '',
                        url: '',
                    },{
                        title: '',
                        source: '',
                        time: '',
                        content: '',
                        url: '',
                    }],
                choose_news: 0,
                currentpage: 1,
                total: null,
                link: 'http://localhost:8181',
                picktopic: 10,
                pics:[''],
                labels: [],
                picsrc:[
                    '../../static/news_img/word_cloud_0.jpg',
                    '../../static/news_img/word_cloud_1.jpg',
                    '../../static/news_img/word_cloud_2.jpg',
                    '../../static/news_img/word_cloud_3.jpg',
                    '../../static/news_img/word_cloud_4.jpg',
                    '../../static/news_img/word_cloud_5.jpg',
                    '../../static/news_img/word_cloud_6.jpg',
                    '../../static/news_img/word_cloud_7.jpg',
                    '../../static/news_img/word_cloud_8.jpg',
                    '../../static/news_img/word_cloud_9.jpg',
                ]
            }
        },
        components: {
            //someComponent
        },
        mounted() {
        },
        created(){
            this.getnews(1);
        },
        methods: {
            getnews(i){
                this.currentpage = i;
                axios.get(this.link+'/news_basis/findByOrder/'+this.picktopic+'f/'+this.currentpage+'/5').then(res=>{
                    this.news = res.data.content;
                    this.total = res.data.totalElements/5;
                    console.log(res);
                    console.log(this.total);
                })
            },
            changeNews(i){
                this.choose_news = i
                axios.get(this.link+'/news_content_keyword/findLabel/'+this.news[i-1].id).then(res=>{
                    console.log(res);
                    this.labels = res.data
                })
            },
            back(){
                this.choose_news = 0;
            },
            next(){
                this.currentpage++;
                this.getnews(this.currentpage);
            },
            front(){
                this.currentpage--;
                this.getnews(this.currentpage);
            },
            entertopic(i){
                this.picktopic = i;
                this.getnews(1);
            },
            backtopic(){
                this.picktopic = 10;
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
  .backtopic{
    font-family: 方正粗黑宋简体;
    font-size: 16px;
    color: #2A2E31;
    cursor: pointer;
    margin-left: 12%;
    margin-bottom: 10px;
  }
  .topic{
    width: 90%;
    height: 86%;
  }
  .topic_title{
    font-family: 方正粗黑宋简体;
    font-size: 36px;
    color: #2A2E31;
  }
  .topic_eng{
    font-family: 方正粗黑宋简体;
    font-size: 20px;
    color: #2A2E31;
  }
  .topic_pics{
    width: 100%;
    height: 90%;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-content: space-around;
  }
  .t_pic{
    margin-top: 20px;
    width: 19%;
    height: 40%;
    background-color: white;
    /*cursor: pointer;*/
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-radius: 10px;
  }
  .t_img{
    width: 98%;
    height: 60%;
    margin-bottom: 10px;
    overflow: hidden;
  }
  .news_div{
    height: 90%;
    width: 100%;
  }
  .news_list_title{
    font-size: 24px;
    /*font-weight: 600;*/
    color: #2A2E31;
    margin-left: 12%;
    font-family: 方正粗黑宋简体;
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
  .news_ul{
    width: 100%;
    height: 90%;
    margin-top: 10px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .news_ul li{
    width: 100%;
    height: 19%;
    background-color: rgba(255,255,255,0.5);
    cursor: pointer;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .news_li_con{
    width: 80%;
    height: 70%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .news_ul li:hover{
    background-color: rgba(255,255,255,1);
  }
  .news_li_t{
    font-size: 16px;
    width: 100%;
    color: rgba(0,0,0,0.6);
    font-weight: bold;
    font-family: 方正粗黑宋简体;
  }
  .news_li_sub{
    width: 100%;
    font-size: 12px;
    height: 32px;
    overflow: hidden;
    text-overflow: -o-ellipsis-lastline;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    line-clamp: 2;
    -webkit-box-orient: vertical;
    font-family: 华文细黑;
    color: rgba(0,0,0,0.6);
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
  .news_main_pic{
    width: 100%;
    height: 86%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .pic_top{
    height: 56%;
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
  .pic_tl{
    width: 66%;
    height: 100%;
    background-color: yellowgreen;
    border-radius: 10px;
    cursor: pointer;
  }
  .pic_tr{
    width: 32%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .pic_trt{
    width: 100%;
    height: 48%;
    background-color: yellowgreen;
    border-radius: 10px;
    cursor: pointer;
  }
  .pic_trb{
    width: 100%;
    height: 48%;
    background-color: yellowgreen;
    border-radius: 10px;
    cursor: pointer;
  }
  .pic_bottom{
    width: 100%;
    height: 42%;
    display: flex;
    justify-content: space-between;
  }
  .pic_bl{
    width: 26%;
    height: 100%;
    background-color: yellowgreen;
    border-radius: 10px;
    cursor: pointer;
  }
  .pic_br{
    width: 72%;
    height: 100%;
    background-color: yellowgreen;
    border-radius: 10px;
    cursor: pointer;
  }
  .news_con_titlte{
    font-family: 方正粗黑宋简体;
    font-size: 40px;
    width: 60%;
  }
  .news_sor{
    font-family: 方正粗黑宋简体;
    font-size: 20px;
    color: #6d767d;
    margin-top: 20px;
    float: left;
  }
  .labels{
    float: right;
  }
  .news_labels{
    font-family: 方正粗黑宋简体;
    float: left;
    font-size: 20px;
    color: #6d767d;
    margin-top: 20px;
    margin-left: 5px;
  }
  .news_time{
    font-family: 方正粗黑宋简体;
    font-size: 20px;
    color: #6d767d;
    margin-top: 5px;
  }
  .news_content{
    width: 100%;
    height: 60%;
    overflow-x: auto;
    font-size: 16px;
    line-height: 24px;
    font-family: 方正粗黑宋简体;
    margin-top: 40px;
    font-weight: lighter;
    color: rgba(0,0,0,0.6);
  }
  .news_content::-webkit-scrollbar{
    width:10px;
    height:10px;
    /**/
  }
  .news_content::-webkit-scrollbar-track{
    background: rgb(239, 239, 239);
    border-radius:2px;
  }
  .news_content::-webkit-scrollbar-thumb{
    background: #6D767D!important;
    border-radius:10px!important;
  }
  .news_content::-webkit-scrollbar-thumb:hover{
    background: #333;
  }
  .news_content::-webkit-scrollbar-corner{
    background: #179a16;
  }
  .back{
    font-family: 方正粗黑宋简体;
    font-size: 16px;
    color: #6d767d;
    cursor: pointer;
    margin-bottom: 5px;
  }
  .back:hover{
    color: #2A2E31;
  }
  .active_new{
    background-color: white!important;
  }
  .active_new .news_li_con .news_li_t{
    color: #2A2E31!important;
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
</style>
