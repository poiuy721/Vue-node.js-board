<template>
    <div id="app">
      <BoardHeader></BoardHeader>
      <BoardList :propsdata="items" @deleteBoard="deleteBoard" @openEditBoard="openEditBoard" @readOne="readOne"></BoardList>
      <BoardDetail @closeBoard="closeBoard" :propsdata="item" v-show="detailFlag"></BoardDetail>
      <BoardInput class="BoardInput" @createBoard="createBoard" v-show="registFlag"></BoardInput>
      <BoardEdit class="BoardEdit" :boardId="boardId" @editBoard="editBoard" v-show="editFlag"></BoardEdit>
      <BoardFooter @clearAll="clearAll" @showRegist="showRegistForm"></BoardFooter>

    </div>
</template>

<script>
import BoardHeader from './components/BoardHeader.vue'
import BoardInput from './components/BoardInput.vue'
import BoardList from './components/BoardList.vue'
import BoardEdit from './components/BoardEdit.vue'
import BoardDetail from './components/BoardDetail.vue'
import BoardFooter from './components/BoardFooter.vue'
import axios from 'axios'
export default{
  data(){
    return {
      registFlag:false,
      detailFlag:false,
      editFlag:false,
      items:[],
      item:[],
      boardId:''
    }
  },
  created(){
      this.read()
      }
    ,
  methods:{
    read(){
      axios.get('http://localhost:3000/restapi/board/').then((res)=>{
        this.items=res.data
      })
    },
    readOne(boardId){
      axios.get('http://localhost:3000/restapi/board/'+boardId).then((res)=>{
        this.item=res.data[0]
        this.detailFlag=true;
      })
    },
    createBoard(form){
      axios.post('http://localhost:3000/restapi/board/',form,{
        headers: { 'Content-Type': 'multipart/form-data' }
      }).then((res)=>{
        this.$router.go();
      })
    },
    openEditBoard(boardId){
      this.boardId=boardId;
      if(this.editFlag==false)
        this.editFlag=true;
      else
        this.editFlag=false;
    },
    editBoard(form,boardId){
      axios.put('http://localhost:3000/restapi/board/'+boardId,form,{
        headers: { 'Content-Type': 'multipart/form-data' }
      }).then((res)=>{
        this.$router.go();
      })
    },
    deleteBoard(boardId){
      axios.delete('http://localhost:3000/restapi/board/'+boardId).then((res)=>{
        this.$router.go();
      })
    },
    clearAll(){
      axios.delete('http://localhost:3000/restapi/board/').then((res)=>{
        this.$router.go();
      })
    },
    showRegistForm(){
      if(this.registFlag==false)
        this.registFlag=true;
      else
        this.registFlag=false;
    },
    closeBoard(){
      this.detailFlag=false;
    }
  },
  components:{
    'BoardHeader':BoardHeader,
    'BoardInput':BoardInput,    
    'BoardList':BoardList,   
    'BoardDetail':BoardDetail, 
    'BoardEdit':BoardEdit, 
    'BoardFooter':BoardFooter
  }
}
</script>

<style>

    body{
        text-align: center;
        background-color: #F6F6F8;
    }
    input{
        border-style: groove;
        width: 200px;
    }
    button{
        border-style: groove;
    }
    .shadow{
        box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
    }
</style>
