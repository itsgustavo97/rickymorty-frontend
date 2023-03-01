<template>
  <div class="modal" :class="{ 'is-active': modal }" v-if="modal">
    <div class="modal-background" @click="($event) => modal"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">Acerca de: {{ currentCharacter.name }}</p>
        <button class="delete" aria-label="close"></button>
      </header>
      <section class="modal-card-body">
        <!-- Content -->
        <label class="label">Genero</label>
        <span>{{ currentCharacter.gender }}</span>

        <label class="label">Estado</label>
        <span>{{ currentCharacter.status }}</span>

        <label class="label">Especie</label>
        <span>{{ currentCharacter.species }}</span>

        <label class="label">Tipo</label>
        <span>{{ currentCharacter.type }}</span>
      </section>
      <footer class="modal-card-foot">
        <button class="button" @click="($event) => modal">Cerrar</button>
      </footer>
    </div>
  </div>
</template>
<script>
export default {
  name: "ModalItem",
  props: {
    currentCharacter: [],
    modal: Boolean,
  },
  data: () => {},
  methods: {
  },
};
</script>