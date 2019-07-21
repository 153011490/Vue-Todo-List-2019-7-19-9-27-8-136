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
            <li v-for="(item,index) in filter(type)" :key="index" :id="uuid()" :ref="item" :class="{'checked':filter(type)[index].flag}"><input type="checkbox" @click="itemChecked(index)" :checked="filter(type)[index].flag"><span @dblclick="changeItem($event)"  @keydown.enter="change(item,$event)">{{item.content}}</span></li>
        </ol>
        <div>
            <ul id="filters">
                <li>
                    <a href="#" data-filter="all" @click="changeType('all')" ref="all" :class="{'selected':aClass===1}">ALL</a>
                </li>
                <li>
                    <a href="#" data-filter="active"  @click="changeType('active')" ref="active" :class="{'selected':aClass===2}">Active</a>
                </li>
                <li>
                    <a href="#" data-filter="complete" @click="changeType('complete')" ref="complete" :class="{'selected':aClass===3}">Complete</a>
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
            type:'all',
            aClass:''
        }
    },
    methods:{
        addItem(){
            if(this.item!=''){
                this.itemList.push({flag:false,content:this.item});
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
            this.itemList[index].flag=!this.itemList[index].flag;
            this.$forceUpdate();
        },
        filter(type){
            if(type=='all'){
                this.aClass=1;
                return this.itemList;
            }
            else if(type=='active'){
              this.aClass=2;
               return this.itemList.filter((item,index)=>!this.itemList[index].flag);
            }else{
                this.aClass=3;
              return this.itemList.filter((item,index)=>this.itemList[index].flag);
            }
        },
        changeType(type){
            this.type=type;
        },
        changeItem(e){
            e.currentTarget.setAttribute('contenteditable',true);
            e.currentTarget.click;
        },
        change(item,e){
            item.content=e.currentTarget.innerText;
            e.currentTarget.setAttribute('contenteditable',false);
        }
    }
}
</script>

<style>
    @import "../css/todolist.css";
</style>
