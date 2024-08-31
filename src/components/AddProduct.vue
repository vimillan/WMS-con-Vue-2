<template>
    <div class="modal fade" id="mdlAgregarTipoTablero" aria-hidden="true" aria-labelledby="mdlAgregarTipoTableroLabel"
        tabindex="-1">
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content rounded-xl">
                <div class="modal-header center-item justify-content-between">
                    <div class="center-item gap-3">
                        <div class="hw-45 bg-primary-op center rounded-circle text-primary">
                            <i class="bx bx-plus icon-lg center"></i>
                        </div>
                        <h5 class="font-weight-bold text-black m-0 p-0">Agregar producto</h5>
                    </div>
                    <button type="button" class="btn btn-outline-close hw-30 rounded center p-0" data-dismiss="modal"
                        aria-label="Close">
                        <i class="bx bx-x icon-lg"></i>
                    </button>
                </div>
                <div class="modal-body fs-14">
                    <div class="form-group">
                        <label for="nombreProducto" class="mb-1">Nombre</label>
                        <input type="text" class="form-control" id="nombreProducto" placeholder="Ingresa el nombre">
                    </div>
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="form-group">
                                <label for="skuProducto" class="mb-1">SKU</label>
                                <input type="text" class="form-control" id="skuProducto" placeholder="Ingresa el SKU">
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="form-group">
                                <label for="cantidadProducto" class="mb-1">Cantitad</label>
                                <input type="number" class="form-control" id="cantidadProducto" min="1"
                                    placeholder="Ingresa el nombre">
                            </div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-outline-primary rounded-xs" data-dismiss="modal"
                        aria-label="Close">Cancelar</button>
                    <button type="button" class="btn btn-primary rounded-xs" data-dismiss="modal"
                        aria-label="Close">Guardar</button>
                </div>
            </div>
        </div>
    </div>

    <div class="modal fade" id="mdlAddProduct" tabindex="-1" aria-labelledby="mdlAddProductLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content rounded-xl">
                <div class="modal-header center-item justify-content-between">
                    <div class="center-item gap-3">
                        <div class="hw-45 bg-primary-op center rounded-circle text-primary">
                            <i class="bx bx-plus icon-lg center"></i>
                        </div>
                        <h5 class="font-weight-bold text-black m-0 p-0">Agregar producto</h5>
                    </div>
                    <button type="button" class="btn btn-outline-close hw-30 rounded center p-0" data-bs-dismiss="modal" aria-label="Close">
                        <i class="bx bx-x icon-lg"></i>
                    </button>
                </div>
                <div class="modal-body">
                    ...
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary " data-bs-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-primary">Save changes</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "AddProduct",
    data() {
        return {
            producto: {
                nombre: '',
                sku: '',
                cantidad: 1
            },
            errors: {},
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
            }

            if (this.producto.cantidad < 1) {
                this.errors.cantidad = 'La cantidad debe ser al menos 1.';
            }

            return Object.keys(this.errors).length === 0;
        },
        handleSubmit() {
            if (this.validateForm()) {
                this.$emit('producto-agregado', this.producto);
                console.log('Producto agregado:', this.producto);
                this.resetForm();
                // Aquí puedes añadir el producto al array local o hacer cualquier otra acción necesaria
            }
        },
        resetForm() {
            this.producto = {
                nombre: '',
                sku: '',
                cantidad: 1
            };
            this.errors = {};
        }
    }
};
</script>