<template>
    <v-col cols="12" sm="4">
      <v-card class="mx-auto" max-width="400">
        <v-img
          v-bind:src="character.image" v-bind:alt="character.name"
          cover
        ></v-img>
        <v-card-title>
          {{ character.name }}
        </v-card-title>
        <v-card-subtitle>
          {{ character.origin.name }}
        </v-card-subtitle>
        <v-card-actions>
          
          <!-- oafaousfhaosidahos -->
            <v-btn
              block
              variant="flat"
              color="success"
              @click="($event) => showModal(character.id)">
              More
              <modal v-bind:dialog="dialog"
                v-bind:currentCharacter="currentCharacter"/>
            </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </template>
  <script>
    import Modal from './ModalDetail';
    import axios from 'axios';

  export default {
    name: 'CharacterItem',
    props: ["character"],
    components: {
      Modal,
    },
    data: function () {
      return {
        currentCharacter: [],
        dialog: false
      };
    },
    methods: {
      showModal(id) {
      this.fetchOne(id);
    },
    async fetchOne(id) {
      //
      let result = await axios.get(
        `https://rickandmortyapi.com/api/character/${id}`
      );
      this.currentCharacter = result.data;
      this.modal = true;
      console.log(this.currentCharacter, "Personaje");
    },
    },
  };
  </script>