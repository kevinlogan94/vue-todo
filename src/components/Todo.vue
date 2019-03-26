<template>
    <div class="card">
        <button v-on:click="updateView('all')" v-bind:class="{focused: view==='all'}">All</button>
        <button v-on:click="updateView('todo')" v-bind:class="{focused: view==='todo'}">Todo</button>
        <button v-on:click="updateView('completed')" v-bind:class="{focused: view==='completed'}">Completed</button>
        <button v-on:click="edit()" v-bind:class="{focused: editable}">Edit</button>        
        <InputForm v-bind:submit="addTodo" v-bind:editable="editable" v-bind:errorMessage="error"/>
        <ol>
            <li v-for="todo in todos" v-bind:key="todo.id" v-bind:class="{displayNone: !displayTodo(todo)}">
                <span v-if="displayTodo(todo)">
                    <button title="delete" v-if="editable" v-on:click="deleteTodo(todo)" class="icon">X</button> <input type="checkbox" v-if="!editable" v-bind:checked="todo.completed" v-on:click="toggleTodo(todo)" /> {{todo.task}}
                </span>
            </li>
        </ol>
        <button v-if="editable" v-on:click="saveChanges()">Save</button>
        <button v-if="editable" v-on:click="cancel()">Cancel</button>
    </div>
</template>

<script>
import InputForm from "./InputForm";

export default {
  name: 'Todo',
  components: {
    InputForm
  },
  data: function() {
    return {
        todos: [{task: "clean the dishes", completed: false, display: true, id:0}, {task: "vacuume the living room", completed: false, display: true, id:1}], 
        view: "all",
        error: "Please provide a task to be added.",
        editable: false,
        id: 1
    }
  },
  methods: {
    addTodo: function(todo) {
        let newId = ++this.id;
        let newTodo = {task: todo, completed: false, display: true, id: newId}
        this.todos.unshift(newTodo);
    },
    cancel: function(){
        this.todos.forEach(todo => {
            if(!todo.display) {
                //Add back the missing todos.
                todo.display = true;
            }
        })
        this.editable = false;
    },
    toggleTodo: function(todo) {
        todo.completed = !todo.completed;
    },
    deleteTodo: function(todo) {
        todo.display = false;
    },
    displayTodo: function(todo) {
        if(todo.display === false) {
            return false;
        }

        if(this.view==="all") {
            return true;
        } else if(todo.completed && this.view==="completed") {
            return true;
        } else if(!todo.completed && this.view==="todo") {
            return true;
        }
        return false;
    },
    edit: function(){
        this.editable = !this.editable;
    },
    saveChanges: function() {
        //filter out all the todos we no longer want.
        this.todos = this.todos.filter(todo => todo.display)
        this.editable = false;
    },
    updateView: function(newView){
        if(newView === "all" || newView === "completed" || newView === "todo") {
            this.view = newView
        }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .card {
        position: relative;
        margin: auto;
        height: auto;
        width: 20%;
        background-color: #f1f1f1;
        box-shadow: 0 2px 4px 0 rgba(0,0,0,0.16),0 2px 10px 0 rgba(0,0,0,0.12);
    }
    .icon {
        background: none;
        border: none;
        padding: 0;
    }
    ol {
        list-style: none;
        text-align: left;
    }
    .displayNone {
        display: none;
    }
    .error {
        color: red;
        font-size: 12px;
        padding-top: 0;
        margin-top: 2px;
    }
    .focused {
        background-color: lightgray;
    }
</style>
