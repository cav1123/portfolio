<template>
    <div class="outer-container">
        <main>
            <div class="main-container">
                <nav>
                    <ul class="breadcrumbs-list typo-label-xs">
                        <li><router-link to="/portfolio"><v-icon>mdi-home</v-icon></router-link></li>
                        <li>
                            <router-link
                                :to="{ name: 'portfolio', query: { selectedTaxonomy: work.categories[0].id, taxonomyName: work.categories[0].name, taxonomyType: 'isCategory' } }">{{
                                    work.categories[0].name }}</router-link>
                        </li>
                        <li><span>{{ work.title }}</span></li>
                    </ul>
                </nav>
                <article class="work-article">
                    <img :src="`${work.thumbnail.url}?q=100`" alt="">
                    <div class="work-contents-wrapper">
                        <h2 class="typo-heading-sm">{{ work.title }}</h2>
                        <ul class="category-nav-list">
                            <li v-for="category in work.categories" :key="category.id">
                                <router-link
                                    :to="{ name: 'portfolio', query: { selectedTaxonomy: category.id, taxonomyName: category.name, taxonomyType: 'isCategory' } }">
                                    <button class="category-nav-btn">
                                        <v-icon size="var(--typo-font-size-30)"
                                            color="var(--color-text-accent)">mdi-package-variant</v-icon>
                                        <span class="typo-label-sm">{{ category.name }}</span>
                                    </button>
                                </router-link>
                            </li>
                        </ul>
                        <ul class="tag-nav-list">
                            <li v-for="tag in work.tags" :key="tag.id">
                                <router-link
                                    :to="{ name: 'portfolio', query: { selectedTaxonomy: tag.id, taxonomyName: tag.name, taxonomyType: 'isTag' } }">
                                    <button class="tag-nav-btn">
                                        <v-icon size="var(--typo-font-size-20)"
                                            color="var(--color-text-default)">mdi-tag-outline</v-icon>
                                        <span class="typo-label-sm">{{ tag.name }}</span>
                                    </button>
                                </router-link>
                            </li>
                        </ul>
                        <p class="work-releasedAt typo-label-xs">
                            <v-icon size="var(--typo-font-size-20)"
                                color="var(--color-text-default)">mdi-update</v-icon>
                            <time datetime="">{{ new Date(work.releasedAt).toDateString() }}</time>
                        </p>
                        <div v-html="work.contents.html" class="work-contents"></div>
                    </div>
                </article>
            </div>
        </main>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'WorksDetailView',

    data: () => ({
        work: {
            thumbnail: {
                url: "",
            },
            contents: {
                html: ""
            },
            categories: [
                { name: "" }
            ],
            tags: [
                { name: "" }
            ],
        }
    }),

    async mounted() {
        const work = await axios.get('https://85hz3u9qwx.microcms.io/api/v1/works/' + this.$route.params.id, {
            headers: { "X-API-KEY": process.env.VUE_APP_XMicrocmsApiKey }
        })
        this.work = work.data
    },
}
</script>

<style scoped>
.outer-container {
    max-width: 75rem;
    margin: 0 auto;
}

.breadcrumbs-list {
    display: flex;
    align-items: center;
    gap: var(--spacing-xs);

    & li:not(:last-of-type) {
        display: flex;
        align-items: center;
        gap: var(--spacing-xxs);
        font-weight: var(--typo-font-weight-bold);

        &::after {
            content: ">";
        }
    }
}

.work-article {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xl);

    & img{
        border-radius: var(--border-radius-md);
    }

    & h2 {
        margin-bottom: var(--spacing-lg);
    }

    & .work-contents-wrapper {
        max-width: 40rem;
        width: 100%;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        gap: var(--spacing-xs);
    }

    & .category-nav-list {
        gap: var(--spacing-sm);
    }

    & .tag-nav-list {
        gap: var(--spacing-xxs);
    }

    & .work-contents {
        margin-top: var(--spacing-xl);
    }
}
</style>