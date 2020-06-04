<template>
    <div>
        <span>
            <span v-on:click="clearTodo">Clear All</span>
        </span>
    </div>
</template>

<script>
    export default {
        methods: {
            clearTodo: function() {
                localStorage.clear();
            }
        }
    }
</script>

<style scoped>

</style>