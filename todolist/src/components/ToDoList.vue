<template>
    <div class="container">
        <div>
            <h2>Jquery To Do List</h2>
            <p>
                <em>Simple Todo List with adding and filter by diff status.</em>
            </p>
        </div>
        <div>
            <input class="input-text" type="text" name="ListItem" v-model="item"/>
            <div id="button" @click="addItem">Add</div>
        </div>
        <br/>
        <ol>
            <li v-for="item in itemList" :key="item.id" :id="uuid()"><input type="checkbox">{{item.content}}</li>
        </ol>
        <div>
            <ul id="filters">
                <li>
                    <a href="#" data-filter="all">ALL</a>
                </li>
                <li>
                    <a href="#" data-filter="active">Active</a>
                </li>
                <li>
                    <a href="#" data-filter="complete">Complete</a>
                </li>
            </ul>

        </div>
    </div>
</template>

<script>
export default {
    name:"ToDoList",
    data(){
        return{
            item:'',
            itemList:[]
        }
    },
    methods:{
        addItem(){
            if(this.item!=''){
                this.itemList.push({id:1,content:this.item});
                this.item='';
            }
        },
        uuid(){
            var s = [];
            var hexDigits = "0123456789abcdef";
           for (var i = 0; i < 36; i++) {
            s[i] = hexDigits.substr(Math.floor(Math.random() * 0x10), 1);
            }
            s[14] = "4"; 
            s[19] = hexDigits.substr((s[19] & 0x3) | 0x8, 1); 
            s[8] = s[13] = s[18] = s[23] = "-";
            var uuid = s.join("");
            return uuid;
        }
    }
}
</script>

<style>
    @import "../css/todolist.css";
</style>
