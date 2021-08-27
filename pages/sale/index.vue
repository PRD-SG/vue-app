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
            <b-button v-on:click="data.coins1 += 1">Add 1</b-button>
            <b-button v-on:click="data.coins2 += 2">Add 2</b-button>
            <b-button v-on:click="data.coins5 += 5">Add 5</b-button>
            <b-button v-on:click="data.coins10 += 10">Add 10</b-button>
            <h2>
              coins :
              {{ data.coins1 + data.coins2 + data.coins5 + data.coins10 }}
            </h2>
            <b-button v-on:click="total(10)">Add</b-button>
          </div>
        </b-col>
      </b-row>

      <b-row id="b-row"> </b-row>
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
  data() {
    return {
      data: {
        coins1: 0,
        coins2: 0 * 2,
        coins5: 0 * 5,
        coins10: 0 * 10,
      },
    };
  },
  methode: {
    total: function(coins) {
        this.coins = coins;
        console.log(coins);
    },
  },
};
</script>
ß
<style scoped>
#b-row {
  margin: 1%;
}

.insert {
  background-color: aquamarine;
  height: 10px;
}
</style>