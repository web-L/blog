<template>
  <section>
    <div class="jztop"></div>
    <slideNav :slideState="slideNavState"></slideNav>
    <transition name="fade-mask">
      <div class="slide-mask" v-if="slideNavState" @click="showSlideNav"></div>
    </transition>
    <div :class="[slideNavState ? 'artiveSlide' : 'closeSlide']">
      <transition name="fade" :mode="trasitionMode"><router-view/></transition>
    </div>
    <Back-top></Back-top>
    <div v-if="!slideNavState" class="slide-menu" @click="showSlideNav"><Icon type="navicon"></Icon></div>
    <div class="jzend"></div>
  </section>
</template>

<script>
import slideNav from '@/components/common/slide-nav.vue'
import { mapState } from "vuex";

export default {
  name: 'v-main',
  data(){
    return {
      trasitionMode: 'out-in'
    }
  },
  created(){
    document.body.onresize = () => {
      let w = window.innerWidth || document.documentElement.clientWidth || document.body.clientWidth;
      this.trasitionMode = w > 768 ? 'out-in' : 'in-out';
    }
  },
  components: {
    slideNav,
  },
  methods: {
    showSlideNav(){
      this.$store.commit('updateSlideNavState');
    }
  },
  computed: {
    ...mapState([
      'slideNavState'
    ])
  }
}
</script>
<style>
  .ivu-back-top-inner{
    border-radius: 50% !important;
    background: #5b5b5b !important;

  }
  .ivu-back-top-inner i {
      color: #fff !important;
      font-size: 20px !important;
      padding: 8px 9px !important;
  }
  
  .fade-mask-enter-active, .fade-mask-leave-active {
    transition: all .8s;
  }
  .fade-mask-enter, .fade-mask-leave-to {
    opacity: 0;
  }
  .fade-mask-leave-to {
    left: 0;
  }
</style>
