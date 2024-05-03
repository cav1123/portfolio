<template>
  <div class="outer-container">
    <aside>
      <nav class="nav-container">
        <!-- <v-btn @click="showAllWorks">ALL{{ works.length }}</v-btn> -->
        <ul class="category-nav-list">
          <li v-for="category in categories" :key="category.id">
            <button @click="filterWorks(category.id, category.name, 'isCategory')" class="category-nav-btn">
              <v-icon size="var(--typo-font-size-30)" color="var(--color-text-accent)">mdi-package-variant</v-icon><span
                class="typo-label-md">{{
                  category.name }}</span><span class="category-reg-num typo-label-xs">{{
                  category.reg_num }}</span>
            </button>
          </li>
        </ul>
        <ul class="tag-nav-list">
          <li v-for="tag in tags" :key="tag.id">
            <button @click="filterWorks(tag.id, tag.name, 'isTag')" class="tag-nav-btn">
              <v-icon size="var(--typo-font-size-20)" color="var(--color-text-default)">mdi-tag-outline</v-icon><span
                class="typo-label-sm">{{ tag.name }}</span><span class="category-reg-num typo-label-xs">{{ tag.reg_num
                }}</span>
            </button>
          </li>
        </ul>
      </nav>
    </aside>
    <main>
      <div class="main-container">
        <h2 class="typo-heading-sm">{{ selectedTaxonomyName }}</h2>
        <ul class="work-list">
          <li v-for="work in filteredWorks" :key="work.id">
            <article class="work-articles">
              <router-link :to="{ name: 'works-detail', params: { id: work.id } }">
                <img :src="work.thumbnail.url" alt="" class="work-thumbnail">
                <h3 class="typo-heading-xs">{{ work.title }}</h3>
              </router-link>
              <ul class="category-nav-list">
                <li v-for="category in work.categories" :key="category.id">
                  <button @click="filterWorks(category.id, category.name, 'isCategory')" class="category-nav-btn">
                    <v-icon size="var(--typo-font-size-30)"
                      color="var(--color-text-accent)">mdi-package-variant</v-icon><span class="typo-label-sm">{{
                        category.name }}</span>
                  </button>
                </li>
              </ul>
              <ul class="tag-nav-list">
                <li v-for="tag in work.tags" :key="tag.id">
                  <button @click="filterWorks(tag.id, tag.name, 'isTag')" class="tag-nav-btn">
                    <v-icon size="var(--typo-font-size-20)"
                      color="var(--color-text-default)">mdi-tag-outline</v-icon><span class="typo-label-sm">{{ tag.name
                      }}</span>
                  </button>
                </li>
              </ul>
              <p class="work-releasedAt typo-label-xs">
                <v-icon size="var(--typo-font-size-20)" color="var(--color-text-default)">mdi-update</v-icon>
                <time datetime="">{{ new Date(work.releasedAt).toDateString() }}</time>
              </p>
            </article>
          </li>
        </ul>
      </div>
    </main>
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
    works: [],
    categories: [],
    tags: [],
    worksIndexes: [],
    selectedTaxonomyName: "",
  }),

  computed: {
    // 絞り込まれたWORKSデータ
    filteredWorks() {
      return this.works.filter((_, index) => {
        return this.worksIndexes.includes(index)
      })
    }
  },

  async mounted() {
    // WORKSデータ取得
    const works = await axios.get('https://85hz3u9qwx.microcms.io/api/v1/works?fields=id,title,thumbnail,categories,tags,releasedAt&limit=100', {
      headers: { "X-API-KEY": process.env.VUE_APP_XMicrocmsApiKey }
    })
    this.works = works.data.contents
    // CATEGORIESデータ取得
    const categories = await axios.get('https://85hz3u9qwx.microcms.io/api/v1/categories?fields=id,name,reg_num', {
      headers: { "X-API-KEY": process.env.VUE_APP_XMicrocmsApiKey },
    })
    this.categories = categories.data.contents
    // TAGSデータ取得
    const tags = await axios.get('https://85hz3u9qwx.microcms.io/api/v1/tags?fields=id,name,reg_num&limit=100', {
      headers: { "X-API-KEY": process.env.VUE_APP_XMicrocmsApiKey },
    })
    this.tags = tags.data.contents
    // WORKS表示
    if (this.$route.query.selectedTaxonomy) {
      this.filterWorks(this.$route.query.selectedTaxonomy, this.$route.query.taxonomyName, this.$route.query.taxonomyType)
    } else {
      this.showAllWorks()
    }
    // タクソノミー登録数カウント初期化
    this.countTaxonomyRegNum()
  },

  methods: {
    // WORKS全件表示
    showAllWorks() {
      this.worksIndexes = [...Array(this.works.length)].map((_, index) => index)
    },
    // WORKS絞り込み
    filterWorks(selectedTaxonomyId, selectedTaxonomyName, taxonomyType) {
      this.selectedTaxonomyName = selectedTaxonomyName
      this.worksIndexes = []
      for (let i = 0; i < this.works.length; i++) {
        const work = this.works[i];
        switch (taxonomyType) {
          case 'isCategory':
            for (let j = 0; j < work.categories.length; j++) {
              const category = work.categories[j].id;
              if (category === selectedTaxonomyId) {
                this.worksIndexes[i] = i
              }
            }
            break;
          case 'isTag':
            for (let j = 0; j < work.tags.length; j++) {
              const tag = work.tags[j].id;
              if (tag === selectedTaxonomyId) {
                this.worksIndexes[i] = i
              }
            }
            break;
          default:
            break;
        }
      }
    },
    // タクソノミー登録数カウント
    countTaxonomyRegNum() {
      for (let i = 0; i < this.works.length; i++) {
        const work = this.works[i];

        // カテゴリーカウント
        for (let j = 0; j < work.categories.length; j++) {
          const category = work.categories[j].id;
          for (let k = 0; k < this.categories.length; k++) {
            if (this.categories[k].id === category) {
              this.categories[k].reg_num++
            }
          }
        }
        // タグカウント
        for (let j = 0; j < work.tags.length; j++) {
          const tag = work.tags[j].id;
          for (let k = 0; k < this.tags.length; k++) {
            if (this.tags[k].id === tag) {
              this.tags[k].reg_num++
            }
          }
        }
      }
    },
  }
}
</script>

<style>
.outer-container {
  padding: var(--spacing-md) var(--spacing-sm);
  display: flex;
  flex-direction: column;
  gap: var(--spacing-xl);
}

.nav-container {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
  padding: var(--spacing-xl) 0;
  border-top: var(--border-md) solid var(--color-border-subtle);
  border-bottom: var(--border-md) solid var(--color-border-subtle);

  & .category-nav-list {
    gap: var(--spacing-md);
  }

  & .tag-nav-list {
    gap: var(--spacing-xxs);
  }
}

.category-nav-list,
.tag-nav-list {
  display: flex;
  flex-wrap: wrap;
}

.category-nav-btn {
  display: flex;
  align-items: center;
  gap: var(--spacing-xxs);

}

.tag-nav-btn {
  display: flex;
  align-items: center;
  gap: var(--spacing-xxs);
  background-color: var(--color-bg-secondary-action-enabled);
  padding: var(--spacing-xs);
  border-radius: var(--border-radius-sm);
}

.category-reg-num {
  font-family: var(--typo-font-family-english);
  min-width: 1.25rem;
  background-color: var(--color-bg-accent-subtler);
  padding: var(--spacing-xxs);
  border-radius: var(--border-radius-xs);
}

.main-container {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-lg);
}

.work-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(min(100%, 23rem), 1fr));
  gap: var(--spacing-xl);

  &>li {
    display: grid;
    grid-template-rows: subgrid;
    grid-row: span 4;

    & .work-articles {
      display: grid;
      grid-template-rows: subgrid;
      grid-row: span 4;
      gap: var(--spacing-xs);

      &>a {
        display: flex;
        flex-direction: column;
        gap: var(--spacing-md);

        & .work-thumbnail {
          width: 100%;
          border-radius: var(--border-radius-md);
        }
      }

      & .category-nav-list {
        gap: var(--spacing-sm);

        &>li {
          display: flex;
        }
      }

      & .tag-nav-list {
        gap: var(--spacing-xxs);
      }

    }
  }
}

.work-releasedAt {
  font-family: var(--typo-font-family-english);
  display: flex;
  align-items: center;
  gap: var(--spacing-xxs);
}
</style>