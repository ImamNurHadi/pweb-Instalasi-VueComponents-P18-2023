<template>
    <div class="container mx-auto p-4">
        <div class="bg-gray-100 p-4 rounded-lg shadow-lg mb-4">
            <h1 class="text-3xl font-bold mb-4">Welcome To Our Store!</h1>
            <div>
                <button @click="showAddProductForm = true"
                    class="bg-green-500 hover:bg-green-600 text-white font-semibold px-4 py-2 rounded-md">Add
                    Product</button>
                    
            </div>
        </div>

        <div v-if="showAddProductForm" class="bg-white p-4 rounded-lg shadow-lg">
            <form @submit.prevent="addOrUpdateProduct" class="custom-form">
                <div class="mb-4">
                    <label for="productName" class="block text-sm font-medium text-gray-600"  >Product Name</label>
                    <input v-model="newProduct.name" type="text" id="productName"
                        class="form-input mt-1 block w-full rounded-md ">
                </div>
                <div class="mb-4">
                    <label for="productType" class="block text-sm font-medium text-gray-600">Product Type</label>
                    <select v-model="newProduct.type" id="productType"
                        class="form-select mt-1 block w-full rounded-md ">
                        <option value="Makanan">Makanan</option>
                        <option value="Pakaian">Pakaian</option>
                    </select>
                </div>
                <div class="mb-4">
                    <label for="productPrice" class="block text-sm font-medium text-gray-600">Product Price</label>
                    <input v-model.number="newProduct.price" type="number" id="productPrice"
                        class="form-input mt-1 block w-full rounded-md ">
                </div>
                <div class="mb-4">
                    <label for="productQuantity" class="block text-sm font-medium text-gray-600">Product Quantity</label>
                    <input v-model.number="newProduct.quantity" type="number" id="productQuantity"
                        class="form-input mt-1 block w-full rounded-md ">
                </div>
                <button type="submit" class="bg-green-600 hover:bg-green-500 text-white font-semibold px-4 py-2 rounded-md">{{
                    editingIndex !== null ? 'Save' : 'Add' }}</button>
                <button type="button" @click="cancelForm" class="bg-gray-500 hover:bg-red-500 text-white font-semibold px-4 py-2 rounded-md ml-2" style="width: 50%;">
                   Cancel
        </button>

            </form>
        </div>

        <div class="bg-white p-4 rounded-lg shadow-lg mt-4">
            <table class="table-auto w-full">
                <thead>
                    <tr>
                        <th class="px-4 py-2">Nama</th>
                        <th class="px-4 py-2">Tipe</th>
                        <th class="px-4 py-2">Harga</th>
                        <th class="px-4 py-2">Jumlah</th>
                        <th class="px-4 py-2">Action</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(product, index) in products" :key="index"
                        class="bg-white hover:bg-gray-100 transition duration-300 ease-in-out">
                        <td class="px-4 py-2 text-gray-800">{{ product.name }}</td>
                        <td class="px-4 py-2 text-gray-800">{{ product.type }}</td>
                        <td class="px-4 py-2 text-gray-800">{{ product.price }} Rb</td>
                        <td class="px-4 py-2 text-gray-800">{{ product.quantity }}</td>
                        <td class="px-4 py-2 flex items-center">
                            <button @click="editProduct(index)"
                                class="bg-blue-500 hover:bg-blue-600 text-white font-semibold px-2 py-1 rounded-md  transition duration-300 ease-in-out">
                                Edit
                            </button>
                            <button @click="deleteProduct(index)"
                                class="bg-red-500 hover:bg-red-600 text-white font-semibold px-2 py-1 ml-1 rounded-md transition duration-300 ease-in-out">
                                Delete
                            </button>
                            <div class="form-check ml-2">
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
input{
  border-color: black;
  border-width:0.1vh;
}

select
{
  border-color: black;
  border-width:0.1vh;
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
            editingIndex: null, // Indeks produk yang sedang diedit
        };
    },
    created() {
        // Load products from local storage when the component is created
        const savedProducts = localStorage.getItem('products');
        if (savedProducts) {
            this.products = JSON.parse(savedProducts);
        }
    },
    methods: {
        addOrUpdateProduct() {
            if (this.editingIndex !== null) {
                // Mengganti data produk yang lama dengan data produk yang telah diedit
                this.products.splice(this.editingIndex, 1, { ...this.newProduct });
                this.editingIndex = null;
            } else {
                // Tambahkan produk baru ke dalam array
                this.products.push({ ...this.newProduct });
            }

            // Reset data produk baru
            this.newProduct = {
                name: "",
                type: "",
                price: 0,
                quantity: 0,
            };

            // Tutup form setelah produk ditambahkan atau diedit
            this.showAddProductForm = false;
            localStorage.setItem('products', JSON.stringify(this.products));
        },
        
        cancelForm() {
        this.showAddProductForm = false;
        // Reset nilai newProduct dan editingIndex jika perlu
        this.newProduct = {
            name: "",
            type: "",
            price: 0,
            quantity: 0,
        };
        this.editingIndex = null;
            },


        editProduct(index) {
            // Mengisi data produk baru dengan data produk yang akan diedit
            this.newProduct = { ...this.products[index] };
            // Menyimpan indeks produk yang sedang diedit
            this.editingIndex = index;
            // Menampilkan form tambah produk
            this.showAddProductForm = true;
        },
        deleteProduct(index) {
            // Menghapus produk dari array berdasarkan indeks
            this.products.splice(index, 1);
            localStorage.setItem('products', JSON.stringify(this.products));
        },
        },
        };
</script>
  
  