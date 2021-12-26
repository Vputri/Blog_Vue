<template>
  <div class="card">
    <h5 class="card-header">Kategori</h5>
    <div class="card-body">
      <div class="row">
        <div class="col-lg-12">
          <ul class="list-unstyled mb-0">
            <li
                v-for="category in categories" v-bind:key="category.id"
            >
              <router-link
                class="text-decoration-none"
                :to="{ path: '/category/' + category.id }"
                :key="category.id"
              >
                {{ category.name }}
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";

export default {
  name: "CategoryList",
  data() {
    return {
      categories: []
    };
  },
  apollo: {
    categories: gql`
      query Categories {
        categories {
          id
          name
        }
      }
    `
  }
};
</script>
