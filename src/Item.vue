<template>
<div class="col-sm-4 item">
  <div class="card text-center" >
    <div>
      <img :src="item.thumbnail_url" alt="" class="card-img-top grow">
    </div>
    <div class="card-body">
      <h5 class="card-title">{{ item.title }}</h5>
      <h6 class="card-subtitle mb-2 remain">{{ item.quantity }} left in stock</h6>
      <p class="card-text">{{ item.description | shortDescription }}</p>
      <div class="row">
        <p class="col-6 lead">${{ item.price }}</p>
        <p class="col-6">
          <button class="btn btn-success" :disabled="item.quantity === 0" @click="addToCart(item)">
            Add to cart
          </button>
        </p>
      </div>
    </div>
  </div>
</div>
</template>

<script>

export default {
    name: 'item',
    props: ['item'],
    data() {
        return {
            size: ''
        }
    },
    filters: {
        shortDescription(value) {
        if (value && value.length > 70) {
            return value.substring(0, 70) + '...';
        } else {
            return value;
        }
        }
    },
    methods: {
        addToCart(item) {
            this.$store.commit('addToCart',item)
        }
    }
}
</script>

<style scoped>

.remain {
  color: #d17581;
}

.grow {
  width: 90%;
  height: 90%;
  padding: 15px;
  transition: all .2s ease-in-out;
}

.grow:hover {
  transform: scale(1.1);
}

.item {
    display: flex;
    content: "";
    padding: 10px 10px;
}

</style>