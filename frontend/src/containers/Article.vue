<template>
  <div class="py-4">
    <div class="container px-5">
      <b-row>

        <b-col cols="8">
          <div class="card mb-4">
            <div class="card-body">
              <div class="container px-5 py-5">
                <div class="jumbotron"> 
                  <h1 class="text-center mb-5">{{ article.title }}</h1>   

                  <p v-if="article.published_at">
                    Posted by {{article.author.name}} at {{ moment(article.published_at).format("MMM Do YY") }}
                  </p>

                  <div class="mb-5">
                    <img :src="article.image.url" v-if="state === 'production'" alt="" height="100" />
                    <img :src="api_url + article.image.url" v-else alt="" height="100" />
                  </div>

                  <div class="mb-5">
                    <vue-markdown-it
                      v-if="article.content"
                      :source="article.content"
                      id="editor"
                    />
                  </div>

                </div>
              </div>
            </div>
          </div>
        </b-col>

        <b-col cols="4">
          <CategoryList />
        </b-col>

      </b-row>
    </div>
  </div>
</template>

<script>
var moment = require("moment");
import VueMarkdownIt from "vue-markdown-it";
import CategoryList from "../components/CategoryList.vue";
import gql from "graphql-tag";

export default {
  data() {
    return {
      article: {},
      moment: moment,
      api_url: process.env.VUE_APP_STRAPI_API_URL || "http://localhost:1337",
      routeParam: this.$route.params.id
    };
  },
  components: {
    VueMarkdownIt,
    CategoryList,
  },
  apollo: {
    article: {
      query: gql`
        query Articles($id: ID!) {
          article(id: $id) {
            id
            title
            content
            image {
              url
            }
            published_at
            author{
              name
            }
          }
        }
      `,
      variables() {
        return {
          id: this.routeParam
        };
      }
    }
  }
};
</script>
