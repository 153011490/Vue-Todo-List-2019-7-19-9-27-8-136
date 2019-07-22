<template>
    <div>
        <ul id="filters">
                <li v-for="btn in btns" :key="btn.type">
                    <a href="#" @click="filter(btn.type,$event)" :class="btn.cls">{{btn.type}}</a>
                </li>
            </ul>
        
    </div>
</template>

<script>
export default {
    name:'Footer',
    data(){
        return {
            btns:[{type:'All',cls:'none'},
                {type:'Active',cls:'none'},
             {type:'Complete',cls:'none'}
            ]
        }
    },
    methods:{
        filter(type,e){
            this.btns.forEach(btn=>btn.cls='none');
            e.currentTarget.setAttribute('class','selected');
            this.$emit('filter',type);
        }
    }
}
</script>

<style>
 #filters{
     text-align: center;
     margin-bottom: -10px;
     margin-top: 40px;
 
 }

#filters li a {
    color: #fc999b;
    margin: 3px;
    padding: 3px 7px;
    text-decoration: none;
    border: 1px solid transparent;
    border-radius: 3px;
}

#filters li a.selected {
    border-color: rgba(175, 47, 47, 0.2);
}
#filters li a.selected, #filters li a:hover {
    border-color: rgba(175, 47, 47, 0.1);
}

#filters li {
	display: inline;
	margin: 0 0 5px 0;
	padding: 8px;
	list-style: none;
    outline: none;
 }
</style>
