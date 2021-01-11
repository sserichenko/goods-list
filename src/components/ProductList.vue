<template>
  <div class="product-list">
    <div class="flex top-information">
      <h1>Перечень столов</h1>
    </div>
    
    <ul class="list-default flex">
      <li
        v-for="(product, index) in products"
        :key="index"
      >
        <product-card
          :title="product.title"
          :price="product.price"
          :img-url="product.imgUrl"
          :aviable-count="product.aviableCount"
          @addToBasket="addToBasket"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import ProductCard from './ProductCard'

export default {
  name: 'ProductList',
  components: { ProductCard },
  data() {
    return {
      searchText: '',
      totalPrice: 0,
      products: [
        {
          title: 'Стол "Конструктор"',
          price: 3500,
          imgUrl: 'https://hoff.ru/upload/iblock/8c9/8c989500ee8639b9e3aa267b1888b4af.jpg',
          aviableCount: 8
        },
        {
          title: 'Стол "Кухонный"',
          price: 2100,
          imgUrl: 'https://hoff.ru/upload/iblock/af2/af2d37161f217d4f489373be7da4a7a0.jpg',
          aviableCount: 11
        },
        {
          title: 'Стол "Письменный"',
          price: 4250,
          imgUrl: 'https://hoff.ru/upload/iblock/1cc/1ccb33b50e3e9cfa08629bf455e41855.jpg',
          aviableCount: 4
        },
      ]
    }
  },
  methods: {
    addToBasket(totalPrice, price) {
      totalPrice === 1?this.totalPrice = price:this.totalPrice = totalPrice;
      alert(`Вы добавили в корзину товаров на ${this.totalPrice} грн.`)
      }
    }
}
</script>

<style scoped>

li {
  margin-right: 20px;
}
.top-information {
align-items: center;
}
.top-information h1 {
  margin-bottom: 30px;
}
.top-information button {
  background-color: rgb(221, 56, 56);
  color: #fff;
  border: none;
  border-radius: 4px;
  padding: 8px 14px;
  display: block;
  cursor: pointer;
  margin-left: 10px;
}
</style>
