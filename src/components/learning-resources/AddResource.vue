<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="Invalid Input"
    @close="confirmError"
  >
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>Please. check all the inputs correctly.</p></template
    >
    <template #actions
      ><base-button @click="confirmError">Okay</base-button></template
    ></base-dialog
  >
  <base-card
    ><form @submit.prevent="submit">
      <div class="form-control">
        <lable for="title">Title</lable>
        <input id="title" name="title" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <lable for="description">Description</lable>
        <textarea id="description" name="description" rows="3" ref="desInput" />
      </div>
      <div class="form-control">
        <lable for="link">URL</lable>
        <input id="link" name="link" type="url" ref="linkInput" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>
<script>
export default {
  inject: ["addResource"],
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  methods: {
    submit() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.desInput.value;
      const enteredUrl = this.$refs.linkInput.value;
      if (
        enteredTitle.trim() === "" ||
        enteredDescription.trim() === "" ||
        enteredUrl.trim() === ""
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(enteredTitle, enteredDescription, enteredUrl);
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
  },
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
