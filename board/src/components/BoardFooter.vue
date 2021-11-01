<template>
<div>
    <div class="registBtnContainer">
        <span class="registBtn" @click="showRegist">Regist</span>
    </div>
    <div class="clearAllContainer">
        <span class="clearAllBtn" @click="clearAll">Clear All</span>
    </div>
</div>
</template>

<script>
export default{
    methods:{
        showRegist(){
            this.$emit('showRegist');
        },
        clearAll(){
            this.$emit('clearAll');
        }
    }
}
</script>

<style scoped>
.registBtnContainer{
    width: 8.5rem;
    height: 50px;
    line-height: 50px;
    background-color: white;
    border-radius: 5px;
    margin:0 auto;
    margin-top: 5px;
}
.clearAllContainer{
    width: 8.5rem;
    height: 50px;
    line-height: 50px;
    background-color: white;
    border-radius: 5px;
    margin:0 auto;
    margin-top: 5px;
}
.clearAllBtn{
    color: #e20303;
    display: block;
}

</style>
