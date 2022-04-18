<template>
  <div>
    <h1>Products</h1>
    <p>{{ num }}</p>
    <p>{{ num2 }}</p>
    <div>
      <input type="num" id="one" />
      <input type="num" id="two" />
      <button @click="inp">click</button>
    </div>
    <div v-for="p in Poduct" :key="p.id" class="cart">
      <p>{{ p.title }}</p>
      <p>{{ p.price }}</p>
      <!-- <img :src="'http://localhost:8055/assets/' + p.image.id" alt="" /> -->
    </div>
  </div>
</template>

<script>
import gql from "graphql-tag";
export default {
  apollo: {
    Poduct: {
      query: gql`
        query product {
          Poduct {
            title
            price
          }
        }
      `,
      variables() {
        return {
          gte: this.num,
          lte: this.num2,
        };
      },
    },
  },
  data() {
    return {
      num: 1,
      num2: 100000000,
    };
  },
  methods: {
    move(id) {
      this.$router.push("/products/" + id);
    },
    inp() {
      this.num = document.querySelector("#one").value;
      this.num2 = document.getElementById("two").value;
    },
  },
};
</script>

<style scoped>
.cart {
  border: 1px solid black;
  padding: 10px;
}
</style>