<template>
  <div align="center">
    <b-container fluid="md" class="bv-example-row">
      <b-row class="justify-content-md-center" id="b-row">
        <b-col col md="12"
          ><b-jumbotron bg-variant="danger" text-variant="white">
            <template #header>Vending Machine Problem</template>
            <template #lead>I GEAR GEEK</template>
          </b-jumbotron></b-col
        >
      </b-row>

      <b-row id="b-row">
        <b-col col md="12">
          <h2>Insert coins</h2>
          <div class="insert" id="app">
            <b-button @click="append(1)" class="btn">Coins 1</b-button>
            <b-button @click="append(2)" class="btn">Coins 2</b-button>
            <b-button @click="append(5)" class="btn">Coins 5</b-button>
            <b-button @click="append(10)" class="btn">Coins 10</b-button>
            <b-button @click="clear" variant="warning">Clear</b-button>
            <b-button href="/" variant="danger">Exit</b-button>
            <h3>Total Coins : {{ total }}</h3>
            <b-row id="b-row">
              <div v-for="pro in pro.data" :key="pro.data">
                <div class="pro-info" v-if="pro.in_stock == true">
                  <div class="pro-info" v-if="total >= pro.price">
                    <b-col col lg="12">
                      <div class="product" align="center">
                        <h4>ชื่อสินค้า : {{ pro.name }}</h4>
                        <h4>ราคา : {{ pro.price }} บาท</h4>
                        <img :src="pro.image" />
                      </div>
                    </b-col>
                  </div>
                </div>
              </div>
            </b-row>
          </div>
        </b-col>
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
    };
  },
  methods: {
    clear() {
      this.total = 0;
    },
    append(number) {
      this.total = this.total + number;
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
ß
<style scoped>
#b-row {
  margin: 1%;
}

.b-row {
  margin-top: 5%;
}

.product {
  background-color: #ffedda;
  border-radius: 10px;
  padding: 10px;
  margin-top: 5%;
  height: 400px;
}

img {
  border-radius: 10px;
  width: 100;
}
</style>