<template>
  <div id="app">
    <Header></Header>
    <Main></Main>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from '@/components/common/head.vue'
import Footer from '@/components/common/footer.vue'
import Main from '@/components/common/main.vue'

export default {
  name: 'app',
  components: {
    Header,
    Footer,
    Main,
  },
}
</script>
