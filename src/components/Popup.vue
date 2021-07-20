<template>
  <div class="text-center">
    <v-dialog v-model="dialog" min-width="500" max-width="800">
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="primary white--text" dark v-bind="attrs" v-on="on">
          More info
        </v-btn>
      </template>

      <v-card @click="dialog = false">
        <article class="blog-card">
          <img
            class="post-image fill-height justify-center"
            :src="$attrs.beer.image_url"
          />
          <div class="article-details" primary--text>
            <h3 class="post-title">{{ $attrs.beer.name }}</h3>
            <h4 class="post-category">{{ $attrs.beer.tagline }}</h4>
            <p class="post-description">{{ $attrs.beer.description }}</p>
            <p class="post-author">
              Brewery tip: {{ $attrs.beer.brewers_tips }}
            </p>
            <p class="post-author">
              Yeast: {{ $attrs.beer.ingredients.yeast }}
            </p>
          </div>
        </article>

        <!-- <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" text @click="dialog = false">
            Close
          </v-btn>
        </v-card-actions> -->
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: ["name"],
  data() {
    return {
      dialog: false,
    };
  },
};
</script>
<style>
.blog-card {
  display: flex;
  flex-direction: row;
  box-shadow: 0 0.1875rem 1.5rem rgba(0, 0, 0, 0.2);
  border-radius: 0.375rem;
  overflow: hidden;
}

.card-link {
  position: relative;
  display: block;
  color: inherit;
  text-decoration: none;
}

.card-link:hover .post-title {
  color: #e04f62;
}

.card-link:hover .post-image {
  opacity: 0.9;
}

.post-image {
  display: block;
  object-fit: cover;
  padding: 20px;
  width: 150px;
}

.article-details {
  padding: 1.5rem;
}

.post-category {
  display: inline-block;
  text-transform: uppercase;
  font-size: 0.75rem;
  font-weight: 700;
  line-height: 1;
  letter-spacing: 0.0625rem;
  margin: 0 0 0.75rem 0;
  padding: 0 0 0.25rem 0;
  border-bottom: 0.125rem solid #ebebeb;
}

.post-title {
  font-size: 1.125rem;
  line-height: 1.4;
  color: #121212;
  font-weight: 700;
  margin: 0 0 0.5rem 0;
}

.post-author {
  font-size: 0.875rem;
  line-height: 1;
  margin: 1.125rem 0 0 0;
  padding: 1.125rem 0 0 0;
  border-top: 0.0625rem solid #ebebeb;
}
</style>
