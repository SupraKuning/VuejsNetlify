<template>
  <v-app id="inspire">
    <v-navigation-drawer
      style="background-color: rgb(137, 199, 219)"
      v-model="drawer"
      app
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h6" style="color: rgb(12, 70, 88)">
            GAVRIEL NEWS
          </v-list-item-title>
          <v-list-item-subtitle style="color: rgb(12, 70, 88)">
            hot banget newsnya
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider class="mx-3 my-5"></v-divider>

      <v-list-item
        v-for="item in berita"
        id="article"
        :key="item.title"
        style="color: rgb(12, 70, 88)"
        link
      >
        <v-avatar
          class="d-block text-center mx-auto mr-5"
          color="blue lighten-1"
          size="40"
        >
          <img :src="item.urlToImage" alt="" />
        </v-avatar>
        <v-list-item-content>
          <v-list-item-title> {{ item.title }} </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-navigation-drawer>
    <br />
    <v-app-bar style="background-color: rgb(137, 199, 219)" app>
      <v-app-bar-nav-icon
        style="color: rgb(12, 70, 88)"
        @click="drawer = !drawer"
      ></v-app-bar-nav-icon>

      <v-toolbar-title style="color: rgb(12, 70, 88)"
        >BERITA HARI INI, SOALNYA API NYA CUMA BISA SEHARI</v-toolbar-title
      >
    </v-app-bar>

    <v-main>
      <v-card
        elevation="9"
        shaped
        style="width: 50%; margin: auto; margin-bottom: 20px"
        v-for="item in berita"
        id="article"
        :key="item.title"
      >
        <v-img img :src="item.urlToImage" alt=""></v-img>
        <v-card-title> {{ item.title }} </v-card-title>
        <v-card-text>
          {{ item.description }}
        </v-card-text>
      </v-card>
    </v-main>
  </v-app>
</template>

<script>
export default {
  // data: () => ({ drawer: null }),
  data() {
    return {
      berita: [],
      drawer: null,
    };
  },
  mounted() {
    this.$axios
      .get(
        "https://newsapi.org/v2/everything?q=tesla&from=2022-03-11&sortBy=publishedAt&apiKey=b0add871ad124200989a58f18fb4e036"
      )
      .then((response) => {
        this.berita = response.data.articles;
      });
  },
};
</script>

<style scoped>
#inspire {
  background-color: rgb(172, 214, 227);
}

.v-navigation-drawer {
  background-color: rgb(137, 199, 219);
  color: white;
}
.v-list-item-title {
  color: white;
}
</style>
