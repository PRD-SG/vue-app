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
        <b-col md="12">
        <span v-if="re != false">
          <h2>{{message}}</h2>
        </span>
        <span v-else>
          <h2>{{message}}</h2>
        </span>
          
          <div class="insert">
            <span v-if="re != false">
              <b-button @click="append(1)" class="btn">Coins 1</b-button>
              <b-button @click="append(2)" class="btn">Coins 2</b-button>
              <b-button @click="append(5)" class="btn">Coins 5</b-button>
              <b-button @click="append(10)" class="btn">Coins 10</b-button>
              <b-button @click="clear" variant="warning">Clear</b-button>
              <b-button @click="exit" variant="danger">Exit</b-button>
            </span>
            <div class="ale" v-if="change == null">
              <b-alert show variant="primary">
                Total Coins : {{ total }} Baht</b-alert>
            </div>

            <div class="ale" v-if="change != null">
              <div v-if="change == 0">
                <b-alert show variant="danger">
                 no change
                </b-alert>
              </div>
              <div v-else>
                  <b-alert show variant="danger">
                    <p> Insert Coins : {{ totals}} Baht </p>
                    <p> Change Coins : {{ change }} Baht  </p>
                      <div class="text-center">
                        <b-button variant="danger">
                          Coins 10 : <b-badge variant="light">{{ coins10 }} เหรียญ</b-badge>
                        </b-button>
                        <b-button variant="danger">
                          Coins 5 : <b-badge variant="light">{{ coins5 }} เหรียญ</b-badge>
                        </b-button>
                        <b-button variant="danger">
                          Coins 2 : <b-badge variant="light">{{ coins2 }} เหรียญ</b-badge>
                        </b-button>
                        <b-button variant="danger">
                          Coins 1 : <b-badge variant="light">{{ coins1 }} เหรียญ</b-badge>
                        </b-button>
                      </div>                   
                  </b-alert>
              
                </div>
               
               <b-alert show variant="warning">
                 Auto reload page in 8 seconds
               </b-alert>
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
                        @click="select(pro.price, total, pro.id)"
                        variant="warning">Selected</b-button>
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
      totals:0,
      re: true,
      change: null,
      sale: false,
      time: 5,
      coins10: 0,
      coins5: 0,
      coins2: 0,
      coins1: 0,
      message: 'Insert coins',
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
    select(number1, number2, id) {
      console.log("price : " + number1);
      console.log("total : " + number2);
      console.log("chang : " + (number2 - number1));
      console.log('id product :'+id);
      this.totals = number2
      this.total = 0;
      this.change = number2 - number1;
      window.scrollTo(0, 0);
      this.num2coins(this.change);
      setTimeout(function(){ 
        location.reload(); 
       },8000);
      this.re = false;
      this.message = 'Change coins';
    },
    selectproduct() {
        this.sale = true;
    },
    exit() {
        this.sale = false;
        this.change = null;
        this.total = 0;
    },
    num2coins(number){
      let ten = (number-(number%10))/10
      let five = ((number%10)-(number%10)%5)/5
      let one = ((number % 5)%2)
      let two = two = ((number-((ten*10)+(five*5))) - one)/2
        console.log('Ten : '+ (ten)); 
        this.coins10 = (ten);
        console.log('five : '+(five)); 
        this.coins5 = (five);
        console.log('Two : '+(two));
        this.coins2 = (two);
        console.log('One : '+(one));
        this.coins1 = (one);
      console.log((ten*10)+(five*5)+(two*2)+one);
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