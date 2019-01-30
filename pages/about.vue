<template>
  <div>
    <section class="main-content columns">
      <aside class="column is-2 section">
        <p class="menu-label is-hidden-touch">General</p>
        <ul class="menu-list">
          <li v-for="author of allAuthors" :key="author.id">
            <div class="author">
              <div class="info-header">
                <img
                  src="`https://media.graphcms.com/resize=w:100,h:100,fit:crop/${author.avatar.handle}`"
                  alt="author.name"
                >
                <h1>Hello! My name is {{ author.name }}</h1>
                <p>{{ author.bibliography }}</p>
              </div>
            </div>
          </li>
        </ul>
      </aside>

      <div class="container column is-10">
        <nuxt/>
      </div>
    </section>
  </div>
</template>

<script>
import gql from 'graphql-tag'
export const allAuthors = gql`
  query allAuthors {
    allAuthors {
      id
      name
      bibliography
      avatar {
        handle
      }
    }
  }
`
export default {
  name: 'AboutPage',
  data: () => ({
    loading: 0
  }),
  apollo: {
    $loadingKey: 'loading',
    allAuthors: {
      query: allAuthors,
      prefetch: true
    }
  }
}
</script>

<style scoped lang="scss">
.author {
  margin-bottom: 72px;
}
.info-header {
  text-align: center;
}
img {
  height: 120px;
  width: auto;
}
</style>
