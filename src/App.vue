<template>
  <myMenu></myMenu>
  <div class="container-fluid py-4">

    <div :class="{ 'row':cart.length > 0 }">
      <div :class="{ 'col-lg-9':cart.length > 0 }">
        <div class="container">

          <!-- cards filter -->
          <div>
            <h1>Articles</h1>
            <input v-model="searchKey" id="search" type="search" class="form-control" placeholder="Search..."
              autocomplete="off">
            <span v-if="searchKey && filteredList.length >=1 ">
              <b>{{ filteredList.length }}</b> Resultat<span v-if="filteredList.length >= 2">s</span> trouvé<span
                v-if="filteredList.length >= 2">s</span>
            </span>
            <hr>
          </div>
          <div class="row">

            <!-- cards display -->
            <div v-for="phone in filteredList" :key="phone.id" class="col-md-6 col-lg-4 col-xl-3  my-3">
              <div class="card shadow-sm">
                <div class="card-body">
                  <img class="card-img-top" :src="phone.image">
                  <div class="card-img-overlay">
                    <h5 class="text-right"><span class="badge badge-dark badge-pill pb-1">{{ phone.price }} €</span>
                    </h5>
                  </div>

                </div>
                <div class="card-footer bg-dark text-white" style="z-index: 1">
                  <h4 class="card-title">{{ phone.name }}</h4>
                  <p class="card-text">{{ phone.description }}</p>
                  <input hidden id="ok" type="checkbox" class="" name="">
                  <label for="ok" class="btn btn-outline-danger mr-3"><span class="fas fa-heart"></span></label>
                  <button @click.prevent="addToCart(phone)" class="btn btn-outline-primary mb-2 ml-auto">Add to
                    cart</button>
                </div>
              </div>
            </div>

          </div>
        </div>
      </div>
      <transition name="slide-fade">
      <!-- shopping cart display-->
        <div v-if="montreCard" class="col-lg-3 mx-auto">
          <div class="card">
            <div class="card-header bg-dark text-white">
              <h5>Shopping cart</h5>
            </div>
            <div class="card-body" style="max-height: 400px; overflow-x: hidden;padding: 0">
              <table class="table" style="margin-top: -5px">

                <!-- cart items -->
                <transition-group name="fade">
                  <tr v-for="phone in cart" :key="phone.id">
                    <td class="d-flex ">
                      <div class="text-center">
                        <img class="border p-2 my-2 mr-3 img-fluid rounded-circle" width="100" height="100"
                          :src="phone.image">
                      </div>
                      <div class="flex-fill ">
                        <b>{{ phone.price }}€</b>
                        <p>{{ phone.name }}</p>
                        <button @click="minusOne(phone, id)" class="btn btn-outline-warning mr-2"><span
                            class=" fas fa-minus"></span></button>
                        <span class="btn border mr-2">{{ phone.quantity }}</span>
                        <button @click="plusOne(phone)" class="btn btn-outline-primary mr-2"><span
                            class=" fas fa-plus"></span></button>
                        <button @click="removePhone(phone)" class="btn btn-outline-danger mr-2"><span
                            class=" fas fa-trash"></span></button>
                      </div>
                    </td>
                  </tr>
                </transition-group>

              </table>

            </div>
            <div class="card-footer bg-dark text-white">
              <h5>Total <b>{{ voirTotal }}</b></h5>
              <p>Quantity : <b>{{ quantityTotal }}</b></p>
              <button class="btn btn-success w-100 font-weight-bold py-2 text-uppercase">Validate</button>
            </div>
          </div>
        </div>
      </transition>
    

    </div>
  </div>





</template>

<script>
  const phones = [
    { id: 1, name: "Coque iphone X", description: "Coque en silicone TPU antichoc aux coin", price: 7, image: "images/IPHONE X.png" },
    { id: 2, name: "Coque de protection S8", description: "Protection total pour Samsung Galaxy S8", price: 9, image: "images/SAMSUNG S8.png" },
    { id: 3, name: "Gel TPU pour S7", description: "Coque en gel TPU pour Samsung Galaxy S7", price: 5, image: "images/SAMSUNG S7 FLAT.png" },
    { id: 4, name: "Verre trempé Iphone 8", description: "Verre trempé pour protection écran Iphone 8", price: 10, image: "images/IPHONE 8.png" },
    { id: 5, name: "Verre trempé incurvé", description: "Film protection en verre trempé incurvé pour Iphone 8", price: 20, image: "images/IPHONE 6.png" },
    { id: 6, name: "Silicone pour S6", description: "Coque transparent pour Samsung S6", price: 5, image: "images/SAMSUNG S6.png" },
    { id: 7, name: "Verre trempé S7", description: "Protection en verre trempé avec bord curvé pour Samsung Galaxy S7 Edge", price: 10, image: "images/SAMSUNG S7 EDGE.png" },
    { id: 8, name: "Verre trempé Galaxy A5", description: "Protection en verre pour Samsung Galaxy A5 modèle 2016", price: 10, image: "images/SAMSUNG A5.png" },
    { id: 9, name: "Silicone TPU Iphone 7", description: "Coque en Silicone TPU transparent pour Iphone 7", price: 8, image: "images/IPHONE 7.png" }

  ]
  import myMenu from './menu.vue'


  export default {
    components: {
      myMenu
    },
    name: 'App',
    data() {
      return {
        phones: phones,
        searchKey: '',
        cart: [],
        visible: true
      }
    },
    methods: {
      addToCart(phone) {
        for (let i = 0; i < this.cart.length; i++) {
          if (this.cart[i].id === phone.id) {
            return this.cart[i].quantity++;
          }
        }
        this.cart.push({
          id: phone.id,
          image: phone.image,
          name: phone.name,
          price: phone.price,
          quantity: 1
        })
      },
      plusOne(phone) {
        phone.quantity = phone.quantity + 1
      },
      removePhone(phone) {
        this.cart = this.cart.filter((i) => i !== phone)
      },

      minusOne(phone) {
        if (phone.quantity == 1) {
          this.removePhone(phone);
        } else {
          phone.quantity = phone.quantity - 1
        }
      },

      toggle() {
        this.visible = !this.visible
      }

    },
    computed: {
      filteredList() {
        return this.phones.filter((phone) => {
          return phone.description.toLowerCase().includes(this.searchKey.toLowerCase());
        })
      },
      voirTotal() {
        let total = 0;
        for (let item in this.cart) {
          total = total + (this.cart[item].quantity * this.cart[item].price);
        }
        return total;
      },
      quantityTotal() {
        let x = 0;
        for (let i in this.cart) {
          x = x + this.cart[i].quantity;
        }
        return x;
      },
      montreCard(){
        if(this.cart.length > 0) {
         return true
        }
        return false
      }

    }

  }
</script>

<style>
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity .5s;
  }

  .fade-enter,
  .fade-leave-to

  /* .fade-leave-active below version 2.1.8 */
    {
    opacity: 0;
  }

  .slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
</style>