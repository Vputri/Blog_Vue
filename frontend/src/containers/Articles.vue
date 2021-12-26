<template>
  <div>
    <div class="uk-section">
      <b-container class="bv-example-row">
        <h1 class="uk-link-reset">
          <b-breadcrumb>
            <b-breadcrumb-item href="">
              <b-icon icon="house-fill" scale="1.25" shift-v="1.25" aria-hidden="true"></b-icon>
              Blog
            </b-breadcrumb-item>
          </b-breadcrumb>
        </h1>
        <b-row>
          <b-col cols="8">
            <ArticlesList :articles="articles"></ArticlesList>
          </b-col>
          <b-col cols="4">
            <CategoryList />
          </b-col>
        </b-row>
      </b-container>
    </div>
  </div>
</template>

<script>
import ArticlesList from "../components/ArticlesList.vue";
import CategoryList from "../components/CategoryList.vue";
import gql from "graphql-tag";

export default {
  components: {
    ArticlesList,
    CategoryList
  },
  data() {
    return {
      articles: []
    };
  },
  apollo: {
    articles: gql`
      query Articles {
        articles {
          id
          title
          content
          image {
            url
          }
          author{
            name
          }
          category {
            name
          }
        }
      }
    `
  }
};
</script>
