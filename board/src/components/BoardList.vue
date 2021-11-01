<template>
    <section>
        <ul>
            <li>
                <label class="leftLabel">Image</label>
                <label class="leftLabel">Title</label>
                <label class="leftLabel">Content</label>
                <label class="emptyLabel"></label>
                <label class="rightLabel">Edit</label>
                <label class="rightLabel">Delete</label>
            </li>
        </ul>
        <transition-group name="list" tag="ul">
            <li v-for="board in propsdata" :key="board.id" class="shadow">
                <img v-if="board.image.endsWith('.jpg')" :src='`http://localhost:3000/image/${board.image}`' width="70px" height="50px"  @click="readOne(board.id)"/>
                <img v-else :src='`http://localhost:3000/image/noImage.jpg`'  width="70px" height="50px"  @click="readOne(board.id)"/>
                <a name="title"  @click="readOne(board.id)">{{board.title}}</a>
                <a name="content" @click="readOne(board.id)">{{board.content}}</a>
                <span class="editBtn" type="button" @click="editBoard(board.id)">
                    <i class="far fa-edit" aria-hidden="true"></i>
                </span>
                <span class="removeBtn" type="button" @click="deleteBoard(board.id)">
                    <i class="far fa-trash-alt" aria-hidden="true"></i>
                </span>
            </li>
        </transition-group>
    </section>
</template>

<script>
export default{
    props:['propsdata'],
    data(){
        return {
            items:[]
        }
    },
    methods:{
        editBoard(boardId){
            this.$emit('openEditBoard',boardId);
        },
        deleteBoard(boardId){
            this.$emit('deleteBoard',boardId);
        },
        readOne(boardId){
            this.$emit('readOne',boardId);
        }
    }
}
</script>

<style scoped>
    label{
        font-weight: bold;
        width: 100px;
    }
    .leftLabel{
        text-align: left;
    }
    .emptyLabel{
        width:70%;
    }
    .rightLabel{
        float: right;
        margin-left:0;
        text-align:center
    }
    i{
        width: 30px;
    }
    a{
        display: inline-block;
        width: 100px;
        text-align: center;
    }
    .list-enter-active, .list-leave-active{
        transition: all 1s;
    }
    .list-enter, .list-leave-to{
        opacity:0;
        transform: translateY(30px);
    }
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
    .checkBtn{
        line-height: 45px;
        color: #62acde;
        margin-right: 5px;
    }
    .editBtn{
        width: 50px;
        margin-left: auto;
        color: blue;
    }
    .removeBtn{
        width: 100px;
        text-align: center;
        color: #de4343;
    }
</style>
