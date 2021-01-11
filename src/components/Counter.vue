<template>
    <div>
        <button
            class="decreise-button"
            type="button"
            @click="decreaseCount"
        >
        -
        </button>
        <input 
        type="number"
        class="count-input"
        :value="count"
        :min="minCount"
        :max="maxCount"       
        />
        <button
            class="increise-button"
            type="button"
            @click="increaseCount"
        >
        +
        </button>
    </div>
</template>

<script>
export default {
    name: "Counter",
    data(){
        return{
            maxCount: this.aviableCount,
            minCount: 1,
        }
    },
     props: {
        count: {
            type: Number,
            default: 1
    },
     aviableCount: {
      type: Number,
      default: 10
    }
  },
    methods:{
        increaseCount(){
            if(this.count < this.maxCount){
                this.$emit('increaseCount')
            }
        },
        decreaseCount(){
            if(this.count > this.minCount){
                this.$emit('decreaseCount')
            }

        }
    }
}
</script>

<style scoped>
.increise-button, .decreise-button{
    width: 30px;
    height: 30px;
    border-radius: 50%;
    border: 1px solid grey;
    background: transparent;
    color: grey;
    font-weight: 700;
    margin-right: 6px;
    padding: 0;
}
.count-input{
    width: 30px;
    height: 30px;
    padding: 0;
    background: transparent;
    color:grey;
    border: grey;
}
</style>