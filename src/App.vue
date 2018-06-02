<template>
    <div id="app">
        <div>{{test()}}</div>
        <ul v-if="todos && todos.length">
            <li v-for="todo of todos">
                {{ todo.title }}
            </li>
        </ul>

    </div>
</template>

<script>
    import Arena from 'are.na';
    const arena = new Arena();

    export default {
        name: "App",
        data() {
            return {
                message: 'test',
                todos: []
            }
        },
        methods: {
            test() {
                window.console.log('test')
            },
        },
        mounted: function () {
            this.$nextTick(function () {
                arena.channel('arena-influences').get()
                    .then(chanel => {
                        chanel.contents.map(item => {
                            window.console.log(item.title);
                            this.todos.push(item)
                        })
                    })
                    .catch(err => window.console.log(err));
            })
        }
    }
</script>

<style>

</style>
