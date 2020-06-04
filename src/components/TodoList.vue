<template>
    <div>
        <ul>
            <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item">
                <i class="fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem, index)"></i>
                <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
                <span v-on:click="removeTodo(todoItem, index)">
                    <i class="fas fa-trash-alt"></i>
                </span>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        data: function() {
            return{
                todoItems: []
            }
        },
        methods: {
          removeTodo: function (todoItem, index) {
              console.log(todoItem, index);
              localStorage.removeItem(todoItem);
              this.todoItems.splice(index, 1);
          },
            toggleComplete: function (todoItem) {
                todoItem.completed = !todoItem.completed;
                localStorage.removeItem(todoItem.item);
                localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
            }
        },
        created: function () {
            if(localStorage.length > 0) {
                for (var i = 0 ; i < localStorage.length ; i++) {
                    if(localStorage.key(i) !== 'loglevel:webpack-dev-server') {
                        this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));

                        // this.todoItems.push(localStorage.key(i));
                    }

                    // console.log(localStorage.key(i));
                }

            }
        }
    }
</script>

<style scoped>
    .checkBtnCompleted {
        color: #b3adad;
    }
    .textCompleted {
        text-decoration: line-through;
        color: #b3adad;
    }
</style>