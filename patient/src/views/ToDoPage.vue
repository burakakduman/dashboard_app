<template class="body">
    <h3 class="text-center">List</h3>
    <hr>
    <div class="q-pa-xl">
        <q-form @submit.prevent="addTodo">
            <div>
                <div>
                    <q-input v-model="newTodo" label="Add a new todo" class="" />
                    <q-btn type="submit" label="Add" color="primary" />


                </div>
            </div>
            <q-hr size="3px" color="" />
        </q-form>
        <q-hr />
        <hr>
        <q-list>
            <q-item v-for="todo in todos" :key="todo.id" clickable>
                <!-- <q-item-label>{{ todo.text }}</q-item-label> -->
                <div>
                    <q-input filled color="purple-12" v-model="todo.text" label="Label">
                        <template v-slot:append>
                            <q-btn color="negative" label="Delete" @click="deleteTodo(todo.id)" />
                        </template>
                    </q-input>
                    <!-- <q-item-section side>
                        <q-btn color="negative" label="Delete" @click="deleteTodo(todo.id)" />
                    </q-item-section> -->
                </div>
            </q-item>
        </q-list>

    </div>
    <div class=" q-pa-md">
        <pre>{{ JSON.stringify(todos, null, 2) }}</pre>
    </div>
</template>

<script>

import { ref } from 'vue';

export default {
    setup() {
        const todos = ref([]);
        const newTodo = ref('');
        const textInput = ref(null);

        const addTodo = () => {
            if (newTodo.value.trim() !== '') {
                todos.value.push({ id: Date.now(), text: newTodo.value });
                newTodo.value = '';
                saveTodosToLocalStorage();
                if (textInput.value) {
                    textInput.value.focus();
                }
            }
        };

        const deleteTodo = (todoId) => {
            todos.value = todos.value.filter((todo) => todo.id !== todoId);
            saveTodosToLocalStorage();
        };

        const saveTodosToLocalStorage = () => {
            localStorage.setItem('todos', JSON.stringify(todos.value));
        };

        const loadTodosFromLocalStorage = () => {
            const savedTodos = localStorage.getItem('todos');
            if (savedTodos) {
                todos.value = JSON.parse(savedTodos);
            }
        };

        loadTodosFromLocalStorage();

        const focusTextInput = () => {
            if (textInput.value) {
                textInput.value.focus();
            }
        };

        return {
            todos,
            newTodo,
            textInput,
            addTodo,
            deleteTodo,
            focusTextInput,
        };
    },
};
</script>

<style scoped>
.qinput {
    width: 100% !important;
}
</style>