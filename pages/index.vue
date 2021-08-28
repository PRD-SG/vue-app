<template>
  <div align="center">
    <b-container fluid="md" class="bv-example-row">
      <b-row align-h="center" id="b-row">
        <b-col col md="12"
          ><b-jumbotron bg-variant="primary" text-variant="white">
            <template #header>Vending Machine Problem</template>
            <template #lead>I GEAR GEEK</template>
          </b-jumbotron></b-col
        >
      </b-row>

      <b-row id="btn-sale">
        <b-col col md="12"
          ><b-button href="/sale" variant="danger"
            >กดเพื่อทำการซื้อ</b-button
          ></b-col
        >
      </b-row>
      <h3>Product in stock</h3>
      <div align="center">
        <b-row align-h="center">
          <div v-for="pro in pro.data" :key="pro.data">
            <div v-if="pro.in_stock == true">
              <b-col sm="12" align-self="start">
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

h3 {
  padding: 10px;
}
</style>