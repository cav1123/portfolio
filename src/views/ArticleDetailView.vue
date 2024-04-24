<template>
    <v-card>
        <v-img src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"></v-img>
        <v-card-title>{{ article.title }}</v-card-title>
        <v-card-text>
            <div>Whitehaven Beach</div>
            <div>Whitsunday Island, Whitsunday Islands</div>
        </v-card-text>
    </v-card>
</template>

<script>
import axios from 'axios'

export default {
    name: 'ArticleDetailView',
    data: () => ({
        article: {}
    }),
    async mounted() {
        const response = await axios.get('https://85hz3u9qwx.microcms.io/api/v1/work/' + this.$route.params.id, {
            headers: { "X-API-KEY": process.env.VUE_APP_XMicrocmsApiKey }
        })
        this.article = response.data
    }
}
</script>