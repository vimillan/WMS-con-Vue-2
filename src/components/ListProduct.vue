<template>
    <div>
        <ul>
            <li v-for="(producto, index) in productos" :key="index">
                {{ producto.nombre }} - {{ producto.sku }} - {{ producto.cantidad }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "ListProduct",
    props: {
        productos: {
            type: Array,
            required: true
        }
    }
};
</script>