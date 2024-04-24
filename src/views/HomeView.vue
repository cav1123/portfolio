<template>
  <div>
    <v-row>
      <v-col v-for="work in works" :key="work.id">
        <v-card>
          <v-img src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"></v-img>
          <v-card-title>{{work.title}}</v-card-title>
          <v-card-text>
            <div>{{work.id}}</div>
            <div>Whitsunday Island, Whitsunday Islands</div>
          </v-card-text>
          <v-card-action>
            <router-link :to="{name:'works-detail',params:{id:work.id}}">
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
    works: []
  }),

  async mounted() {
    const response = await axios.get('https://85hz3u9qwx.microcms.io/api/v1/work', {
      headers: { "X-API-KEY": process.env.VUE_APP_XMicrocmsApiKey }
    })
    this.works = response.data.contents
  }
}
</script>
