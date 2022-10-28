<template>
    <div class="modal modal-md fade" id="modalAddProduct" tabindex="-1" role="dialog" aria-labelledby="modalAddProduct" aria-hidden="true">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="modalAddProduct">Add Product</h5>
                </div>
                <div class="modal-body">
                    <form>
                        <!-- Product Title -->
                        <div class="form-group mb-3">
                            <div class="inputHeader d-flex">
                                <i class="fas fa-pen text-primary"></i>
                                <label for="productTitle">Title</label>
                            </div>
                            <input type="text" class="form-control" id="productTitle" v-model="produtTitle">
                        </div>

                        <!-- Product Price -->
                        <div class="form-group mb-3">
                            <div class="inputHeader d-flex">
                                <i class="fas fa-tag text-primary"></i>
                                <label for="productPrice">Price</label>
                            </div>
                            <input type="text" class="form-control" id="productPrice" v-model="productPrice">
                        </div>

                        <!-- Product Description -->
                        <div class="form-group mb-3">
                            <div class="inputHeader d-flex">
                                <i class="fas fa-pen text-primary"></i>
                                <label for="productDescription">Description</label>
                            </div>
                            <textarea style="resize: none; height: 100px;" class="form-control" id="productDescription" v-model="productDescription"></textarea>
                        </div>

                        <!-- Product Image URL -->
                        <div class="form-group mb-3">
                            <div class="inputHeader d-flex">
                                <i class="fas fa-image text-primary"></i>
                                <label for="productImageUrl">Image Url</label>
                            </div>
                            <input type="text" class="form-control" id="productImageUrl" v-model="productImageUrl">
                        </div>

                        <!-- Product Category -->
                        <div class="form-group mb-3">
                            <div class="inputHeader d-flex">
                                <i class="fas fa-filter text-primary"></i>
                                <label for="productCategory">Category</label>
                            </div>
                            <input type="text" class="form-control" id="productCategory" v-model="productCategory">
                        </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-outline-secondary" @click="closeAddProductModal">Close</button>
                    <button type="button" class="btn btn-primary" @click="addNewProduct">Add Product</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import "jquery";
import "bootstrap";
import axios from "axios";

export default {
    name: "modalAddProduct",

    data() {
        return {
            // Data Vars to Post
            produtTitle: "",
            productPrice: "",
            productDescription: "",
            productImageUrl: "",
            productCategory: "",
        }
    },

    methods: {
        openModalAddProduct() {
            $('#modalAddProduct').modal('show') // Method to Call open the Modal from anywhere
        },

        addNewProduct() {

            // Post Object
            let data = {
                title: this.produtTitle,
                price: this.productPrice,
                description: this.productDescription,
                image: this.productImageUrl,
                category: this.category,
            }

            axios.post("https://fakestoreapi.com/products", data)
            .then(res => {
                $('#modalAddProduct').modal('hide'); // Close Modal after Posting Object
            })
            .catch(err => console.log(err))
        },

        closeAddProductModal() {
            $('#modalAddProduct').modal('hide'); // Close Modal
        }
    },
}
</script>

<style scoped>
.inputHeader i {
    margin: 0 7px 1px 0;
    align-self: center;
    font-size: 15px;
}
</style>