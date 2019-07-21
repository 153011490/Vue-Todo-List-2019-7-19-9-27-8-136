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
            <li v-for="(item,index) in itemList" :key="item.id" :id="uuid()" :ref="item" :class="{'checked':isChecked[index]}"><input type="checkbox" @click="itemChecked(index)"><span>{{item.content}}</span></li>
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
import { isIP } from 'net';
export default {
    name:"ToDoList",
    data(){
        return{
            item:'',
            itemList:[],
            isChecked:[]
        }
    },
    methods:{
        addItem(){
            if(this.item!=''){
                this.itemList.push({id:this.itemList.length,content:this.item});
                this.isChecked.push(false);
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
        },
        itemChecked(index){
            this.isChecked[index]=!this.isChecked[index];
            this.$forceUpdate();
        }
    }
}
</script>

<style>
    @import "../css/todolist.css";
</style>
