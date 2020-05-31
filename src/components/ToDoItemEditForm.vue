<template>
  <form class="stack-small" @submit.prevent="onSubmit">
    <div>
      <label class="edit-label">Edit Name for &quot;{{ label }}&quot;</label>
      <input
        :id="id"
        type="text"
        autocomplete="off"
        ref="labelInput"
        v-model.lazy.trim="newLabel"
      />
    </div>
    <div class="btn-group">
      <button type="button" class="btn grey lighten-2" @click="onCancel">
        Cancel
        <span class="visually-hidden">editing {{ label }}</span>
      </button>
      <button class="btn blue accent-2"> Save
        <span class="visually-hidden">edit for {{ label }} </span>
      </button>
    </div>
  </form>
</template>
<script>
export default {
    props: {
        label: {
            type: String,
            required: true
        },
        id: {
            type: String,
            required: true
        }
    },
    mounted() {
        const labelInputRef = this.$refs.labelInput;
        labelInputRef.focus();
    },
    data() {
        return {
            newLabel: this.label
        }
    },
    methods: {
        onSubmit() {
            if (this.newLabel && this.newLabel !== this.label) {
                this.$emit("item-edited", this.newLabel);
            }
        },
        onCancel() {
            this.$emit("edit-canceled");
        }
    }
}
</script>
<style scoped>

</style>
