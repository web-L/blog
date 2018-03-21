<template>
    <div class="bloglist">
        <Menu mode="horizontal" class="top-title" theme="light" active-name="1" top-title>
            <Menu-item name="1"><Icon type="paper-airplane"></Icon>{{ topTitle }}</Menu-item>
        </Menu>
        <section class="article-items">
            <article v-for="(item,index) in listdata" :key="index">
              <figure>
                  <router-link :to="/details/+item.id"><img :src="$http.defaults.baseURL+item.thumbnail" width="150" height="114" :alt="item.title"></router-link>
              </figure>
              <section>
                <h3><router-link :to="/details/+item.id">{{item.title}}</router-link></h3>
                <div class="info">
                    <p class="abstract">{{ item.abstract }}</p>
                    <p class="autor">
                      <span class="lm " v-if="isNaN(parseInt(item.category))">
                        <Icon type="ios-pricetags"></Icon>&nbsp
                        <router-link :to="`/article/${item.category.pinpy}__${item.category.id}`">{{ item.category.name }}</router-link>
                      </span>
                      <span class="dtime "><Icon type="clock"></Icon>&nbsp{{ item.create_time | dateFilter }}</span>
                      <span class="viewnum "><Icon type="eye"></Icon>&nbsp浏览（{{ item.click }}）</span>
                      <!-- <span class="pingl f_r"><Icon type="chatbubble"></Icon>&nbsp评论（30）</span> -->
                    </p>
                </div>
              </section>
            </article>
        </section>
        <Page v-if="totalPage > 10" :total="totalPage" :current="currentPage" size="small" class="paging" @on-change="pageChange"></Page>
    </div>
</template>

<script>
export default {
  name: 'articleList',
  props: ["listdata",'topTitle','currentPage','totalPage','pageRouter'],
  methods: {
    pageChange( current ){
      this.$router.push({name: this.pageRouter, params: { id: current }});
    }
  },
  
}
</script>
<style lang="scss" scoped="">
  .top-title{
    background: none;
    height: 46px;
    border-bottom: 1px solid #d2d2d2;
    margin-left: 16px;
    z-index: 7;

    .ivu-menu-item,.ivu-menu-item:hover{
      line-height: auto!important;
      color: #090e08 !important;
      border-color:#090e08 !important; 
      background: none;
      font-size: 16px;
      font-weight: bold;
    }
   
  }
  
  /*文章*/
  .bloglist {
    width: 100%;
    overflow: hidden;
    padding-right: 18px;
    figure{
      float: left;
        margin-right: 10px;
        overflow: hidden;
        padding: 4px;
        border: #f4f2f2 1px solid;

        img{
            transition:transform 1.2s;
        }
    }

    .article-items{
      line-height: 20px;

      article{
        position: relative;
        border-bottom: 1px solid #d2d2d2;
        padding: 7px;
        padding-bottom: 16px;
        margin-top: 10px;
        margin-left: 10px;
        transition: background .8s;


        .info{
          overflow: hidden;
        }

        h3{
            padding: 8px 0;
            color: #333;
            font-size: 16px;
            font-family: "微软雅黑";
            a{
              color: #070c06;
            }
        }
       
        h3 a:hover,.rank li a:hover{
          color: #627174;
        }
      }

      article:hover {
        transition: background .8s;
        background:#f7f5f5;
      }

      article:hover .readmore{
        transition: border-radius .8s;
        border-radius:8px;
      }

      figure:hover img{
        transition:transform 1.2s;
        transform: scale(1.08);
      }

    }

    .abstract{
      height: 58px;
      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 4;
      overflow: hidden;
    }
    .autor {
      margin-top: 6px;

      span {
        padding-right: 20px;

        a {
          color: #759b08;
         
          &:hover {
            text-decoration: underline
          }
        }
      }
    }
  }

</style>
