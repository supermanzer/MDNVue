<template>
  <div id="app" class="container">
    <div class="card">
      <div class="card-content">
        <h1 class="center-align">To-Do List</h1>
        <to-do-form @todo-added="addToDo"></to-do-form>
        <h3 class="center-align"  ref="listSummary" tabindex="-1" id="list-summary">{{listSummary}}</h3>
        <div class="row">
          <div class="col s8 offset-s2">
            <ul aria-labelledby="list-summary" class="stack-large">
              <li v-for="item in ToDoItems" :key="item.id">
                <to-do-item :label="item.label" :done="item.done" :id="item.id"
                            @checkbox-changed="updateDoneStatus(item.id)"
                            @item-deleted="deleteToDo(item.id)"
                            @item-edited="editToDo(item.id, $event)"></to-do-item>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ToDoItem from './components/ToDoItem'
import ToDoForm from './components/ToDoForm'
import uniqueId from 'lodash.uniqueid'

export default {
  name: 'App',
  components: {
    ToDoItem,
    ToDoForm
  },
  data() {
    return {
      ToDoItems: [
        { id: uniqueId('todo-'), label: 'Learn Vue', done: false },
        { id: uniqueId('todo-'), label: 'Create a Vue project with the CLI', done: true },
        { id: uniqueId('todo-'), label: 'Have fun', done: true },
        { id: uniqueId('todo-'), label: 'Create a to-do list', done: false },
        { id: uniqueId('todo-'), label: 'Drink bubbly', done: false },
        { id: uniqueId('todo-'), label: 'Eat cheese', done: false },
        { id: uniqueId('todo-'), label: 'Have Fun', done: true }  // This
      ]
    }
  },
  methods: {
    addToDo(toDoLabel) {
      this.ToDoItems.push({id: uniqueId('todo-'), label: toDoLabel, done: false})
    },
    updateDoneStatus(toDoId) {
      const toDoToUpdate = this.ToDoItems.find(item => item.id === toDoId)
      toDoToUpdate.done = !toDoToUpdate.done
    },
    deleteToDo(toDoId) {
      const itemIndex = this.ToDoItems.findIndex(item => item.id === toDoId);
      this.ToDoItems.splice(itemIndex, 1);
      this.$refs.listSummary.focus();
    },
    editToDo(toDoId, newLabel) {
      const toDoToEdit = this.ToDoItems.find(item => item.id === toDoId);
      toDoToEdit.label = newLabel;
    }
  },
  computed: {
    listSummary() {
      const numberFinishedItems = this.ToDoItems.filter(item => item.done).length;
      return `${numberFinishedItems} out of ${this.ToDoItems.length} items completed`
    }
  },
}
</script>
<style>
/* Global styles */
#app {
  font-family: Manrope, Helvetica, sans-serif;


}
.stack-large > * + * {
  margin-top: 3rem;
}
.btn-group {
    display: flex;
    justify-content:space-around;
}

</style>