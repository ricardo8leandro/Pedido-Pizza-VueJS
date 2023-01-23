<template>
    <footer id="footer">
        <p>Faça sua Pizza &copy;2022</p>
    </footer>
</template>
<script>
export default {
    name: "Footer"
}
</script>
<style scoped>
#footer {
    height:100px;
    background-color: #222;
    color: #fcba03;
    border-top: 4px solid #111;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    bottom: 0;
    position: fixed;
    margin-top:100px;
}
</style>
