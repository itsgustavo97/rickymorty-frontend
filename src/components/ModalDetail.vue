<template>
  <v-dialog v-model="dialog" activator="parent" width="450px">
    <v-card>
      <v-card-title>
        {{ currentCharacter.name }}
      </v-card-title>
      <v-card-text>
        <v-form disabled>
          <v-text-field>{{ currentCharacter.gender== '' ? 'No gender': currentCharacter.gender }}</v-text-field>
          <v-text-field>{{ currentCharacter.status== '' ? 'No status': currentCharacter.status }}</v-text-field>
          <v-text-field>{{ currentCharacter.species== '' ? 'No species': currentCharacter.species }}</v-text-field>
          <v-text-field>{{ currentCharacter.type== '' ? 'No type': currentCharacter.type }}</v-text-field>
        </v-form>
        
      </v-card-text>
      <v-card-actions>
        <v-btn color="primary" block @click="dialog = false">Cerrar</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>
<script>
export default {
  props: {
    currentCharacter: []
  },
  data: () => ({
    dialog: false,

  }),
}
</script>