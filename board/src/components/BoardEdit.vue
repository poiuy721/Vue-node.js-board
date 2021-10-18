<template>
    <div class="inputBox shadow">
        <form method="POST" id="editForm" enctype="multipart/form-data">
            <input class="editTitle" type="text" v-model="editTitle" placeholder="Title" v-on:keyup.enter="createBoard">
            <input class="editContent" type="text" v-model="editContent" placeholder="Content" v-on:keyup.enter="createBoard">
            <input class="editImage" type='file' ref="serveyImage" @change="onSelect">
            <span class="addContainer" v-on:click="editBoard">
                <i class="addBtn fas fa-plus" aria-hidden="true"></i>
            </span>
        </form>
    </div>
</template>

<script>
export default{
    data(){
        return{
            editTitle:'',
            editContent:'',
            editFile:'',
        }
    },
    props:["boardId"],
    methods:{
        onSelect(){
            const file=this.$refs.serveyImage.files[0]
            this.editFile=file;
        },
        editBoard(){
                const form=new FormData()
                var title=this.editTitle&&this.editTitle.trim();
                var content=this.editContent&&this.editContent.trim();
                form.append('title',title)
                form.append('content',content)
                form.append('file',this.editFile)
                this.$emit('editBoard',form,this.boardId);
                this.clearInput();
                console.log("edit 1")
        },
        clearInput(){
            this.editTitle='';
            this.editContent='';
        }
    },
}
</script>

<style scoped>
input{
    text-align: center;
}
input:focus{
    outline: none;
}
.inputBox{
    background:white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input{
    border-style: none;
    font-size: 0.9rem;
}
.addContainer{
    float: right;
    background:linear-gradient(to right, #6478FB,#8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn{
    color: white;
    vertical-align: middle;
}

</style>
