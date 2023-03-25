<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="Invalid Input"
    @close="confirmError"
  >
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>
        Please check all inputs and make sure you enter at least a few
        characters into each input field.
      </p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="mb-3">
        <label for="title" class="form-label">Title</label>
        <input
          type="text"
          id="title"
          name="title"
          class="form-control"
          ref="titleInput"
        />
      </div>
      <div class="mb-3">
        <label for="description" class="form-label">Description</label>
        <textarea
          type="text"
          class="form-control"
          id="description"
          name="description"
          ref="descInput"
        />
      </div>
      <div class="mb-3">
        <label for="link" class="form-label">Link</label>
        <input
          type="url"
          class="form-control"
          id="link"
          name="link"
          ref="linkInput"
        />
      </div>
      <base-button type="submit">Add Resource</base-button>
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
    submitData() {
      const newData = [
        this.$refs.titleInput.value,
        this.$refs.descInput.value,
        this.$refs.linkInput.value,
      ];
      if (
        newData[0].trim() === "" ||
        newData[1].trim() === "" ||
        newData[2].trim() === ""
      ) {
        this.inputIsInvalid = true;
        return;
      }
      this.addResource(newData[0], newData[1], newData[2]);
    },
    
    confirmError() {
      this.inputIsInvalid = false;
    },
  },
};
</script>

<style scoped>
.card {
  margin: auto;
  max-width: 40rem;
}
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
  background-color: #e4f7fa;
}

.form-control {
  margin: 1rem 0;
}
</style>
