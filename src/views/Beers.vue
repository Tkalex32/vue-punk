<template>
  <v-container class="grey lighten-5 home pa-4">
    <v-row class="my-n4">
      <v-col />
      <v-col class="text-center">Alcohol By Volume (%)</v-col>
    </v-row>
    <v-row class="my-n8">
      <v-col cols="6">
        <v-text-field
          v-model="search"
          placeholder="Search"
          prepend-inner-icon="mdi-magnify"
          class="mt-6"
          solo
          dense
        ></v-text-field>
      </v-col>

      <v-col class="px-4">
        <v-range-slider
          v-model="range"
          :max="max"
          :min="min"
          :value="[0, 50]"
          class="align-center"
        >
          <template v-slot:prepend>
            <v-text-field
              :value="range[0]"
              class="mt-0 pt-0"
              hide-details
              single-line
              type="number"
              style="width: 60px"
              @change="$set(range, 0, $event)"
            ></v-text-field>
          </template>
          <template v-slot:append>
            <v-text-field
              :value="range[1]"
              class="mt-0 pt-0"
              hide-details
              single-line
              type="number"
              style="width: 60px"
              @change="$set(range, 1, $event)"
            ></v-text-field>
          </template>
        </v-range-slider>
      </v-col>
    </v-row>

    <v-row>
      <v-col v-for="beer in filterBeers" :key="beer.id" cols="12" sm="4">
        <v-hover v-slot="{ hover }">
          <v-card width="375" class="mx-auto">
            <v-img :src="beer.image_url" max-height="300" contain dark>
              <v-fade-transition>
                <v-overlay v-if="hover" absolute color="blue darken-4">
                  <v-list-item>
                    <v-list-item-content>
                      Food Pairing:
                      <ul
                        class="my-2"
                        v-for="food in beer.food_pairing"
                        :key="food"
                      >
                        <li>{{ food }}</li>
                      </ul>
                    </v-list-item-content>
                  </v-list-item>
                </v-overlay>
              </v-fade-transition>
            </v-img>
            <v-row class="fill-height justify-center">
              <v-card-title class="blue--text">
                <div class="title">{{ beer.name }}</div>
              </v-card-title>
            </v-row>

            <v-list two-line>
              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title class="text-center">{{
                    beer.tagline
                  }}</v-list-item-title>
                  <div class="text-center">
                    <v-chip class="ma-2" color="warning" outlined pill>
                      abv: {{ beer.abv }}
                    </v-chip>
                    <v-chip class="ma-2" color="warning" outlined pill>
                      ibu: {{ beer.ibu }}
                    </v-chip>
                  </div>
                </v-list-item-content>
              </v-list-item>

              <v-divider></v-divider>

              <v-list-item>
                <v-list-item-content>
                  <div class="my-2 d-flex justify-space-between">
                    <Popup :beer="beer" />
                    <v-btn color="teal white--text">Buy</v-btn>
                  </div>
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </v-card>
        </v-hover>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Popup from "./../components/Popup";
export default {
  components: { Popup },
  name: "Home",
  data() {
    return {
      beers: [],
      search: "",
      min: 0,
      max: 50,
      range: [0, 50],
    };
  },
  methods: {
    fetchData() {
      fetch("https://api.punkapi.com/v2/beers?page=2&per_page=50")
        .then((res) => {
          return res.json();
        })
        .then(this.setResults);
    },
    setResults(results) {
      this.beers = results;
      this.searchBeer = results;
    },
    filterBeersByName: function(beers) {
      return beers.filter((beer) => beer.name.toLowerCase().match(this.search));
    },
    filterBeersByRange: function(beers) {
      return beers.filter((beer) =>
        beer.abv >= this.range[0] && beer.abv <= this.range[1] ? beer : ""
      );
    },
  },
  beforeMount() {
    this.fetchData();
  },
  computed: {
    /* searchedBeers() {
      return this.searchBeer.filter((beer) => {
        return beer.name.toLowerCase().match(this.search);
      });
    }, */
    filterBeers: function() {
      return this.filterBeersByRange(this.filterBeersByName(this.beers));
    },
  },
};
</script>
<style>
.v-card__title {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
</style>
