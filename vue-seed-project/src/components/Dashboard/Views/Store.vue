<template>
<div>
<div class="container" >
<head>
<link href="//netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet" id="bootstrap-css">
</head>
<div>
<label> Product Name    </label>
<input type="text" v-model="name"> </input>
</div>
<div>
<label> Product Price   </label>
<input type="text" v-model="price"> </input>       <a href="#" class="btn btn-primary" v-on:click="addItem"><b>+</b> Add new Product</a>
</div>
<label> Seller Name    </label>
<input type="text" v-model="sellername"> </input>
<div>
<label>______________________________________________________________ </label>
</div>
<div>
<label> Product ID   </label>
<input type="text" v-model="prodID"> </input>        <a href="#" class="btn btn-primary" v-on:click="deleteRow"><b>-</b> Delete Product</a>
</div>
<div>
<label>______________________________________________________________ </label>
</div>
<label> Product ID    </label>
<input type="text" v-model="prodID2"> </input>
</div>
<div>
<label> Product Name   </label>
<input type="text" v-model="name2"> </input>        <a href="#" class="btn btn-primary" v-on:click="updateRow"><b></b> Update Product</a>
</div>
<div>
<label> Product Price     </label>
<input type="text" v-model="price2"> </input>
</div>


  <div class="row col-lg-20 col-md-15 custyle">
  <table class="table table-striped custab">
  <thead>

      <tr>
          <th class="text-center">Product ID</th>
          <th class="text-center">Name</th>
          <th class="text-center">Price</th>
          <th class="text-center">Created at</th>
          <th class="text-center">Updated at</th>
          <th class="text-center">Seller Name</th>
          <th class="text-center">Action</th>
      </tr>
  </thead>
          <tr v-for="item in product.data">
              <td class="text-center">{{item._id}}</td>
              <td class="text-center">{{item.name}}</td>
              <td class="text-center">{{item.price}}</td>
              <td class="text-center">{{item.createdAt}}</td>
              <td class="text-center">{{item.updatedAt}}</td>
              <td class="text-center">{{item.sellerName}}</td>
              <td class="text-center"><a class='btn btn-info btn-xs' href="#"><span class="glyphicon glyphicon-edit"></span> Update</a> <a href="#" class="btn btn-danger btn-xs"><span class="glyphicon glyphicon-remove" value="Delete" v-on:Click="deleteRow(item._id)"></span> Delete</a></td>
              <br></br>
          </tr>
  </table>
  </div>
</div>
</div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      product: [],
      name: '',
      price: '',
      sellername: '',
      prodID: '',
      name2: '',
      price2: '',
      prodID2: ''
    }
  },
  created () {
    this.showItem()
  },
  methods: {
    showItem: function () {
      axios.get('http://localhost:3000/api/product/getProducts')
      .then((response) => {
        this.product = response.data
        console.log(response)
      })
    },
    addItem () {
      axios.post('http://localhost:3000/api/product/createProduct', {
        sellerName: this.sellername,
        name: this.name,
        price: this.price
      })
      .then((response) => {
        window.location.reload()
        console.log(response)
      })
    },
    deleteRow () {
      axios.delete('http://localhost:3000/api/product/deleteProduct/' + this.prodID)
      .then((response) => {
        window.location.reload()
        console.log(response)
      })
    },
    updateRow () {
      axios.patch('http://localhost:3000/api/product/updateProduct/' + this.prodID2, {
        name: this.name2,
        price: this.price2
      })
      .then((response) => {
        window.location.reload()
        console.log(response)
      })
    }
  }
}

</script>

<style>
.custab{
    border: 1px solid #ccc;
    padding: 5px;
    margin: 5% 0;
    box-shadow: 3px 3px 2px #ccc;
    transition: 0.5s;
    padding: 0;
    height: auto;
    }
.custab:hover{
    box-shadow: 3px 3px 0px transparent;
    transition: 0.5s;
    }
</style>
