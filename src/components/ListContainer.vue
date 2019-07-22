<template>
    <div>
        <ol>
           <li v-for="(item,index) in filter(type)" :key="item.content">
               <input type="checkbox" @click="itemChecked(index)" :checked="item.status">
               <span @dblclick="modify($event)" @keydown.enter="update($event,item)" ref="span" :class="item.status?'checked':''">
                   {{item.content}}
                </span>
                </li> 
        </ol>
    </div>
</template>

<script>
export default {
    name:'ListContainer',
    props:['list'],
    data(){
        return{
            type:'All'
        }
    },
    methods:{
        modify(e){
            e.currentTarget.setAttribute('contenteditable',true);
        },
        update(e,item){
            item.content=e.currentTarget.innerText;
            e.currentTarget.setAttribute('contenteditable',false);
        },
        itemChecked(index){
            this.list[index].status=!this.list[index].status;
            this.$forceUpdate();
        },
         filter(param){
            if(param==='All')return this.list;
            else if(param==='Active') return this.list.filter(item=>!item.status);
            else return this.list.filter(item=>item.status);
        },
        changeType(param){
            this.type=param;
        }
    }
}
</script>

<style>
ol {
    padding-left: 25px;
}

ol li:nth-child(even){
    width:350px;
    background: lightgreen;
}

li:hover{
  cursor: pointer;
 }

 .checked {
    color: #999;
    text-decoration: line-through;
}

</style>
