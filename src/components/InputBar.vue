<template>
    <div>
        <input type="text" class="input-text" v-model="item" @keypress.enter="outputList">
        <div id="button" @click="outputList">Add</div>
    </div>
</template>

<script>
export default {
    name:'InputBar',
    data(){
        return {
            item:'',
            toDoList:[]
        }
    },
    methods:{
        outputList(){
            this.toDoList.push({content:this.item,status:false});
            this.$emit('outputList',this.toDoList);
        }
    }
}
</script>

<style>
.input-text{
    width: 70%;
}
#button{
display: inline-block;
background-color:#fc999b;
color:#ffffff;
border-radius: 5px;
text-align:center;
margin-top:2px;
padding: 5px 15px;
}
input{
padding: 4px 15px 4px 0;
}
#button:hover{
cursor: pointer;
opacity: .8;
}
</style>


