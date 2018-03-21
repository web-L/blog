<template>
  <div class="index">
    <div class="container relative display-flex flex-justify-content">
      <div class="left-wrap">
        <ArticleList :topTitle="title" :pageRouter="'page'" :listdata="articleLists.news.data" :totalPage="articleLists.news.total" :currentPage="articleLists.news.page"></ArticleList>
        <Spin size="large" fix v-if="spinShow"></Spin>
      </div>
      <indexRight></indexRight>
    </div>
  </div>
</template>

<script>
import ArticleList from '@/components/common/article-list.vue';
import indexRight from '@/components/common/index-right.vue';
import { mapState } from "vuex";

export default {
  name: 'index',
  data: () => {
    return {
      title: "最新文章",
      spinShow: true,
    }
  },
  mounted(){
    let store =  this.$store;
    Promise.all([
      store.dispatch('getHotArticleData',{limit:5,field:'click',order: 'desc'}),
      store.dispatch('getRecommendArticleData',{limit:10,tag:'推荐'}),
      store.dispatch('getNewsArticleData',{limit:10,offset: this.$route.params.id||1 }),
      store.dispatch('getCategoryData'),
    ]).then(() => {
      this.$store.commit('updateMetaTitle','首页');
      this.spinShow = false;
    });
  },
  computed: {
    ...mapState([
      'articleLists',
      'categoryData'
    ]),
  },
  components: {
    ArticleList,
    indexRight
  },
  watch: {
    '$route': 'fetchPageData'
  },
  methods: {
    fetchPageData(){
      this.spinShow = true;
      this.$store.dispatch('getNewsArticleData',{
        limit:10,
        offset: this.$route.params.id
      }).then( () => {
        this.spinShow = false;
      });
    },
  }
}
</script>
