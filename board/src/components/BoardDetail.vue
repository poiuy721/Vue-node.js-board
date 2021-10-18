<template>
<section>
    <transition-group name="item" tag="ul">
        <img :key="item" :src="require(`@/assets/${propsdata.image}`)" width="200px" height="200px"/>
        <li :key="item">
            Id: {{propsdata.id}}
        </li>
        <li :key="item">
            Title: {{propsdata.title}}
        </li>
        <li :key="item">
            Content: {{propsdata.content}}
        </li>
        <li :key="item">
            Created At: {{propsdata.createdAt}}
        </li>
        <li :key="item">
            Updated At: {{propsdata.updatedAt}}
        </li>
        <div :key="item" class="closeContainer">
            <span class="closeBtn" @click="closeBoard">Close</span>
        </div>
        </transition-group>
</section>
</template>
<script>
export default{
    props:['propsdata'],
    data(){
        return {
            item:[]
        }
    },
    methods:{
        closeBoard(){
            this.$emit('closeBoard');
        }
    }
}
</script>
<style>
    ul{
        list-style-type: none;
        padding-left: 0px;
        margin-top: 0;
        text-align: left;
    }
    li{
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin:0.5rem 0;
        padding: 0 0.9rem;
        background:white;
        border-radius: 5px;
    }
.closeContainer{
    width: 8.5rem;
    height: 50px;
    line-height: 50px;
    background-color: white;
    border-radius: 5px;
    margin:0 auto;
    margin-top: 5px;
    text-align: center;
}
</style>
