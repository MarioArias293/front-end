<template>

    <div class="container-grid">
        <h2>Productos</h2>
        <div>
            <button type="button" class="btn btn-success" data-bs-toggle="modal" data-bs-target="#Add" data-bs-whatever="@mdo">Añadir</button>
        </div>        
        <div class="container" >
            <table class="table table-hover" >
            <thead>
                <tr>
                    <th scope="col">id</th>
                    <th scope="col">Nombre</th>
                    <th scope="col">Precio</th>
                    <th scope="col">isService</th>
                    <th scope="col">imgSource</th>
                    <th scope="col">Acciones</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="product in products" v-bind:key="product.id">
                    <th scope="row">{{product.id}}</th>
                    <td>{{product.name}}</td>
                    <td>{{product.price}}</td>
                    <td>{{product.service}}</td>
                    <td>{{product.imgSrc}}</td>
                    <td>
                        <button v-on:click="getModiProductId(product)" type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#Modify" data-bs-whatever="@mdo">Modificar</button>
                        <button v-on:click="getProductId(product.id)" type="button" class="btn btn-danger" data-bs-toggle="modal" data-bs-target="#Delete" data-bs-whatever="@mdo">Borrar</button>
                    </td>
                </tr>
            </tbody>
            </table>
        </div>
    </div>

    <div class="modal fade" id="Delete" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" >
        <div class="modal-dialog">
            <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Escribe id para borrar</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                <form>
                    <h3> ¿Estas seguro de borrar producto con ID: <span>{{idProductDelete}}</span> ?</h3>
                <!-- <div class="mb-3">
                    <label for="recipient-name" class="col-form-label">Id:</label>
                    <input type="text" class="form-control" id="recipient-name" >
                </div> -->
                <!-- <div class="mb-3">
                    <label for="message-text" class="col-form-label">Message:</label>
                    <textarea class="form-control" id="message-text"></textarea>
                </div> -->
                </form>
            </div>
            <div class="modal-footer">
                <button v-on:click="deleteProduct(idProductDelete)" type="button" class="btn btn-danger">Borrar</button>
            </div>
            </div>
        </div>
    </div>

    <div class="modal fade" id="Add" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" >
        <div class="modal-dialog">
            <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Escribe Datos del nuevo producto</h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">

            <!-- form -->      
            <form class="mx-1 mx-md-4">
                <br>
                <div class="d-flex flex-row align-items-center mb-4">
                <i class="fas fa-user fa-lg me-3 fa-fw"></i>
                <div class="form-outline flex-fill mb-0">
                    <input v-model="createProduct.name" type="text" id="form3Example1c" class="form-control" />
                    <label class="form-label" for="form3Example1c">Nombre del Producto</label>
                </div>
                </div>

                <div class="d-flex flex-row align-items-center mb-4">
                <i class="fas fa-lock fa-lg me-3 fa-fw"></i>
                <div class="form-outline flex-fill mb-0">
                    <input v-model="createProduct.price" type="number" id="form3Example4cd" class="form-control" />
                    <label class="form-label" for="form3Example4cd">Precio del producto</label>
                </div>
                </div>

                <div class="d-flex flex-row align-items-center mb-4">
                <i class="fas fa-key fa-lg me-3 fa-fw"></i>
                <select class="dropDownCentroOpciones" v-model="createProduct.service">
                    <option selected :value="true">Producto</option>
                    <option :value="false">Servicio</option>
                </select>    
                </div>

                <div class="d-flex flex-row align-items-center mb-4">
                <i class="fas fa-key fa-lg me-3 fa-fw"></i>
                <div class="form-outline flex-fill mb-0">
                    <input v-model="createProduct.imgSrc" type="text" id="form3Example4cdax" class="form-control" />
                    <label class="form-label" for="form3Example4cdax">imgSrc</label>
                </div>
                </div>

            </form>

            </div>
            <div class="modal-footer">
                <button v-on:click="createAnProduct" type="button" class="btn btn-success" >Crear</button>
            </div>
            </div>
        </div>
    </div>

    <div class="modal fade" id="Modify" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" >
        <div class="modal-dialog">
            <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Escribe datos para modificar producto <span>{{idProductModi.id}}</span></h5>
                <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <!-- form -->      
            <form class="mx-1 mx-md-4">
                <br>
                <div class="d-flex flex-row align-items-center mb-4">
                <i class="fas fa-user fa-lg me-3 fa-fw"></i>
                <div class="form-outline flex-fill mb-0">
                    <input v-model="modifyProduct.name" type="text" id="form3Example1ca" class="form-control" :placeholder="[[idProductModi.name]]" />
                    <label class="form-label" for="form3Example1c">Nombre del Producto</label>
                </div>
                </div>

                <div class="d-flex flex-row align-items-center mb-4">
                <i class="fas fa-lock fa-lg me-3 fa-fw"></i>
                <div class="form-outline flex-fill mb-0">
                    <input v-model="modifyProduct.price" type="number" id="form3Example4c" class="form-control" :placeholder="[[idProductModi.price]]" />
                    <label class="form-label" for="form3Example4c">Precio del producto</label>
                </div>
                </div>

                <div class="d-flex flex-row align-items-center mb-4">
                <i class="fas fa-key fa-lg me-3 fa-fw"></i>
                <select class="dropDownCentroOpciones" v-model="modifyProduct.service" :placeholder="[[idProductModi.service]]">
                    <option selected :value="true">Producto</option>
                    <option :value="false">Servicio</option>
                </select>    
                </div>

                <div class="d-flex flex-row align-items-center mb-4">
                <i class="fas fa-key fa-lg me-3 fa-fw"></i>
                <div class="form-outline flex-fill mb-0">
                    <input v-model="modifyProduct.imgSrc" type="text" id="form3Example4cdax" class="form-control" :placeholder="[[idProductModi.imgSrc]]" />
                    <label class="form-label" for="form3Example4cdax">imgSrc</label>
                </div>
                </div>

            </form>

            <div class="modal-footer">
                <button v-on:click="modifyAnProduct" type="submit" class="btn btn-primary" >Modificar</button>
            </div>
            </div>
        </div>
    </div>    

</template>


<script>   
import gql from "graphql-tag";

export default {
    name: "AdminProducts",

    data: function(){
        return {
            product: [],
            products: [],
            createProduct: {
                name: "",
                price: 0,
                service: false,
                imgSrc: ""
            },
            modifyProduct: {
                name: "",
                price: "",
                service: false,
                imgSrc: ""
            },
            idProductDelete: "",
            idProductModi: ""
        }
    },

    methods: {
        getProductsList: async function(){
            await this.$apollo
            .query({
            query: gql`
                query Products {
                    products {
                        id
                        name
                        price
                        service
                        imgSrc
                    }
                }
                `,
                    
            })
            .then((result) => {
                this.products = result.data.products;
            })
            .catch((error) => {
            alert("ERROR: Fallo geUserData");
            });
        },

        getProductId: function(productID){
            this.idProductDelete = productID;

        },

        getModiProductId: function(product){
            this.idProductModi = product;
        },

        createAnProduct: async function(){
            console.log(typeof(this.createProduct.service));
            await this.$apollo
                .mutate({
                mutation: gql`
                mutation CreateProduct($inputProduct: inProduct!) {
                    createProduct(inputProduct: $inputProduct) {
                        id
                        name
                        price
                        service
                    }
                }
                `,
                variables:{
                    inputProduct: this.createProduct,
                }
            })
            .then((result) => {
                alert("Producto "+result.data.createProduct.name+" creado");
                this.getProductsList();
                this.$forceUpdate();
            })
            .catch((error) => {
            alert("ERROR: Fallo creando producto");
            });

        },

        modifyAnProduct: async function(){
            await this.$apollo
                .mutate({
                mutation: gql`
                mutation UpdateProduct($updateProductId: Int!, $product: updateProduct!) {
                    updateProduct(id: $updateProductId, product: $product) {
                        id
                        name
                        price
                        service
                        imgSrc
                    }
                }
                `,
                variables:{
                    updateProductId: this.idProductModi.id,
                    product: this.modifyProduct
                }
            })
            .then((result) => {
                alert("Producto "+result.data.updateProduct.id+" Modificado");
                this.getProductsList();
                this.$forceUpdate();
                this.modifyProduct = "";
            })
            .catch((error) => {
            alert("ERROR: Fallo creando producto");
            });

        },     

        deleteProduct: async function(productId){
            await this.$apollo
                .mutate({
                mutation: gql`
                mutation DeleteProduct($deleteProductId: Int!) {
                   deleteProduct(id: $deleteProductId)
                }
                `,
                variables:{
                    deleteProductId: productId
                }
            })
            .then((result) => {
                this.getProductsList();
                this.$forceUpdate();
                alert(result.data.deleteProduct);
                
            })
            .catch((error) => {
            alert("ERROR: Fallo eliminando producto");
            });

        }


    },
    created: async function(){
        this.getProductsList();
    }
}


</script>


<style>
    *, ul , li {
        list-style: none;
    }
    ul li > a {
        text-decoration: none;
        color: #000;
    }
    ul {
        display: flex;
        justify-content: center;
        gap: 15px;
    }
    .greetings{
        margin: 0;
        padding: 0%;
        height: 100%;
        width: 100%;
    
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 9.5em;
    }

    .greetings h1{
        font-size: 50px;
        color: #283747;
    }

    .greetings span{
        color: crimson;
        font-weight: bold;
    }

    .container-grid {
        display: grid;
        grid: repeat(2, 1fr);
    }

    .btn .show:active {
        background: rgb(247, 63, 247);
    }

    .signUp_user{
        margin: 40px 0;
    }

    .container_signUp_user {
        border: 3px solid  #5b06a0;
        border-radius: 10px;
        width: 50%;
    }

    .signUp_user form{
        width: 95%;
    }

    .signUp_user input{
        height: 40px;
        width: 100%;
        box-sizing: border-box;
        padding: 10px 20px;
        margin: 5px 0;
        border: 1px solid #5b06a0;
    }

    .signUp_user button{
        width: 100%;
        height: 40px;
        color: #E5E7E9;
        background: #5b06a0;
        border: 1px solid #E5E7E9;
        border-radius: 5px;
        padding: 10px 25px;
        margin: 5px 0 25px 0;
    }

    .signUp_user button:hover{
        color: #E5E7E9;
        background: crimson;
        border: 1px solid #5b06a0;
    }

    textarea {
        width: 100%;
    }

    .dropDownCentroOpciones{
        width: 100%;
        width: 100%;
        height: 40px;
        border: 1px solid #858585;
        border-radius: 5px;
        padding: 10px 25px;
        margin: 5px 0 25px 0;
    }

</style>