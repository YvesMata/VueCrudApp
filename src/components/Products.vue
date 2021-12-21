<template>
    <div :key="product.id" v-for="product in products">
        <Product
            @toggle-enable="$emit('toggle-enable', product.id)"
            @edit-product="$emit('edit-product', product)"
            @delete-product="$emit('delete-product', product.id)"
            :product="product"
        />
    </div>
</template>

<script>
    import Product from './Product';

    export default {
        name: 'Products',
        props: {
            products: Array,
        },
        components: {
            Product
        },
        emits: ['toggle-enable', 'edit-product', 'delete-product']
    }
</script>

<style>
    
</style>
