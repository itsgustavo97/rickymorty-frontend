<template>
  <v-card>
    <v-layout>
      <!-- <v-system-bar color="deep-purple darken-3"></v-system-bar> -->

      <v-app-bar color="success" prominent>
        <v-app-bar-nav-icon variant="text" @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

        <v-toolbar-title>Rick & morty</v-toolbar-title>

        <v-spacer></v-spacer>

        <v-text-field clearable label="Buscar" v-model="search" v-on:keyup.enter="searchCharacter"
          append-inner-icon="mdi-magnify"></v-text-field>

        <v-btn variant="text" icon="mdi-filter" v-model="search" @click="searchCharacter"></v-btn>

        <v-btn variant="text" icon="mdi-dots-vertical"></v-btn>
      </v-app-bar>

      <v-navigation-drawer v-model="drawer" location="left" temporary>
        <v-list :items="items"></v-list>
      </v-navigation-drawer>

      <v-main>
        <v-container fluid>
          <v-card title="Personajes de rick & morty" elevation="4">
            <v-row dense>
              <!-- Here goes the card character from Character.vue component-->
              <character @showModal="showModal" v-for="character of characters" v-bind:key="character.id"
                v-bind:character="character" />
            </v-row>
            <div class="text-center">
              <v-row justify="center">
                <v-col cols="8">
                  <v-pagination v-model="page" class="my-4" :length="pages" rounded="circle"
                    v-on:click="changePage(page)"></v-pagination>
                </v-col>
              </v-row>
            </div>
          </v-card>
        </v-container>
      </v-main>
    </v-layout>
  </v-card>
</template>

<script>
import axios from "axios";
import Character from "./components/Character";

export default {
  name: "App",
  components: {
    Character,
  },
  data: () => ({
    characters: [],
    page: 1,
    pages: 1,
    search: "",
    modal: false,
    currentCharacter: {},
    drawer: false,
  }),

  created() {
    this.fetch();
  },
  methods: {
    fetch() {
      const params = {
        page: this.page,
        name: this.search,
      };
      axios
        .get("https://rickandmortyapi.com/api/character/", { params })
        .then((res) => {
          this.characters = res.data.results;
          this.pages = res.data.info.pages;
        })
        .catch((err) => {
          console.log(err);
        });
    },

    changePage(page) {
      this.page = page <= 0 || page > this.pages ? this.page : page;
      this.fetch();
    },
    searchCharacter() {
      this.page = 1;
      this.fetch();
    },

  },
};
</script>