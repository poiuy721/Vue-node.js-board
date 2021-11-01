<template>
<section>
    <ul v-if="propsdata.image">
        <img v-if="propsdata.image.endsWith('.jpg')" :src='`http://localhost:3000/image/${propsdata.image}`' width="200px" height="200px"/>
        <img v-else :src='`http://localhost:3000/image/noImage.jpg`'  width="200px" height="200px"/>
        <li>
            Id: {{propsdata.id}}
        </li>
        <li>
            Title: {{propsdata.title}}
        </li>
        <li>
            Content: {{propsdata.content}}
        </li>
        <li>
            Created At: {{this.formatDate(propsdata.createdAt)}}
        </li>
        <li>
            Updated At: {{this.formatDate(propsdata.updatedAt)}}
        </li>
        <div class="closeContainer">
            <span class="closeBtn" @click="closeBoard">Close</span>
        </div>
        </ul>
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
        formatDate(date) {
            const tmpDate=new Date(date)
            return tmpDate.getFullYear() + '/' + 
                (tmpDate.getMonth() + 1) + '/' + 
                tmpDate.getDate() + '   ' + 
                tmpDate.getHours() + ':' + 
                tmpDate.getMinutes() + '';
        },
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
