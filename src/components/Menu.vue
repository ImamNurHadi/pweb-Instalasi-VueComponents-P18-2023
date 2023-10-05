<template>
    <div class="container mx-auto p-4">
        <div class="bg-gray-100 p-4 rounded-lg shadow-lg mb-4">
            <h1 class="text-3xl font-bold mb-4">Our stock</h1>
            <div>
                <button @click="showAddProductForm = true"
                    class="bg-green-500 hover:bg-green-600 text-white font-semibold px-4 py-2 rounded-md">Add
                    Product</button>
                <button @click="toggleMakananTable"
                    class="bg-blue-500 hover:bg-blue-600 text-white font-semibold px-4 py-2 rounded-md ml-4"> {{
                        showMakananTable ? 'Hide Electronic' : 'Show Electronic' }}</button>
                <button @click="togglePakaianTable"
                    class="bg-blue-500 hover:bg-blue-600 text-white font-semibold px-4 py-2 rounded-md ml-4">{{
                        showPakaianTable ? 'Hide Wearable' : 'Show Wearable' }}</button>
                <button @click="toggleAccessoriesTable"
                    class="bg-blue-500 hover:bg-blue-600 text-white font-semibold px-4 py-2 rounded-md ml-4">{{
                        showAccessoriesTable ? 'Hide Accessories' : 'Show Accessories' }}</button>
            </div>
        </div>

        <div v-if="showAddProductForm" class="bg-white p-4 rounded-lg shadow-lg">
            <form @submit.prevent="addOrUpdateProduct" class="custom-form">
                <div class="mb-4">
                    <label for="productName" class="block text-sm font-medium text-gray-600">Product Name</label>
                    <input v-model="newProduct.name" type="text" id="productName"
                        class="form-input mt-1 block w-full rounded-md pl-3">
                </div>
                <div class="mb-4">
                    <label for="productType" class="block text-sm font-medium text-gray-600">Product Type</label>
                    <select v-model="newProduct.type" id="productType" class="form-select mt-1 block w-full rounded-md ">
                        <option value="Electronic">Electronic</option>
                        <option value="Wearable">Wearable</option>
                        <option value="Accessories">Accessories</option>
                    </select>
                </div>
                <div class="mb-4">
                    <label for="productPrice" class="block text-sm font-medium text-gray-600">Product Price</label>
                    <select v-model.number="newProduct.price" id="productPrice"
                        class="form-select mt-1 block w-full rounded-md">
                        <option value="10">10</option>
                        <option value="15">15</option>
                        <option value="20">20</option>
                        <option value="25">25</option>
                        <option value="30">30</option>
                    </select>
                </div>

                <div class="mb-4">
                    <label for="productQuantity" class="block text-sm font-medium text-gray-600">Product Quantity</label>
                    <input v-model.number="newProduct.quantity" type="number" id="productQuantity"
                        class="form-input mt-1 block w-full rounded-md pl-3 py">
                </div>
                <button type="submit"
                    class="bg-green-600 hover:bg-green-500 text-white font-semibold px-4 py-2 rounded-md">{{
                        editingIndex !== null ? 'Save' : 'Add' }}</button>
                <button type="button" @click="cancelForm"
                    class="bg-gray-500 hover:bg-red-500 text-white font-semibold px-4 py-2 rounded-md ml-2">
                    Cancel
                </button>

            </form>
        </div>

        <div v-if="showMakananTable" class="bg-white p-4 rounded-lg shadow-lg mt-4">
            <h2 class="text-2xl font-semibold mb-2">Electronic</h2>
            <table class="table-auto w-full">
                <thead>
                    <tr>
                        <th class="px-4 py-2">Name</th>
                        <th class="px-4 py-2">Type</th>
                        <th class="px-4 py-2">Price</th>
                        <th class="px-4 py-2">Quantity</th>
                        <th class="px-4 py-2">Action</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(product, index) in filteredProducts('Electronic')" :key="index"
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
                            <button @click="deleteProduct(product.id)"
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

        <div v-if="showPakaianTable" class="bg-white p-4 rounded-lg shadow-lg mt-4">
            <h2 class="text-2xl font-semibold mb-2">Wearable</h2>
            <table class="table-auto w-full">
                <thead>
                    <tr>
                        <th class="px-4 py-2">Name</th>
                        <th class="px-4 py-2">Type</th>
                        <th class="px-4 py-2">Price</th>
                        <th class="px-4 py-2">Quantity</th>
                        <th class="px-4 py-2">Action</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(product, index) in filteredProducts('Wearable')" :key="index"
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
                            <button @click="deleteProduct(product.id)"
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

        <div v-if="showAccessoriesTable" class="bg-white p-4 rounded-lg shadow-lg mt-4">
            <h2 class="text-2xl font-semibold mb-2">Accessories</h2>
            <table class="table-auto w-full">
                <thead>
                    <tr>
                        <th class="px-4 py-2">Name</th>
                        <th class="px-4 py-2">Type</th>
                        <th class="px-4 py-2">Price</th>
                        <th class="px-4 py-2">Quantity</th>
                        <th class="px-4 py-2">Action</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(product, index) in filteredProducts('Accessories')" :key="index"
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
                            <button @click="deleteProduct(product.id)"
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




        <!-- <div class="bg-white p-4 rounded-lg shadow-lg mt-4">
            <table class="table-auto w-full">
                <thead>
                    <tr>
                        <th class="px-4 py-2">Name</th>
                        <th class="px-4 py-2">Type</th>
                        <th class="px-4 py-2">Price</th>
                        <th class="px-4 py-2">Quantity</th>
                        <th class="px-4 py-2">Action</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(product, index) in products" :key="index"
                        class="bg-white hover:bg-gray-100 transition duration-300 ease-in-out">
                        <td class="px-4 py-2 text-gray-800">{{ product.name }}</td>
                        <td class="px-4 py-2 text-gray-800">{{ product.type }}</td>
                        <td class="px-4 py-2 text-gray-800">$ {{ product.price }}</td>
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
        </div> -->
    </div>
</template>
  

<style>
input {
    border-color: black;
    border-width: 0.1vh;
}

select {
    border-color: black;
    border-width: 0.1vh;
}
</style>

<script>
export default {
    data() {
        return {
            products: [],
            showAddProductForm: false,
            showMakananTable: true,
            showPakaianTable: true,
            showAccessoriesTable: true,
            newProduct: {
                id: null,
                name: "",
                type: "",
                price: "",
                quantity: "",
            },
            editingIndex: null,
        };
    },
    created() {
        const savedProducts = localStorage.getItem('products');
        if (savedProducts) {
            this.products = JSON.parse(savedProducts);
        }
    },
    methods: {
        filteredProducts(type) {
            return this.products.filter(product => product.type === type);
        },

        addOrUpdateProduct() {
            if (this.newProduct.price >= 0 && this.newProduct.quantity >= 0) {
                if (this.editingIndex !== null) {
                    this.products.splice(this.editingIndex, 1, { ...this.newProduct });
                    this.editingIndex = null;
                } else {
                    const newId = Date.now(); // Generate a unique id
                    this.products.push({ ...this.newProduct, id: newId }); // Set the id 
		    }

            this.newProduct = {
                name: "",
                type: "",
                price: "",
                quantity: "",
            };

            this.showAddProductForm = false;
	        localStorage.setItem('products', JSON.stringify(this.products));
            } else {
            alert('Masukkkan format yang valid!');
            }
        },


        toggleMakananTable() {
            this.showMakananTable = !this.showMakananTable;
        },

        togglePakaianTable() {
            this.showPakaianTable = !this.showPakaianTable;
        },

        toggleAccessoriesTable() {
            this.showAccessoriesTable = !this.showAccessoriesTable;
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
            this.newProduct = { ...this.products[index] };
            this.editingIndex = index;
            this.showAddProductForm = true;
        },
        deleteProduct(id) {
            const index = this.products.findIndex(product => product.id === id);
            if (index !== -1) {
                this.products.splice(index, 1);
                localStorage.setItem('products', JSON.stringify(this.products));
            }
        }
    },
};
</script>
  
  