<template>
  <v-app id="inspire">
    <v-app-bar
      :clipped-left="$vuetify.breakpoint.lgAndUp"
      app
      color="primary"
      dark
    >
      <!--      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />-->

      <v-toolbar-title style="width: 350px">
        <a href="/" class="white--text" style="text-decoration: none"
          ><v-icon>mdi-glass-mug-variant</v-icon>&nbsp;PunkBeer</a
        >
      </v-toolbar-title>

      <v-spacer />
      <v-btn icon>
        <v-icon>mdi-account-circle</v-icon>
      </v-btn>
      <v-btn icon>
        <v-badge content="2" value="2" color="red" overlap>
          <v-icon>mdi-bell</v-icon>
        </v-badge>
      </v-btn>
      <v-btn icon>
        <v-badge content="1" value="1" color="green" overlap>
          <v-icon>mdi-cart</v-icon>
        </v-badge>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>

    <v-footer :padless="true">
      <v-card flat tile width="100%" class="secondary white--text text-center">
        <v-card-text>
          <v-btn class="mx-4 white--text" icon>
            <v-icon size="24px">mdi-home</v-icon>
          </v-btn>
          <v-btn class="mx-4 white--text" icon>
            <v-icon size="24px">mdi-email</v-icon>
          </v-btn>
        </v-card-text>

        <v-card-text class="white--text pt-0">
          Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quia
          corrupti perspiciatis minima porro nobis maiores vitae magnam dicta
          iure aperiam impedit, quasi necessitatibus laborum provident
          exercitationem error rem laboriosam sint culpa tempore numquam
          assumenda hic. Odio, similique doloribus dolores reprehenderit ab quia
          tempora, recusandae quibusdam dolore veniam laborum necessitatibus
          nulla modi magni id est repellat, illo ut. Dolorum rem nesciunt nisi
          atque laudantium dignissimos ducimus quidem neque vel iusto,
          voluptatem sequi aspernatur magnam laboriosam, maxime architecto
          distinctio tempora quas consectetur? Alias cupiditate minima dolores,
          ad id officiis voluptatibus doloribus quisquam iure distinctio magnam
          mollitia! Deserunt quas sequi eaque molestiae doloribus.
        </v-card-text>

        <v-divider></v-divider>

        <v-card-text class="white--text">
          {{ new Date().getFullYear() }} — <strong>PunkBeer</strong>
        </v-card-text>
      </v-card>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: false,
    items: [
      { title: "Beers", icon: "mdi-glass-mug-variant", to: "/" },
      { title: "About", icon: "mdi-help-box", to: "/about" },
    ],
    activeBtn: 1,
  }),
};
</script>
