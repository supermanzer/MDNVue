<template>
    <form class="row" @submit.prevent="onSubmit">
        <div class="input-field col s8 offset-s2 center-align">
            <h2 class="label-wrapper">
                <label for="new-todo-input">What needs to be done?</label>
            </h2>
            <input 
                type="text" 
                name="new-todo" 
                id="new-todo-input" 
                autocomplete="off" 
                v-model.trim.lazy="label"
                class="input__lg">
        </div>    
        <div class="col s12 center-align">
            <button type="submit" class="btn btn__primary btn__lg">Add ToDo</button>
        </div>
    </form>
</template>

<script>
export default {
    methods: {
        onSubmit() {
            if (this.label === "") {
                return;
            }
            this.$emit('todo-added', this.label);
            this.label = "";
        }
    },
    data() {
        return {
            label: ""
        }
    },
}
</script>
<style scoped>
label {
    font-size: 2rem !important
}
</style>