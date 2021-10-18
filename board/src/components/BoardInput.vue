<template>
    <div class="inputBox shadow">
        <form method="POST" id="registForm" enctype="multipart/form-data">
            <input class="inputTitle" type="text" v-model="newTitle" placeholder="Title" v-on:keyup.enter="createBoard">
            <input class="inputContent" type="text" v-model="newContent" placeholder="Content" v-on:keyup.enter="createBoard">
            <input class="inputImage" type='file' ref="serveyImage" @change="onSelect">
            <span class="addContainer" v-on:click="createBoard">
                <i class="addBtn fas fa-plus" aria-hidden="true"></i>
            </span>
        </form>
        <modal v-if="showModal" @close="showModal=false">
            <h3 slot="header">경고</h3>
            <span slot="footer" @click="showModal=false">
                내용을 입력하세요.
                <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
            </span>
        </modal>
    </div>
</template>

<script>
import Modal from './common/Modal.vue'
export default{
    data(){
        return{
            newTitle:'',
            newContent:'',
            newFile:'',
            showModal:false,
        }
    },
    methods:{
        onSelect(){
            const file=this.$refs.serveyImage.files[0]
            this.newFile=file;
        },
        createBoard(){
            if(this.newTitle!==""&&this.newContent!==""){
                const form=new FormData()
                var title=this.newTitle&&this.newTitle.trim();
                var content=this.newContent&&this.newContent.trim();
                form.append('title',title)
                form.append('content',content)
                form.append('file',this.newFile)
                this.$emit('createBoard',form);
                this.clearInput();
                console.log("create 1")
            }else{
                this.showModal=!this.showModal;
            }
        },
        clearInput(){
            this.newTitle='';
            this.newContent='';
        }
    },
    components:{
        Modal:Modal
    }
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
