<template>
  <div class="side-wrap" :class="[slideNavState ? 'artiveSlide' : 'closeSlide']" >
      <div class="head">Ali</div>
      <Alert show-icon>
          <Icon type="ios-lightbulb-outline" slot="icon"></Icon>
          <template slot="desc">没有人不爱惜他的生命，但很少人珍惜他时间。</template>
      </Alert>
      <nav>
        <div  class="navigation">
          <Menu mode="vertical" class="nav" theme="light" active-name="1" top-title  @on-select="curNav">
              <Menu-item :name="item.name" v-for="item in nav.data" :key="item.id" ><router-link :to="item.url">{{ item.name }}</router-link></Menu-item>
          </Menu>
        </div>
      </nav>
      <Footer></Footer>
    </div>
</template>

<script>
import { mapState } from "vuex";
import Footer from '@/components/common/footer.vue'

export default {
  name: 'slideNav',
  methods:{
    curNav(name){
      this.$store.commit('updateMetaTitle',name);
      this.$store.commit('updateSlideNavState');
    }
  },
  components:{
    Footer,
  },
  computed: {
    ...mapState([
      'nav',
      'slideNavState'
    ])
  }
}
</script>
<style>
  .side-wrap{
    position: fixed;
    top: 0;
    left: -264px;
    width: 264px;
    background: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1521476956362&di=7608ae7f689fd6c6ce11bc405c43276b&imgtype=0&src=http%3A%2F%2Fd.hiphotos.baidu.com%2Fzhidao%2Fpic%2Fitem%2F30adcbef76094b36c78d2656a1cc7cd98d109d69.jpg) no-repeat center/cover;
    height: 100%;
    z-index: 10;
  }
  .side-wrap::after{
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, .6);
    z-index: -1;
  }
  .side-wrap .head{
    width: 86px;
    height: 86px;
    line-height: 80px;
    margin: 30px auto 0;
    border: 1px solid #fff;
    text-align: center;
    font-size: 36px;
    color: #fff;
    border-radius: 50%;
  }
  .side-wrap .ivu-alert-info{
    background: none;
    border: none;
  }
  .side-wrap .ivu-alert-desc{
    color: #fff;
  }
  .side-wrap .ivu-menu-light,.side-wrap .navigation,.side-wrap .ivu-menu-item:hover{
    background: none !important;
  }
   .side-wrap .ivu-menu-vertical .ivu-menu-item a{
     color: #fff;
     display: block;
   }
   .side-wrap .ivu-menu-vertical.ivu-menu-light:after{
     display: none;
   }
    .side-wrap .ivu-menu-light.ivu-menu-vertical .ivu-menu-item-active:not(.ivu-menu-submenu){
      border-color: #fff;
      background: none;
    }
    .side-wrap .ivu-menu-light{
      width: 100% !important;
    }
    .side-wrap nav{
      width: 100%;
      position: absolute;
      bottom: 64px;
      left: 0;
    }
    
    .side-wrap .ivu-menu-vertical .ivu-menu-item{
      padding: 14px 26px;
    }
  .side-wrap .navigation{
    height: auto;
  }
  .side-wrap footer{
    position: absolute;
    bottom: 0;
    left: 0;
    display: block;
    padding: 8px 0;
    margin: 0;
  }
</style>
