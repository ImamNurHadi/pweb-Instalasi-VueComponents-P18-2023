<template lang="">
    <div class="container">
        <div class="container-teks">
            Welcome To Our Store!
            <div>
                <button @click="showAddProductForm = true" class="btn btn-success">Add Product</button>
                
            </div>
            
        </div>

            <!-- Jika klik add product -->
            <div v-if="showAddProductForm" class="add-product-form">
                <form @submit.prevent="addProduct">
                <div class="form-group">
                    <label for="productName">Product Name</label>
                    <input v-model="newProduct.name" type="text" class="form-control" id="productName" required>
                </div>
                <div class="form-group">
                    <label for="productType">Product Type</label>
                    <select v-model="newProduct.type" class="form-control" id="productType">
                    <option value="Makanan">Makanan</option>
                    <option value="Pakaian">Pakaian</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="productPrice">Product Price</label>
                    <input v-model.number="newProduct.price" type="number" class="form-control" id="productPrice" required>
                </div>
                <div class="form-group">
                    <label for="productQuantity">Product Quantity</label>
                    <input v-model.number="newProduct.quantity" type="number" class="form-control" id="productQuantity" required>
                </div>
                <button type="submit" class="btn btn-primary">Add</button>
                </form>
            </div>


        <div class="container-card">
                    <table class="table-auto">
            <thead>
                <tr>
                <th>Nama</th>
                <th>Tipe</th>
                <th>Harga</th>
                <th>Jumlah</th>
                <th>Action</th>

                </tr>
            </thead>
            <tbody>
                <tr  v-for="(product, index) in products" :key="index">
                <td>{{ product.name }}</td>
                <td>{{ product.type }}</td>
                <td>{{ product.price }}</td>
                <td>{{ product.quantity }}</td>
                <td>
                    <div class="form-check">
                    <input class="form-check-input" type="checkbox" value="" id="flexCheckChecked" checked>
                    </div>
                </td>
               
                </tr>
            </tbody>
            </table>
        </div>
    </div>
</template>



<style>
    .container
    {
        display: flex;
        flex-direction: column; /* Mengatur tata letak elemen vertikal */
        align-items: center; /* Mengatur konten di tengah horizontal */
        height: 100vh; /* Untuk mengisi tinggi layar secara penuh */
    }
    .container-teks
    {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 20%;
        height: 20%;
        margin-top: 1%;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
        
    }
    .container-card
    {
        display: flex;
        max-width: 80%;
        padding: 1%;
        width: auto;
        height: auto; 
        margin-top: 5%;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
    }

    .add-product-form
    {
        display: flex;
        justify-content: center;

        width: 50vh;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;   
    }

    table {
    width: 100%; /* Mengisi lebar tabel ke seluruh lebar kontainer */
  }

  table, th {
    padding: 10px; /* Mengatur jarak dalam sel */
    text-align: center; /* Mengatur teks menjadi rata tengah */
  }

  tr:first-child {
    font-weight: bold; /* Menambahkan tebal pada teks pada baris pertama */
  }

  button.tadd
  {
    background-color: red;
    border-radius: 2vh;
  }
</style>

<script>
        export default {
        data() {
            return {
        products: [], // Data produk
        showAddProductForm: false, // Status tampilan form tambah produk
        newProduct: {
            name: "",
            type: "",
            price: 0,
            quantity: 0,
                    },
                   };
                },
        methods: {
            // ...
            addProduct() {
            // Tambahkan produk baru ke dalam array
            this.products.push({ ...this.newProduct });
            
            // Reset data produk baru
            this.newProduct = {
                name: "",
                type: "",
                price: 0,
                quantity: 0,
            };

            // Tutup form setelah produk ditambahkan
            this.showAddProductForm = false;
            },
        },
        // ...  
        }
</script>