<template>
  <div>
    <Header />
  </div>

  <div class="main">
    <form @submit="submitProduct" class="form-main">
        <h2>{{currentMode}}</h2>
        <div class="form-field">
            <label>Product Name</label><br>
            <input class="form-textbox" type="text" v-model="productName" name="productName" placeholder="Add Product">
        </div>
        <div class="form-field">
            <label>Description</label><br>
            <input class="form-textbox" type="text" v-model="description" name="description" placeholder="Add Description">
        </div>
        <div class="form-field">
            <label>Price</label><br>
            <input class="form-textbox" type="text" v-model="price" name="price" placeholder="Add Price">
        </div>
        <div class="form-field">
            <label>Enable Product?</label><br>
            <input class="form-checkbox" type="checkbox" v-model="enabled" name="enabled">
        </div>
        <input type="submit" value="Add/Edit" class="submit-button">
    </form>

    <div class="product">
      <Products
        @toggle-enable="toggleEnable"
        @edit-product="editProduct"
        @delete-product="deleteProduct"
        :products="products" 
      />
    </div>   
  </div>
</template>

<script>
import Header from './components/Header';
import Products from './components/Products';

export default {
  name: 'App',
  components: {
    Header,
    Products,
  },
  data() {
    return {
      products: [],
      productName: '',
      description: '',
      price: '',
      enabled: false,
      addMode: true,
      currentMode: 'Add Products'
    }
  },
  methods: {
    toggleEnable(id) {
      this.products = this.products.map((product) => product.id === id ?
       {...product, enabled: !product.enabled} : product );
    },
    deleteProduct(id) {
      this.products = this.products.filter((product) => product.id !== id);
    },
    editProduct(product) {
      this.addMode = false;
      this.currentMode = 'Edit Product';
      console.log(this.products.length);

      this.id = product.id;
      this.productName = product.productName;
      this.description = product.description;
      this.price = product.price;
      this.enabled = product.enabled;;
    },
    submitProduct(e) {
      e.preventDefault();

      if(!this.productName) {
        alert('Please add a product');
        return;
      }

      const newProduct = {
        id: Math.floor(Math.random() * 100000),
        productName: this.productName,
        description: this.description,
        price: this.price,
        enabled: this.enabled,
      }

      if(this.addMode === true) {
        this.products = [...this.products, newProduct];
      } else {
        this.products[this.products.length - 1].productName = newProduct.productName;
        this.products[this.products.length - 1].description = newProduct.description;
        this.products[this.products.length - 1].price = newProduct.price;
        this.products[this.products.length - 1].enabled = newProduct.enabled;

        this.addMode = true;
        this.currentMode = "Add Products";
      }

      this.productName = '';
      this.description = '';
      this.price = '';
      this.enabled = false;
    },
  },
  created() {
    this.products = [
        {
            id: 1,
            productName: 'Sunburst',
            description: 'A bouquet of pink, white, and violet two-toned blooms and a sunflower.',
            price: '₱999',
            enabled: true,
        },
        {
            id: 2,
            productName: 'Ever After',
            description: 'A bouquet of mixed blooms consisting of lilies and carnations.',
            price: '₱1599',
            enabled: true,
        },
        {
            id: 3,
            productName: 'Beautiful You',
            description: 'A bouquet of a dozen fresh red roses arranged in a classic arm bouquet.',
            price: '₱1299',
            enabled: true,
        },
    ]
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: 'Poppins', sans-serif;
  }

  .main {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    margin-top: 30px;
  }

  .form-main {
        background: #fcc9b9;
        border: 2px solid #f7aa92;
        border-radius: 5px;
        margin-top: 50px;
        padding: 20px;
        width: 350px;
        height: 400px;
  }

  .form-field {
      margin-bottom: 15px;
  }

  .form-textbox {
      width: 300px;
      height: 35px;
      padding: 10px;
  }

  .form-checkbox {
      width: 20px;
      height: 20px;
  }

  .submit-button {
      background: #f4f4f4;
      padding: 5px;
      border: black;
      border-radius: 5px;
      width: 100px;
      height: 25px;
      cursor: pointer;
  }
</style>
