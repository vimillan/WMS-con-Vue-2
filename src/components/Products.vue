<template>
    <div>
        <div class="center-item gap-2 justify-content-between mb-3">
            <div class="fs-18">Productos</div>
            <button class="btn btn-primary center rounded-xs hw-35" data-bs-toggle="modal"
                data-bs-target="#mdlAddProduct">
                <i class="bx bx-plus icon-md"></i>
            </button>
        </div>

        <!-- Lista de Productos -->
        <ListProduct :productos="productosLista" />

        <!-- Agregar producto -->
        <div class="modal fade" id="mdlAddProduct" tabindex="-1" aria-labelledby="mdlAddProductLabel"
            aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered">
                <div class="modal-content rounded-xl">
                    <div class="modal-header center-item justify-content-between">
                        <div class="center-item gap-3">
                            <div class="hw-45 bg-primary-op center rounded-circle text-primary">
                                <i class="bx bx-plus icon-lg center"></i>
                            </div>
                            <h5 class="font-weight-bold text-black m-0 p-0">Agregar producto</h5>
                        </div>
                        <button type="button" class="btn btn-outline-close hw-30 rounded center p-0"
                            data-bs-dismiss="modal" aria-label="Close" id="btnClose" @click="resetForm">
                            <i class="bx bx-x icon-lg"></i>
                        </button>
                    </div>
                    <div class="modal-body fs-14">
                        <form @submit.prevent="handleSubmit">
                            <div class="form-group mb-2">
                                <label for="nombreProducto" class="mb-1">Nombre</label>
                                <input type="text" class="form-control" id="nombreProducto"
                                    placeholder="Ingresa el nombre" v-model="producto.nombre" />
                                <div v-if="errors.nombre" class="text-danger">{{ errors.nombre }}</div>
                            </div>
                            <div class="row">
                                <div class="col-lg-6">
                                    <div class="form-group mb-2">
                                        <label for="skuProducto" class="mb-1">SKU</label>
                                        <input type="text" class="form-control" id="skuProducto" v-model="producto.sku"
                                            placeholder="Ingresa el SKU" />
                                        <div v-if="errors.sku" class="text-danger">{{ errors.sku }}</div>
                                    </div>
                                </div>
                                <div class="col-lg-6">
                                    <div class="form-group mb-2">
                                        <label for="cantidadProducto" class="mb-1">Cantidad</label>
                                        <input type="number" class="form-control" id="cantidadProducto" min="1"
                                            v-model.number="producto.cantidad" placeholder="Ingresa la cantidad" />
                                        <div v-if="errors.cantidad" class="text-danger">{{ errors.cantidad }}</div>
                                    </div>
                                </div>
                            </div>
                        </form>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-outline-primary rounded-xs" data-bs-dismiss="modal"
                            aria-label="Close" @click="resetForm">
                            Cancelar
                        </button>
                        <button type="submit" class="btn btn-primary rounded-xs" @click="handleSubmit">
                            Guardar
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import ListProduct from "./ListProduct.vue"

export default {
    name: "Products",
    components: {
        ListProduct,
    },
    data() {
        return {
            producto: {
                nombre: '',
                sku: '',
                cantidad: 1
            },
            errors: {},
            productosLista: []
        };
    },
    methods: {
        validateForm() {
            this.errors = {};

            if (!this.producto.nombre) {
                this.errors.nombre = 'El nombre es obligatorio.';
            } else if (!/^[\w\s-]+$/.test(this.producto.nombre)) {
                this.errors.nombre = 'Sólo se permiten letras, números, guiones y guiones bajos.';
            }

            if (!this.producto.sku) {
                this.errors.sku = 'El SKU es obligatorio.';
            } else if (!/^[a-zA-Z0-9-_]+$/.test(this.producto.sku)) {
                this.errors.sku = 'Sólo se permiten letras, números, guiones y guiones bajos.';
            } else if (this.productosLista.some(p => p.nombre === this.producto.nombre)) {
                this.errors.nombre = 'Este producto ya existe.';
            }

            if (this.producto.cantidad < 1) {
                this.errors.cantidad = 'La cantidad debe ser al menos 1.';
            }

            return Object.keys(this.errors).length === 0;
        },
        handleSubmit() {
            if (this.validateForm()) {
                this.productosLista.push({ ...this.producto });
                this.resetForm();
                //falta mensaje
            }
        },
        resetForm() {
            this.producto = {
                nombre: '',
                sku: '',
                cantidad: 1
            };
            this.errors = {};
            this.closeModal();
        },
        closeModal() {
            const closeMdl = document.getElementById('btnClose');
            if (closeMdl) {
                closeMdl.click()
            }
        }
    }
};
</script>