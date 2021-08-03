<template>
  <base-card>
    <base-dialog v-if='inputIsInvalid' @close='confirmError'>
      <template #header>
        <h2>Input Not Valid</h2>
      </template>
      <template #default>
        <p>Unfortunately, at least one input Value is Invalid</p>
        <p>Please Check all inputs and make sure at least few characters into each Input Field</p>
      </template>

      <template #actions>
        <base-button @click='confirmError'>Okay</base-button>
      </template>
    </base-dialog>
    <form @submit.prevent='submitData'>
      <div class='form-control'>
        <label for='title'>Title</label>
        <input type='text' id='title' name='title' ref='titleInput'>
      </div>
      <div class='form-control'>
        <label for='description'>Description</label>
        <textarea type='text' id='description' name='description' rows='3' ref='descInput' />
      </div>

      <div class='form-control'>
        <label for='link'>Link</label>
        <input type='text' id='link' name='title' ref='linkInput'>
      </div>

      <div class='form-control'>
        <base-button type='submit'>Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>

export default {
  name: 'AddResource',
  inject: ['addResource'],
  emits:['close'],
  data() {
    return {
      inputIsInvalid: false
    };
  },
  methods: {
    confirmError() {
      this.inputIsInvalid = false;
    },

    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredURL = this.$refs.linkInput.value;
      if (enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredURL.trim() === '') {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(enteredTitle, enteredDescription, enteredURL);
    }
  }
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
