<template>
  <div>
    <h1>{{ article.title }}</h1>

    <p>
      {{ article.content }}
    </p>
    <!-- Article Edit/Delete UI -->
    <div v-if="isAuthor">
      <router-link :to="{ name: 'articleEdit', params: { articlePk: article.pk} }">
        <button>Edit</button>
      </router-link> | 
      <button @click="deleteArticle({ articlePk: article.pk })">Delete</button>
    </div>

    <!-- Article Like UI -->
    <div>
      Likeit: <button @click="likeArticle({ articlePk: article.pk })">{{ like_count }}</button>
    </div>
    
    <hr>
    <!-- Comment UI -->
    <comment-list :comments="article.comments"></comment-list>
  </div>
</template>

<script>
import CommentList from '@/components/CommentList.vue'

import { mapGetters, mapActions } from 'vuex'


export default {
  name: 'ArticleDetail',
  components: { CommentList },
  data() {
    return {
      articlePk: this.$route.params.articlePk
    }
  },
  computed: {
    ...mapGetters(['article', 'currentUser', 'isAuthor']),
    like_count() {
      // return article.like_users ? this.article.like_users.length : undefined
      return this.article.like_users?.length
    },
  },
  methods: {
    ...mapActions(['fetchArticle', 'likeArticle', 'deleteArticle'])
  },
  created() {
    this.fetchArticle({ articlePk: this.articlePk })
  },
}
</script>

<style>

</style>