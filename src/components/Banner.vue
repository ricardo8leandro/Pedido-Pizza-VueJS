<template>
    <div id="main-banner">
        <h1>Faça sua pizza</h1>
    </div>
</template>
<script>
export default {
    name: "Banner"
}
</script>
<style scoped>
#main-banner {
    background-image: url('/public/img/pizza.jpg');
    background-position: 0 35%;
    background-size: cover;
    height: 400px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
}

#main-banner h1 {
    background-color: #222;
    color: #FFF;
    font-size: 60px;
    text-align: center;
    padding: 40px 60px;
}
</style>
