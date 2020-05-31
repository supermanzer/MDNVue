<template>
  <div class="stack-small" v-if="!isEditing">
    <div class="custom-checkbox">
      <label :for="id">  
        <input
          type="checkbox"
          name="todo-item"
          :id="id"
          :checked="isDone"
          @change="$emit('checkbox-changed')"
        />
        <span>{{ label }}</span></label>
    </div>
    <div class="btn-group">
      <button type="button" ref="editButton" class="btn amber" @click="toggleToItemEditForm">
        Edit <span class="visually-hidden">{{ label }}</span>
      </button>
      <button type="button" class="btn red darken-3" @click="deleteToDo">
        Delete <span class="visually-hidden">{{ label }}</span>
      </button>
    </div>
  </div>
  <to-do-item-edit-form v-else :id="id" :label="label"
                        @item-edited="itemEdited"
                        @edit-canceled="editCancelled"></to-do-item-edit-form>
</template>

<script>
import ToDoItemEditForm from "./ToDoItemEditForm";

export default {
  props: {
    label: { required: true, type: String },
    done: { default: false, type: Boolean },
    id: { required: true, type: String },
  },
  components: {
      ToDoItemEditForm
  },
  data() {
    return {
      isEditing: false,
    };
  },
  methods: {
    deleteToDo() {
      this.$emit("item-deleted");
    },
    toggleToItemEditForm() {
        console.log(this.$refs.editButton);
        this.isEditing = true;
    },
    itemEdited(newLabel) {
        this.$emit('item-edited', newLabel);
        this.isEditing = false;
        this.focusOnEditButton();
    },
    editCancelled() {
        this.isEditing = false;
        this.focusOnEditButton();
    },
    focusOnEditButton() {
        this.$nextTick(() =>{
            const editButtonRef = this.$refs.editButton;
            editButtonRef.focus();
        })
       
    }
  },
  computed: {
      isDone() {
          return this.done;
      }
  }
};
</script>

<style scoped>
span {
    font-size: 2rem !important;
}

.btn-group {
    padding-top: 0.75rem;
}

</style>
