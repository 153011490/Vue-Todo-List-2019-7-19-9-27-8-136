<template>
    <div>
        <InputBar @outputList="outputList"></InputBar>
        <ListContainer :list="list" ref="listContainer"></ListContainer>
    </div>
</template>

<script>
import InputBar from './InputBar.vue';
import ListContainer from './ListContainer.vue';
export default {
    name:'Body',
    components:{
        InputBar,
        ListContainer
    },
    data(){
        return{
            list:[]
        }
    },
    methods:{
        outputList(inputList){
            this.list=inputList;
        },
        changeType(type){
            this.$refs.listContainer.changeType(type);
        }
    }
}
</script>
