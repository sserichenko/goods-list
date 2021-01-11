<template>
<div class="modal__wrapper" ref="popup_wrapper">
     <div class="modal">
        <div class="modal__header">
            <span>{{productInfoTitle}}</span>
            <span
            class="close-button"
            @click="closePopup"
            >&times;</span>
        </div>
        <div class="modal__content">
            <slot></slot>
        </div>
        <div class="modal__footer">
            <button
            class="close_modal"
            @click="closePopup"
            >
            Close</button>
            
            <button
            class="submit_btn"
            @click="rightButtonAction"
            >
            {{rightButtonTitle}}
            </button>
            
        </div>
    </div>
</div>
   
</template>

<script>
export default {
    name: 'Modal',
    props: {
        rightButtonTitle: {
            type: String,
            default: 'Ok'
        },
        productInfoTitle: {
            type: String,
            default: 'Информация'
        },
        totalPrice: {
            type: Number,
            default: 0
    },
    },
    data(){
        return{

        }
    },
    methods: {
        closePopup(){
            this.$emit('closePopup')
        },
        rightButtonAction(){
            this.$emit('rightButtonAction')
        }
    },
    mounted(){
        let inner = this;
        document.addEventListener('click', function(item){
            if(item.target === inner.$refs['popup_wrapper']){
                inner.closePopup();
            }
        })
    }
}
</script>

<style scoped>
.modal__wrapper{
    background: rgba(0,0,0, .7);
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
}
.modal{
    padding: 20px;
    position: fixed;
    z-index: 5;
    background: #ffffff;
    top: 60px;
    width: 400px;
    box-shadow: 0 0 17px 0 #e7e7e7;
}
.close-button{
    cursor: pointer;
}
.modal__header, .modal__footer{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.modal__content{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
}
.submit_btn{
    background-color: rgb(38, 124, 12);
    color: #fff;
    border: none;
    border-radius: 4px;
    padding: 8px 14px;
    display: block;
    cursor: pointer;
    margin-top: 20px;
}
.close_modal{
    background-color: red;
    color: #fff;
    border: none;
    border-radius: 4px;
    padding: 8px 14px;
    display: block;
    cursor: pointer;
    margin-top: 20px;
}
</style>