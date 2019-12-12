<template>
    <div>
    <Modal :mask-closable="false"
            v-model="inputModal"
            title="Common Modal dialog box title"
            @on-ok="onOk"
            :on-open-model="inputModal=true"
            @on-cancel="onCancel"
           width="360">
        <p slot="header" style="color:#f60;text-align:center">
            <Icon type="ios-information-circle"></Icon>
            <span>修改内容</span>
        </p>
        <div style="text-align:center">
            <!--<p>原有内容 {{this.toDoList}}</p>-->
            <p>修改内容 <Input v-model="inpVal" placeholder="请输入你想要修改的内容" style="width: 200px" /></p>
        </div>
        <div slot="footer">
            <Button type="error"   @click="del">确定</Button>
            <Button type="success"   @click="del">取消</Button>
        </div>
    </Modal>
    </div>
</template>

<script>
    export default {
        props:[
            // 'toDoList'
        ],
        name: "TodoModal",
        date(){
            return{
                inputModal:false,
                inpVal:'',//输入框值
                EditSj:'',
            }
        },
        mounted(){
            // console.log(this.toDoList)
        },
        methods:{
            //隐藏
            onCancel(){
                this.$emit('on-close-cancel',false)
            },
            onOk(){
                this.$emit('on-close-cancel',true)
            },
            del(){
                // console.log(this.inpVal)
                // this.$emit('editeItem',this.EditSj)
                if (!this.inpVal){
                    this.$Message.success('请输入内容');
                }else{
                    // setTimeout(() => {
                    this.onCancel();
                    this.$Message.error('修改失败');
                    // }, 2000);
                }
            }
        }
    }
</script>

<style scoped>
.modal{
    background-color: yellow;
    margin-top: 200px;
    tabindex:"-1"
}
</style>
