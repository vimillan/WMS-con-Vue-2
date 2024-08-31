<template>
    <div class="px-2 py-1">
        <div class="border rounded-xs mb-2 row justify-content-between gap-1" v-for="(producto, index) in productos"
            :key="index">
            <div class="col-lg-8 px-2 py-1">
                <div class="center-item gap-3">
                    <div class="center p-2 bg-primary-op text-primary rounded-xs hw-35">
                        <i class='bx bx-package icon-slg'></i>
                    </div>
                    <div>
                        <div class="fw-bold fs-16">{{ producto.nombre }}</div>
                        <div class="fs-12">{{ producto.sku }}</div>
                    </div>
                </div>
            </div>
            <div class="col-lg">
                <div class="text-underline mt-3 mb-1" data-bs-toggle="collapse" :href="'#cllpsProducto-' + index"
                    role="button" aria-expanded="false" :aria-controls="'cllpsProducto-' + index"
                    @click="editarProducto(index)">
                    <div class="fs-14 mb-1">{{ producto.cantidad }} en almacén</div>
                </div>
                <div class="collapse" :id="'cllpsProducto-' + index">
                    <div class="center-item gap-3 no-wrap align-items-end mb-3">
                        <div class="col p-0">
                            <label for="cantidadProducto" class="mb-1">Cantidad</label>
                            <input type="number" class="form-control" id="cantidadProducto" min="1"
                                v-model.number="tempProd.cantidad" placeholder="Ingresa la cantidad" />
                            <div v-if="errors.cantidad" class="text-danger">{{ errors.cantidad }}</div>
                        </div>
                        <button class="btn btn-primary rounded-xs" @click="guardarCantidad(index)">Guardar</button>
                        <button class="btn btn-outline-danger p-1 center hw-35 rounded-xs" data-bs-toggle="collapse"
                            :href="'#cllpsProducto-' + index" role="button" aria-expanded="false"
                            :aria-controls="'cllpsProducto-' + index">
                            <i class="bx bx-x icon-md"></i>
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ListProduct",
    data() {
        return {
            tempProd: {
                nombre: '',
                sku: '',
                cantidad: 1
            },
            errors: {},
        };
    },
    props: {
        productos: {
            type: Array,
            required: true
        }
    },
    methods: {
        editarProducto(index) {
            this.tempProd = { ...this.productos[index] };
            this.currentIndex = index;
        },
        guardarCantidad(index) {
            if (this.validateForm()) {
                this.$emit('update-producto', { index: this.currentIndex, cantidad: this.tempProd.cantidad });
                this.resetForm();
            }
        },
        validateForm() {
            this.errors = {};
            if (this.tempProd.cantidad < 1) {
                this.errors.cantidad = 'La cantidad debe ser al menos 1.';
            }
            return Object.keys(this.errors).length === 0;
        },
        resetForm() {
            this.tempProd = { nombre: '', sku: '', cantidad: 1 };
            this.errors = {};
            const collapse = document.getElementById(`cllpsProducto-${this.currentIndex}`);
            if (collapse) {
                const bsCollapse = new bootstrap.Collapse(collapse, {
                    toggle: false
                });
                bsCollapse.hide();
            }
        }
    }
};
</script>