<template>
  <div align="center">
    <b-container fluid="md" class="bv-example-row">
      <b-row class="justify-content-md-center" id="b-row">
        <b-col col md="12"
          ><b-jumbotron bg-variant="primary" text-variant="white">
            <template #header>Vending Machine Problem</template>
            <template #lead>I GEAR GEEK</template>
          </b-jumbotron></b-col
        >
      </b-row>

      <b-row id="b-row">
        <b-col col md="12"
          ><b-button href="/sale" variant="danger"
            >กดเพื่อทำการซื้อ</b-button
          ></b-col
        >
      </b-row>

      <b-row id="b-row">
        <div v-for="pro in pro.data" :key="pro.data">
          <div class="pro-info" v-if="pro.in_stock == true">
            <b-col col lg="12">
                <div class="product" align="center">
                  <h4>ชื่อสินค้า : {{ pro.name }}</h4>
                  <h4>ราคา : {{ pro.price }} บาท</h4>
                  <img :src="pro.image" />
              </div>
            </b-col>
          </div>
        </div>
      </b-row>
    </b-container>
  </div>
</template>



<script>
export default {
  async asyncData({ $axios }) {
    const pro = await $axios.$get(
      "https://www.mocky.io/v2/5c77c5b330000051009d64c9"
    );
    return { pro };
  },
};
</script>

<style scoped>
#b-row {
  margin: 1%;
}

.b-row {
  margin-top: 5%;
}

.product {
  background-color: #FFEDDA;
  border-radius: 10px;
  padding: 15px;
  margin-top: 5%;
  height: 400px;
}

img {
  border-radius: 10px;
  width: 100;
}

</style>