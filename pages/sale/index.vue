<template>
  <div align="center">
    <b-container fluid="md" class="bv-example-row">
      <b-row class="justify-content-md-center" id="b-row">
        <!-- Header -->
        <b-col col md="12"
          ><b-jumbotron bg-variant="danger" text-variant="white">
            <template #header>Vending Machine Problem</template>
            <template #lead>I GEAR GEEK</template>
          </b-jumbotron>
        </b-col>
      </b-row>

      <!-- insert coins -->
      <b-row align-h="center">
        <!-- ------------------------- -->
        <b-col md="12"
          ><h2>Insert coins</h2>
          <div class="insert" id="app">
            <b-button @click="append(1)" class="btn">Coins 1</b-button>
            <b-button @click="append(2)" class="btn">Coins 2</b-button>
            <b-button @click="append(5)" class="btn">Coins 5</b-button>
            <b-button @click="append(10)" class="btn">Coins 10</b-button>
            <b-button @click="clear" variant="warning">Clear</b-button>
            <b-button href="/" variant="danger">Exit</b-button>
            <h3>Total Coins : {{ total }}</h3>
            <div v-if="change != null">
              <h4>Change Coins : {{ change }}</h4>
            </div>
          </div>
        </b-col>
        <!-- ------------------------- -->
        <div align="center">
          <b-row align-h="center">
            <div v-for="pro in pro.data" :key="pro.data">
              <div v-if="pro.in_stock == true">
                <div v-if="total >= pro.price">
                  <b-col sm="12" align-self="start">
                    <b-card
                      :title="pro.name"
                      :img-src="pro.image"
                      img-alt="Image"
                      img-top
                      tag="article"
                      style="width: 15rem"
                      class="mb-2"
                      footer="product in stock"
                      img-height="200"
                      ><b-card-text>ราคา {{ pro.price }} บาท </b-card-text>
                      <b-button
                        @click="select(pro.price, total)"
                        variant="warning"
                        >Select</b-button
                      >
                    </b-card>
                  </b-col>
                </div>
              </div>
            </div>
          </b-row>
        </div>
        <!-- ------------- -->
      </b-row>

      <b-row id="b-row"> </b-row>
    </b-container>
  </div>
</template>



<script>
export default {
  data() {
    return {
      total: 0,
      change: null,
    };
  },
  methods: {
    clear() {
      this.total = 0;
    },
    append(number) {
      this.total = this.total + number;
    },
    select(number1, number2) {
      console.log("price : " + number1);
      console.log("total : " + number2);
      console.log("chang : " + (number2 - number1));

      this.change = number2 - number1;
      window.scrollTo(0, 0);
    },
  },
  async asyncData({ $axios }) {
    const pro = await $axios.$get(
      "https://www.mocky.io/v2/5c77c5b330000051009d64c9"
    );
    return { pro };
  },
};
</script>

<style scoped>
h3 {
  padding: 10px;
}

#b-row {
  margin: 10px;
}
.btn {
  margin-bottom: 10px;
}

.b-row {
  margin-top: 5%;
}

.data-product {
  width: 20rem;
  height: auto;
  border: 1px solid #4caf50;
  border-radius: 50px 20px;
  background-color: bisque;
}
h4 {
  padding: 10px;
  color:rebeccapurple;
}
</style>