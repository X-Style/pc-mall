<template>
    <!-- 主信息 -->
      <div  class="funcTab" :class="showNavTop ? 'funcTab-fixed' : ''">
        <div class="row" style="height: 100%;">
          <!-- logo -->
          <router-link to="/" v-show="!showNavTop" class="tabLogo funcTabFixed-hide">
            <i class="logo"></i>
          </router-link>
          <!-- 小Logo -->
          <router-link to="/" v-show="showNavTop" class="tabLogo-fixed">
            <i class="logo"></i>
          </router-link>
          <!-- cart -->
          <div v-show="!showNavTop" class="cartEnterWrap">
            <router-link to="/cart" class="cartEnter">
              <i class="icon icon-gouwuche"></i>
              <span class="cartName">购物车</span>
              <i class="cat-badge cart-num">0</i>
            </router-link>
          </div>
          <!-- nav -->
          <ul class="tabNav">
            <li class="tabNav-item">
              <router-link to="/" class="topLevel">首页</router-link>
            </li>
            <li class="tabNav-item" :class="index == tabNav.length-1 ? 'last' :''" v-for="(item,index) in tabNav" :key='index' >
              <router-link :to="'/categoryList?id='" class="topLevel" >{{item.text}}</router-link>
                <div class="tabNav-dropdown"  >
                  <ul class="cateGroupList">
                    <div class="cateGroup" v-for="(itema,indexa) in item.navList" :key='indexa'>
                      <div class="cateGroup-name">{{itema.title}}</div>
                      <div class="columnList">
                        <div class="cateColumn">
                          <div class="cateItem" v-for="(itemb,indexb) in itema.list" :key='indexb'>
                            <router-link :to="'/categoryList'">
                              <img :src="itemb.img" class="subCate-icon" :alt="itemb.text" />
                              <span class="subCate-text">{{itemb.text}}</span>
                            </router-link>
                          </div>
                        </div>
                      </div>
                    </div>
                  </ul>
                </div>
            </li>
            <!-- <li v-show="!showNavTop" class="tabNav-item">
              <a href="" class="topLevel">为你严选</a>
            </li>
            <li v-show="!showNavTop" class="tabNav-item">
              <a href="" class="topLevel">众筹</a>
            </li> -->
          </ul>
          <!-- search -->
          <div v-show="!showNavTop" class="search">
            <div class="searchInputWrap">
              <i class="search-gray icon icon-search"></i>
              <input type="text" @input="search" class="searchInput" autocomplete="off" maxlength="100" name="searchInput">
              <div class="searchDefaultKeyword" v-show="isShowInfo">{{searchValue}}</div>
            </div>
            <div @click="handleSearch" class="searchButton">
              <span class="searchButtonName">搜索</span>
            </div>
            <div class="hotKeywordListWrap">
              <div class="hotKeywordList">
                <div class="hotKeywordRow">
                  <div @click="handleHot(item)" class="hotKeyword " v-for="(item,index) in hotSearch" :key="index">{{item}}</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
</template>

<script>
export default {
  name: 'MyTop',
  data(){
    return{
      
      showNavTop:false,
      // search
      isShowInfo:true,
      searchValue:'热卖 按摩电器',
      tabNav:[
        {text:'居家生活',url:''
          ,navList:[
            {title:'秋冬好物',list:[
              {text:'秋冬好物',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'主题床品',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'北欧原木',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'餐厨系列',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'秋冬好物',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'秋冬好物',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'秋冬好物',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
            ]},
            {title:'床上用品',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'家居饰品',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'家具安装',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'收纳日用',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'厨房用品',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'餐具水具',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'宠物生活',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
            ]},
          ]
        },
        {text:'服饰鞋包',url:''
          ,navList:[
            {title:'秋冬好物',list:[
              {text:'秋冬好物',url:'',img:'https://yanxuan.nosdn.127.net/d0d518823ba987d6f7b38865ff4f4acc.png?&quality=95&type=webp&imageView',},
              {text:'主题床品',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'北欧原木',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'餐厨系列',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'秋冬好物',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'秋冬好物',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'秋冬好物',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
            ]},
            {title:'床上用品',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'家居饰品',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'家具安装',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'收纳日用',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'厨房用品',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'餐具水具',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              
            ]},
            {title:'宠物生活',list:[
              {text:'床品件套',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'被遮盖谈',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
              {text:'床垫床褥',url:'',img:'https://yanxuan.nosdn.127.net/e48caa07a8ba179f542f428102cb7b71.png?&quality=95&type=webp&imageView',},
            ]},
          ]
        },
        {text:'美食酒水',url:''},
        {text:'个护清洁',url:''},
        {text:'母婴亲子',url:''},
        {text:'运动旅行',url:''},
        {text:'数码家电',url:''},
        {text:'全球特色',url:''},
      ],
      hotSearch:[
        '山羊绒围巾8折','回馈金卡买11得33','保温杯 限时7折','即溶咖啡 直降54'
      ]
    }
  },
  mounted(){
    window.addEventListener('scroll', this.handleScroll);
  },
  methods:{
    // 搜索框
    search(e){
      let value = e.target.value;
      this.searchValue = value;
      this.isShowInfo = value == '' ? true : false;
    },
    handleHot(e){
      this.searchValue = e;
      this.handleSearch();
    },
    // 点击搜索
    handleSearch(){
      this.$router.push(`/search?keyword=${this.searchValue}`)
    },
    handleScroll() {
      let top = document.documentElement.scrollTop;
      let showNavTopNum = 120;
      this.showNavTop = top >= showNavTopNum ? true : false;
    },
  },
  destroyed() {
    window.removeEventListener('scroll', this.handleScroll);
  }
}

</script>

<style lang="scss">
    // 主信息
    .funcTab{
      position: relative;
      height: 140px;
      background-color: #fff;
      box-shadow: 0 0 3px 0 rgba(0,0,0,.2);
      .tabLogo {
        position: absolute;
        top: 24px;
        left: 0;
        // logo
        .logo{
          font-style: normal;
          background-position: 0 -202px;
          height: 60px;
          width: 124px;
          display: block;
          background-image: -webkit-image-set(url(../../assets/img/iconMore.png) 2x);
        }
      }
      // cart
      .cartEnterWrap {
          position: relative;
          margin-top: 26px;
          margin-left: 49px;
          float: right;
          z-index: 4;
          border-radius: 19px;
          &:hover {
            background-color: #F5F3EF;
          }
          .cartEnter {
            display: inline-block;
            position: relative;
            cursor: pointer;
            width: 134px;
            height: 38px;
            border: 1px solid #B4A078;
            border-radius: 19px;
            padding: 8px 0;
            box-sizing: border-box;
            .icon{
              margin-left: 22px;
              font-size: 18px;
              background-position: 0 -114px;
              height: 18px;
              width: 18px;
            }
            .cartName{
              color: #B4A078;
              margin-left: 5px;
              margin-top: -1px;
              font-size: 14px;
            }
            .cart-num{
              margin-left: 10px;
              margin-top: -1px;
              color: #fff;
              text-align: center;
              line-height: 20px;
              z-index: 1;
              background-color: red;
              font-style: inherit;
              text-align: center;
              border-radius: 50%;
              display: inline-block;
              width: 20px;
              height: 20px;
            }
          }
      }
      // tabNav
      .tabNav{
        line-height: 1;
        font-weight: 700;
        position: absolute;
        height: 30px;
        line-height: 30px;
        bottom: 9px;
        width: 100%;
        .tabNav-item:hover .tabNav-dropdown{
          display: block;
        }
        .tabNav-item {
          float: left;
          
          margin: 0 26px;
          font-size: 14px;
          &:hover .topLevel{
              color: #b4a078;
              border-bottom: 3px solid #b4a078;
            }
          
          &:nth-child(1){
            margin-left: 0;
            margin-left: 0;
          }
          &:last-child{
            margin-right: 0;
          }
          .topLevel{
            display: block;
            padding-bottom: 7px;
            color: #000;
           
          }
          // ...
          .tabNav-dropdown{
            display: none;
            position: absolute;
            top: 39px;
            background-color: transparent;
            width: 1202px;
            left: -56px;
            right: auto;
            .cateGroupList{
              display: flex;
              height: 100%;
              padding: 14px 20px 20px;
              background: #fff;
              border: 1px solid rgba(0,0,0,.1);
              .cateGroup{
                float: left;
                margin-right: 24px;
                width: 124px;
                &:last-child{
                  margin-right:0;
                }
                .cateGroup-name{
                  display: inline-block;
                  margin-bottom: 10px;
                  font-size: 16px;
                  font-weight: 700;
                  line-height: 36px;
                  border-bottom: 1px solid #ddd;
                  max-width: 124px;
                  width: 124px;
                }
                .columnList{
                  .cateColumn{
                    float: left;
                    width: 124px;
                    margin-left: 24px;
                    &:first-child{
                      margin-left: 0;
                    }
                    .cateItem{
                      margin-bottom: 4px;
                      font-weight: 400;
                      line-height: 50px;
                      a{
                        display: inline-block;
                      }
                      .subCate-icon{
                        height: 50px;
                        width: 50px;
                        display: inline-block;
                        float: left;
                      }
                      .subCate-text{
                        display: inline-block;
                        width: 70px;
                        max-width: 70px;
                        max-height: 48px;
                        margin-left: 4px;
                        font-size: 14px;
                        vertical-align: middle;
                        line-height: 1.2;
                        overflow: hidden;
                        word-wrap: break-word;
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
      // search
      .search{
        z-index: 3;
        position: relative;
        margin-top: 26px;
        float: right;
        width: 532px;
        height: 36px;
        .searchInputWrap{

          .search-gray{
            font-size: 14px;
            background-position: 0 -312px;
            height: 14px;
            width: 14px;
            position: absolute;
            left: 18px;
            top: 12px;
          }
          .searchInput{
            position: absolute;
            box-sizing: border-box;
            left: 0;
            top: 0;
            z-index: 1;
            display: block;
            height: 38px;
            line-height: 38px;
            padding-top: 2px;
            padding-bottom: 2px;
            border: 1px solid #B4A078;
            border-bottom-left-radius: 19px;
            border-top-left-radius: 19px;
            font-size: 14px;
            width: 442px;
            padding-left: 38px;
            outline: 0;
            overflow: hidden;
            background: 0 0;
          }
          .searchDefaultKeyword{
            position: absolute;
            top: 12px;
            left: 38px;
            color: #999;
            display: block;
            line-height: 1;
            cursor: text;
            touch-action: none;
            -ms-touch-action: none;
            pointer-events: none;
            -ms-pointer-events: none;
            -webkit-user-select: none;
            white-space: nowrap;
            overflow: hidden;
            width: 390px;
            text-overflow: ellipsis;
            font-size: 14px;
          }
        }
        .searchButton{
          width: 90px;
          height: 38px;
          background-color: #B4A078;
          border-top-right-radius: 19px;
          border-bottom-right-radius: 19px;
          cursor: pointer;
          float: right;
          color: #fff;
          line-height: 38px;
          text-align: center;
          font-size: 16px;
          letter-spacing: 1px;
          box-sizing: border-box;
        }
        .hotKeywordListWrap{
          margin-top: 46px;
          margin-left: 8px;
          width: 444px;
          height: 18px;
          overflow: hidden;
          .hotKeywordList{
            position: relative;
            overflow: hidden;
            top:0;
            .hotKeywordRow{
              height: 18px;
              line-height: 18px;
              margin-bottom: 18px;
              font-size: 0;
              .hotKeyword {
                display: inline-block;
                color: #999;
                padding: 0 10px;
                border-right: 1px solid #ccc;
                cursor: pointer;
                line-height: 12px;
                text-overflow: ellipsis;
                overflow: hidden;
                white-space: nowrap;
                max-width: 444px;
                font-size: 12px;
                &:last-child{
                  border-right: 0;
                }
              }
            }
          }
        }
      }
    }
    
    .funcTab-fixed {
      z-index: 9;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 50px!important;
      animation: hdnav2-show .3s;
      .tabLogo-fixed {
        position: absolute;
        top: 12px;
        left: 5px;
        z-index: 1;
        
        i{
          background-image: -webkit-image-set(url(../../assets/img/iconMore.png) 2x);
          background-position: 0 -272px;
          height: 30px;
          width: 90px;
          display: block;
        }
      }
      
      .tabNav {
        display: block;
        top: 11px;
        left: 126px;
        bottom: auto;
        width: 892px;
        .tabNav-item{
          .tabNav-dropdown{
            top: 39px;
            left:-182px
          }
          &.last{
            margin-right: 0;
          }
        }
      }
    }

    @keyframes hdnav2-show {
      0% {
          top: -42px;
      }
      100%{
         top: 0px;
      }
    }
      
</style>