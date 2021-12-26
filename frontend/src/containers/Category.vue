<template>
  <div>
    <div class="uk-section">
      <b-container class="bv-example-row">
        <h1 class="uk-link-reset">
          <b-breadcrumb>
            <b-breadcrumb-item href="#home">
              <b-icon icon="house-fill" scale="1.25" shift-v="1.25" aria-hidden="true"></b-icon>
              Blog
            </b-breadcrumb-item>
            <b-breadcrumb-item href="">{{ category.name }}</b-breadcrumb-item>
          </b-breadcrumb>
        </h1>
        <b-row>
          <b-col cols="8">
            <ArticlesList :articles="category.articles || []"></ArticlesList>
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
import ArticlesList from "../components/ArticlesList";
import CategoryList from "../components/CategoryList.vue";
import gql from "graphql-tag";

export default {
  data() {
    return {
      category: [],
      routeParam: this.$route.params.id
    };
  },
  components: {
    ArticlesList,
    CategoryList
  },
  apollo: {
    category: {
      query: gql`
        query Category($id: ID!) {
          category(id: $id) {
            name
            articles {
              id
              title
              content
              image {
                url
              }
              category {
                id
                name
              }
              author{
                name
              }
            }
          }
        }
      `,
      variables() {
        return { id: this.routeParam };
      }
    }
  }
};
</script>
