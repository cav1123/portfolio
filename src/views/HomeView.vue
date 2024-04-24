<template>
  <div>
    <v-row>
      <v-col v-for="article in articles" :key="article.id">
        <v-card>
          <v-img src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"></v-img>
          <v-card-title>{{article.title}}</v-card-title>
          <v-card-text>
            <div>{{article.id}}</div>
            <div>Whitsunday Island, Whitsunday Islands</div>
          </v-card-text>
          <v-card-action>
            <router-link :to="{name:'article-detail',params:{id:article.id}}">
              <v-btn>More</v-btn>
            </router-link>
          </v-card-action>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
// import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'HomeView',
  // components: {
  //   HelloWorld
  // }
  data: () => ({
    articles: []
  }),

  async mounted() {
    const response = await axios.get('https://85hz3u9qwx.microcms.io/api/v1/work', {
      headers: { "X-API-KEY": process.env.VUE_APP_XMicrocmsApiKey }
    })
    this.articles = response.data.contents
  }
}
</script>
