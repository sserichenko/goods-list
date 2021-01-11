<template>
  <div class="product-card">

    <modal
    v-if="isInfoPopupVisible"
    @closePopup="closePopup"
    :totalPrice="totalPrice"
    rightButtonTitle="Add to card"
    productInfoTitle="Информация о товаре"
    @rightButtonAction="addToBasket"
    >
    <img :src="imgUrl">
    <h2>{{ title }}</h2>
    <br>
    <p> Стоимость за штуку - {{ price }} грн.</p>
    <p>Общая сумма покупки - {{totalPrice === 1?price:totalPrice}} грн.</p>
    <div class="counter__wrapper">
      <Counter 
      :count="count"
        :aviableCount="aviableCount"
        @decreaseCount="decreaseCount"
        @increaseCount="increaseCount"
      
      />
    </div>
    </modal>
    
  

    <img
      :src="imgUrl" 
    >
    <div class="product-card__info">
      <h2>{{ title }}</h2>
      <p class="price">{{ price }} грн.</p>
      <p class="count">Доступно для покупки {{ aviableCount }} шт.</p>
      <div class="counter__wrapper">
        <Counter 
        :count="count"
        :aviableCount="aviableCount"
        @decreaseCount="decreaseCount"
        @increaseCount="increaseCount"
        />
      </div>
      <button class="add-to-card" type="button" @click="addToBasket"> Добавить в корзину</button>
      <button
      class="show_info"
      @click="showPopupInfo"
     
      >
       Информация
      </button>
    </div>
  </div>
</template>

<script>
import Modal from './Modal.vue';
import Counter from './Counter.vue'
export default {
  name: 'ProductCard',
  props: {
    title: {
      type: String,
    },
    price: {
      type: Number,
      required: true
    },
    imgUrl: {
      type: String,
      default: 'https://tsum.by/images/no-photo.png'
    },
    aviableCount: {
      type: Number,
      default: 10
    },
  },
  data(){
    return {
      isInfoPopupVisible: false,
      count: 1,
      totalPrice: 1
    }
  },
  components: {
    Modal,
    Counter
  },
  methods: {
    addToBasket() {
      this.$emit('addToBasket', this.totalPrice, this.price)
    },
    showPopupInfo(){
      this.isInfoPopupVisible = true;
    },
    closePopup(){
      this.isInfoPopupVisible = false;
    },
    decreaseCount(){
      this.count--
      this.totalPrice = this.count * this.price
    },
    increaseCount(){
      this.count++
      this.totalPrice = this.count * this.price
    }
  }
}
</script>

<style scoped>
.product-card {
  border: 1px solid rgb(211, 211, 211);
  padding: 20px 15px;
}
.product-card img{
  width: 250px;
}
.product-card__info {
  margin-top: 20px;
}
.product-card__info h2,  .product-card__info .price {
  font-weight: 500;
}
.product-card__info .count {
  color: rgb(143, 143, 143);
}
.product-card__info .add-to-card {
  background-color: rgb(221, 56, 56);
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 8px 14px;
  display: block;
  cursor: pointer;
  margin-top: 20px;
}
.show_info{
  background-color: rgb(37, 81, 224);
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 8px 14px;
  display: block;
  cursor: pointer;
  margin-top: 20px;
}
.counter__wrapper{
  display: flex;
  justify-content: flex-start;
  align-items: center;
  width: 50%;
}
</style>
