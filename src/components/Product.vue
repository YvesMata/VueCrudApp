<template>
    <div :class="[product.enabled ? 'enabled' : '', 'product']">
        <div class="data-container">
            <h3>{{product.productName}}</h3>
            <p>{{product.description}}</p>
            <p>{{product.price}}</p>
        </div>
        
        <div class="btn-container">
            <button @click="$emit('toggle-enable', product.id)" style="background: #00e60c;">Enable/Disable</button>
            <button @click="$emit('edit-product', product)" style="background: #ff8b26;" id="edit-button">Edit</button>
            <button @click="$emit('delete-product', product.id)" style="background: #ff2e2e;" id="delete-button">Delete</button>
        </div>
        
    </div>
</template>

<script>
    export default {
        name: 'Product',
        props: {
            product: Object,
        },
    }
</script>

<style scoped>
    .product {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        background: #f4f4f4;
        margin: 5px;
        padding: 10px 20px;
        color: #a6a6a6;
    }

    .product.enabled {
        border-left: 5px solid green;
        color: #000;
    }

    .product h3 {
        display: flex;
        align-items: center;
        justify-content: space-between;
    }

    .btn-container {
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        align-items: center;
    }

    button {
        padding: 5px;
        margin: 5px;
        border: none;
        border-radius: 5px;
        width: 100px;
        height: 25px;
        color: white;
        cursor: pointer;
    }
</style>
