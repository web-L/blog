<template>
  <div class="side-wrap" :class="[slideNavState ? 'artiveSlide' : 'closeSlide']" :style="slideBg">
      <div class="head">Ali</div>
      <Alert show-icon>
          <Icon type="ios-lightbulb-outline" slot="icon"></Icon>
          <template slot="desc">{{tips}}</template>
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
  data(){
    return {
      tips: '',
      slideBg: {
        'background-image': ''
      }
    }
  },
  methods:{
    curNav(name){
      this.$store.commit('updateMetaTitle',name);
      this.$store.commit('updateSlideNavState');
    }
  },
  components:{
    Footer,
  },
  watch: {
    slideNavState(){
      document.body.style.overflow = this.slideNavState ? 'hidden':'auto';
      if(this.slideNavState){
        this.tips = this.slideTips[parseInt(Math.random()*this.slideTips.length) % this.slideTips.length];
        this.slideBg['background-image'] = `url(${this.$http.defaults.baseURL}/public/www/slide-bg/${parseInt(Math.random()*8) % 8}.png)`;
      }
    }
  },
  computed: {
    ...mapState([
      'nav',
      'slideNavState',
      'slideTips'
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
    background:#636363 url(../../assets/images/slide-bg/0.png) no-repeat center/cover;
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
    background: none;
  }
</style>
