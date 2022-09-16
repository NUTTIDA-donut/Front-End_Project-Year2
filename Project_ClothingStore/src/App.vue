<script setup>
import { ref, computed, onBeforeUpdate } from "vue";
// ข้อ2
const thisColor = ref("");
const thisSize = ref("28px");
const thisDecoration = ref("");
const thisWeight = ref("normal")
const thisText = ref("Nuttida");


const selectedColor = ref("");
const selectedSize = ref("28px");
const selectedDecoration = ref("");
const selectedWeight = ref("normal")
const editText = () => {
  return (showEditText.value = true);
};
const showEditText = ref(false);
const newText = ref("");

const changeManage = () =>{
  thisColor.value = selectedColor.value
  thisSize.value = selectedSize.value
  thisDecoration.value = selectedDecoration.value
  thisWeight.value = selectedWeight.value
  thisText.value = newText.value;
  showEditText.value = false;
  newText.value = "";
}
const reset = () => {
  thisColor.value = "";
  thisDecoration.value = "";
  thisWeight.value  = ref("normal")
  thisSize.value = "28px";
  thisText.value = "Nuttida";
};
const ManageText = ref(false);
const showManageText = () => (ManageText.value = true);
const closeManageText = () => (ManageText.value = false);

//show products
const products = [
  {
    name: "Baby Tee",
    price: 490,
    path: "../public/images/Baby_Tee.jpg",
  },
  {
    name: "Neck Top",
    price: 690,
    path: "../public/images/Neck_Top.jpg",
  },
  {
    name: "Dad Tee",
    price: 590,
    path: "../public/images/Dad_Tee.jpg",
  },
  {
    name: "Crop Top",
    price: 390,
    path: "../public/images/Crop_Top.jpg",
  },
  {
    name: "Bandana",
    price: 490,
    path: "../public/images/Bandana.jpg",
  },
  {
    name: "Tennis Skirt",
    price: 690,
    path: "../public/images/Tennis_Skirt.jpg",
  },
  {
    name: "Sleeve Tee",
    price: 590,
    path: "../public/images/Sleeve_Tee.jpg",
  },
  {
    name: "Brown Tee",
    price: 690,
    path: "../public/images/Brown_Tee.jpg",
  },
];



const addToCart = (index) => {
  const productAdd = products[index];
  console.log(productAdd);
  countProductInCart.value += 1
  return cart.value.push(productAdd);
};

const selectedPrice = ref()

const showProducts = ref(products)

const filterPrice = () => { 
  console.log(selectedPrice.value);
  return  showProducts.value = products.filter((product) => product.price <= selectedPrice.value)
}

//cart
const cart = ref([]);
const deleteProduct = (index) => {
  countProductInCart.value -= 1
  return cart.value.splice(index,1)
}


//Payment

const totalPrice = computed(() => {
  return cart.value.reduce((Total, cart) => Total + cart.price, 0);
});

const countProductInCart = ref(0)
// const countProductInCart = computed(() => cart.value.length);



</script>

<template>
  <div class="font">
    <!-- 2. -->
    <div>
      <!-- Text -->
      <h1 class="textSize mt-2 text-right">
        Hi , {{ thisText }}
        <button @click="showManageText">
          <img src="./assets/pen.png" width="30" />
        </button>
      </h1>
      <!-- Manage Text -->
      <div v-show="ManageText" class="mr-2 text-right">
        <!-- choose color -->
        <div class="mt-2">
          <select
            class="bg-blue-50 border border-black"
            v-model="selectedColor"
          >
            <option disabled value="">Please select color</option>
            <option value="red">red</option>
            <option value="yellow">yellow</option>
            <option value="green">green</option>
            <option value="blue">blue</option>
            <option value="purple">purple</option>
          </select>
          <!-- show color -->
          <span class="box border border-black">{{ selectedColor }}</span>
        </div>
        <!-- choose size -->
        <div class="mt-2">
          <select class="bg-blue-50 border border-black" v-model="selectedSize">
            <option disabled value="">Please select size</option>
            <option value="32px">32px</option>
            <option value="64px">64px</option>
            <option value="72px">72px</option>
            <option value="96px">96px</option>
            <option value="108px">108px</option>
          </select>
        </div>
        <!-- choose decoration -->
        <div class="mt-2">
          <select
            class="bg-blue-50 border border-black"
            v-model="selectedDecoration"
          >
            <option disabled value="">Please select decoration</option>
            <option value="overline">overline</option>
            <option value="line-through">line through</option>
            <option value="underline">underline</option>
          </select>
        </div>
        <!-- choose weight -->
        <div class="mt-2">
          <select
            class="bg-blue-50 border border-black"
            v-model="selectedWeight"
          >
            <option disabled value="">Please select weight</option>
            <option value="normal">normal</option>
            <option value="bold">bold</option>
            <option value="900">extra bold</option>
          </select>
        </div>
        <!-- Change Name -->
        <div class="mt-2">
          <button
            @click="editText"
            class="mr-2 bg-blue-50 border-2 border-black"
          >
            Change Name
          </button>
          <span v-show="showEditText">
            <input
              type="text"
              class="border-2 border-black"
              v-model="newText"
            />
          </span>
        </div>
        <!-- Reset & Close -->
        <div class="mt-4 text-right">
           <button
            @click="changeManage"
            class="bg-red-100 mx-2 border-2 border-black"
          >
            Change
          </button>
          <button @click="reset" class="bg-red-100 mr-2 border-2 border-black">
            Reset
          </button>
          
          <button
            @click="closeManageText"
            class="bg-red-100 border-2 border-black"
          >
            Close
          </button>
        </div>
      </div>
    </div>
    <div class="text-center font-extrabold text-5xl">Virginheart Shop</div>
    <div class="mx-8 mt-4">Price lower than : 
       <select
            class="bg-stone-50 border border-black"
            v-model="selectedPrice"
          >
            <option disabled value="">Please select Price</option>
            <option value="500">500</option>
            <option value="1000">1000</option>
       </select>
       <button class="ml-2 bg-stone-200 border border-black" @click="filterPrice">OK</button>
    </div>
    <div class="grid grid-cols-2">


      <!-- 1. & 3. -->
      <!-- show product -->
      <div class="product-container grid grid-cols-2 p-10">
        <div
          v-for="(product, index) in showProducts"
          class="flex flex-col bg-white rounded-lg shadow-md m-5 product text-center"
        >
          <img :src="product.path" class="rounded-md" />
          <p class="font-bold text-2xl mt-4">{{ product.name }}</p>
          <p class="font-regular text-lg mt-2">{{ product.price }} bath</p>
          <button
            @click="addToCart(index)"
            class="bg-black text-white rounded-md mx-28 mt-4"
          >
            add to cart
          </button>
        </div>
      </div>
      <!-- Cart -->
      <div class="mt-12">
        <h2 class="text-3xl font-bold text-center">Your Cart</h2>
        <!-- product in cart -->
        <table class="w-full mt-4">
          <tr v-show="countProductInCart !== 0" class="bg-gray-200 text-left">
            <th>Product</th>
            <th>Name</th>
            <th>Price</th>
            <th></th>
          </tr>
          <tr v-for="(product, index) in cart" class="border">
            <td><img :src="product.path" width="100" /></td>
            <td>{{ product.name }}</td>
            <td>{{ product.price }}</td>
            <td><button @click="deleteProduct(index)"><img src="./assets/bin.png" width="20"></button></td>
          </tr>
        </table>
        <div v-show="countProductInCart===0" class="mt-5 text-2xl text-center font-bold border rounded-md py-5 mx-16">
          Your cart is empty
        </div>
        <!-- Payment Summary -->
        <div v-if="countProductInCart !== 0">
          <h2 class="text-3xl font-bold text-center mt-4">Payment Summary</h2>
          <div class="border mt-4">
            <h3>Count : {{ countProductInCart }}</h3>
            <h3>Total : {{ totalPrice }}</h3>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scope>
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
.font {
  font-family: "Poppins", sans-serif;
}
.box {
  width: 300px;
  height: 100px;
  padding-left: 20px;
  padding-right: 20px;
  background-color: v-bind(selectedColor);
}
.textSize {
  font-size: v-bind(thisSize);
  background-color: v-bind(thisColor);
  text-decoration: v-bind(thisDecoration);
  font-weight: v-bind(thisWeight);
}
</style>
