<template>
    <div class="container">
        <input v-model="name">
        <input type="date" v-model="arrival_date" v-bind:min="min_date">
        <button v-on:click="todoAdd">追加</button>
        <div class="sort">
            <label for="sort">
                並び替え
            </label>
            <select id="sort" class="sorting" v-model.number="sortOrder">
                <option value="1">標準</option>
                <option value="2">日付が近い順</option>
            </select>
        </div>
        <ul>
            <li v-for="(todo,index) in list" v-bind:key="todo.id">
                {{todo.do}}: {{todo.date}}まで
                <button v-on:click="todoRemove(index)">削除</button>  
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'ToDo',
    data: function(){
        return {
        name: '',
        arrival_date: null,
        min_date: null,
        sortOrder: 1,
        list: []
        }
    },
    created: function(){
        var dt = new Date()
        dt.setDate(dt.getDate()+1)
        this.arrival_date = this.formatDate(dt)
        this.min_date = this.arrival_date
    },
    methods: {
        todoAdd: function(){
            var max = this.list.reduce(function(a,b){
                return a > b.id ? a : b.id
            },0)

            this.list.push({
                id: max+1,
                do: this.name,
                date: this.arrival_date
            })
        },
        todoRemove: function(index){
            this.list.splice(index,1)
        },
        formatDate: function(dt){
            var y = dt.getFullYear()
            var m = ('0'+(dt.getMonth()+1)).slice(-2)
            var d = ('0'+dt.getDate()).slice(-2)
            var result = y + '-' + m + '-' + d
            return result
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
