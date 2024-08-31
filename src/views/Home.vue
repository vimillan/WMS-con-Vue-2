<template>
    <div>
        <Navbar />
        <div class="mt-4 container">
            <Header />
            <Products />
        </div>
    </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import Header from "../components/Header.vue";
import Products from "../components/Products.vue"

export default {
    name: "Home",
    components: {
        Navbar,
        Header,
        Products,
    },
};
</script>

<style>
@import '../assets/css/main.css';
@import '../assets/css/layout.css';
@import '../assets/css/colors.css';
@import '../assets/css/buttons.css';
@import '../assets/css/modal.css';
@import '../assets/css/images.css';
@import '../assets/css/typography.css';
@import '../assets/css/tables.css';
</style>