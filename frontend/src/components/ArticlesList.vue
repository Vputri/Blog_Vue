<template>
  <div className="card mb-4">
    <div className="card-body">
      <router-link
        v-for="article in articles"
        :to="{ path: '/article/' + article.id }"
        class="uk-link-reset"
        :key="article.id"
      >
        <div class="card mb-4">
          <div class="card-img-top lazy-image">
            <img :src="article.image.url" v-if="state === 'production'" alt="" height="100" />
            <img :src="api_url + article.image.url" v-else alt="" height="100" />
          </div>
          <div class="card-body">
            <h1>{{article.title}}</h1>
            <p>{{article.description}}</p>
          </div>
          <div class="card-footer text-muted">
            <p v-if="article.category">
              Posted by {{article.author.name}} in category {{ article.category.name }} 
            </p>
          </div>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      api_url: process.env.VUE_APP_STRAPI_API_URL || "http://localhost:1337",
      state: process.env.NODE_ENV
    };
  },
  props: {
    articles: Array
  }
};
</script>