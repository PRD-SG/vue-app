<template >
  <div align="center">
    <b-container fluid class="bv-example-row">
      <b-row id="jumbotron">
        <b-col col md="12"
          ><b-jumbotron bg-variant="primary" text-variant="white">
            <template #header>Vending Machine Problem</template>
          </b-jumbotron></b-col>
      </b-row>
    <div v-if="sale != true">
      <b-row>
        <b-col col md="12">
            <b-button @click="selectproduct" variant="danger">กดเพื่อทำการซื้อ</b-button>
        </b-col>
      </b-row>
      
      <h3>Product in stock</h3>
        <b-row align-h="center">
          <div v-for="pro in pro.data" :key="pro.data">
            <div v-if="pro.in_stock == true">
              <b-col md="12">
                <b-card
                  :title="pro.name"
                  :img-src="pro.image"
                  img-alt="Image"
                  img-top
                  tag="article"
                  style="width: 15rem"
                  class="mb-2"
                  footer="Product in stock"
                  img-height="200"
                >
                  <b-card-text>ราคา {{pro.price}} บาท</b-card-text>
                </b-card>
              </b-col>
            </div>
          </div>
        </b-row>
        </div>
        <div v-else>
            
      <!-- insert coins -->
      <b-row align-h="center">
        <b-col md="12"
          ><h2>Insert coins</h2>
          <div class="insert">
            <b-button @click="append(1)" class="btn">Coins 1</b-button>
            <b-button @click="append(2)" class="btn">Coins 2</b-button>
            <b-button @click="append(5)" class="btn">Coins 5</b-button>
            <b-button @click="append(10)" class="btn">Coins 10</b-button>
            <b-button @click="clear" variant="warning">Clear</b-button>
            <b-button @click="exit" variant="danger">Exit</b-button>
            <div class="ale" v-if="change == null">
              <b-alert show variant="primary">
                Total Coins : {{ total }} Baht</b-alert>
            </div>

            <div class="ale" v-if="change != null">
                <b-alert show variant="danger">
                 Change Money : {{ change }} Baht
                </b-alert>
                <p>Auto reload 5 Second</p>
            </div>
          </div>
        </b-col>
        <!-- insert coins -->
        <div align="center">
          <b-row align-h="center">
            <!-- select data  -->
            <div v-for="pro in pro.data" :key="pro.data">
              <div v-if="pro.in_stock == true">
                <div v-if="total >= pro.price">
                  <!-- select data  -->
                  <!-- show data -->
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
                        variant="warning">Select</b-button>
                    </b-card>
                  </b-col>
                </div>
              </div>
            </div>
          </b-row>
        </div>
        <!-- show data -->
      </b-row>
        </div>
    </b-container>
  </div>
</template>



<script>
export default {
  data() {
    return {
      total: 0,
      change: null,
      sale: false,
      time: 5,
    };
  },
  methods: {
    clear() {
      this.total = 0;
      this.change = null;
    },
    append(number) {
      this.total = this.total + number;
    },
    select(number1, number2) {
      console.log("price : " + number1);
      console.log("total : " + number2);
      console.log("chang : " + (number2 - number1));
      this.total = 0;
      this.change = number2 - number1;
      window.scrollTo(0, 0);
      setTimeout(function(){ 
        location.reload(); 
      }, 5000);
      
    },
    selectproduct() {
        this.sale = true;
    },
    exit() {
        this.sale = false;
        this.change = null;
        this.total = 0;
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
.ale {
  max-width: 15rem;
}
.btn {
  margin-bottom: 10px;
}
#jumbotron {
  margin: 10px;
}
h3 {
  padding: 10px;
}
</style>