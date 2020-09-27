<template>
<div id="app">
    <Header></Header>
    <OrderList></OrderList>
</div>
</template>

<script>
import OrderList from "@/components/OrderList.vue";
import Header from "@/components/Header.vue";

export default {
    name: "app",
    components: {
        OrderList,
        Header
    }
};
</script>

<style lang="scss"></style>
