<template>
<base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
  <template #defult>
    <p>At least one input value is invalid</p>
    <p>Please check all inputs</p>
  </template>
  <template #actions>
    <base-button @click="confirmError">Okay</base-button>
  </template>
</base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          id="decription"
          name="description"
          rows="3"
          ref="descInput"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
export default {
  components: { BaseButton },
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false
    }
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredLink = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredLink.trim() === ''
      ) {
        this.inputIsInvalid = true
        return;
      }

      this.addResource(enteredTitle, enteredDescription, enteredLink);
    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  },
};
</script>

<style>
</style>